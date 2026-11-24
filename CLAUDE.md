# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Contexte

Dashboard de suivi de chantier fourni à une cliente (Mariana) pour des travaux de construction (garage/dalle béton, balcon 2e, métal/acier, finitions…). Le projet est en **français** (UI, données, commits). Les données sont mises à jour périodiquement à la main; le code change rarement. Remote: `maximesavard-hue/mariana-dashboard` sur GitHub (branche `main`).

Intervenants dans les données: JD, Yves, Max (Maxime), Marc, MFI, Mariana.

## Architecture

Pas de build, pas de dépendances, pas de tests, pas de lint. Site statique:

- `index.html` — toute l'app (HTML + CSS + JS inline dans un seul fichier, ~45 Ko).
- `taches.csv` — tâches du chantier (source de vérité pour les sections Tâches et Achats).
- `budget.csv` — dépenses réelles (source de vérité pour la section Budget).
- `Archive/` — copies de sauvegarde des deux CSV (format de dates différent, voir plus bas). Ne pas lire comme source active.

Au chargement, `init()` dans `index.html` fait un `fetch('taches.csv?v=<Date.now()>')` et `fetch('budget.csv?v=...')` (cache-busting), parse avec `parseCSV()` puis rend les sections dans le DOM. **Le dashboard doit donc être servi via HTTP** (ouvrir `index.html` en `file://` bloque `fetch`).

Pour tester localement: `python -m http.server 8000` dans le dossier, puis ouvrir `http://localhost:8000`.

### Points clés de `index.html`

- `parseCSV()`: détecte le délimiteur (`;` ou `,`), enlève le BOM, normalise les en-têtes (accents/espaces/casse retirés) puis les mappe via `keyMap` vers des clés internes (`Date Butoire`→`dateButoire`, `Date début`→`deb`, `Date fin`→`fin`, `Responsable`→`resp`, `Fournisseurs`→`fournisseur`, `Dépense Réel`→`desc`…). **Ajouter une colonne utile au rendu = ajouter son entrée dans `keyMap`.** Les colonnes Blocants / Task Dependency / Question existent dans le CSV mais ne passent pas par `keyMap`.
- Les lignes de `taches.csv` sont séparées par **type**: `Action`/`Logistique` → section tâches par zone (`renderZones`); `Achat`/`Location` → section achats (`renderAchatZones`). Les zones sont groupées par la colonne `Zone`, dans l'ordre d'apparition dans le CSV; `Step` donne le numéro d'étape.
- Statuts reconnus (via `statCls`, insensible aux accents/casse): Fait, En cours, Bloqué, À faire, À valider, Annulé. Un statut inconnu n'est pas mappé proprement — rester dans cette liste.
- **Budget**: la constante `BUDGET = 51237.09` est **codée en dur** dans `init()`; `REEL` = somme des `Montant` de `budget.csv`. Les montants sont au format québécois (`1 037,81  $`, virgule décimale, parenthèses = négatif). Statut de paiement: `Payé` / `Non Payé` (détection par sous-chaîne « pay » sans « non »).
- Le tableau `_DATA` dans `init()` (« DONNÉES LEGACY SUPPRIMÉES ») est du code mort laissé en place — il n'est plus utilisé, les données viennent des CSV. Peut être supprimé.

## Mise à jour des données (tâche la plus fréquente)

1. Éditer `taches.csv` et/ou `budget.csv` (séparateur `;`, encodage UTF-8 avec BOM — conserver le BOM si l'éditeur le permet; Excel l'ajoute à l'enregistrement « CSV UTF-8 »).
2. Dates dans `taches.csv`: format `j-m-aaaa` (ex. `15-6-2026`), géré par `parseDate`/`fmtDate`. Les numéros de série Excel et les dates ISO sont aussi tolérés. `Date Butoire` peut valoir `À Valider`.
3. `Qty` utilise la virgule décimale (`0,5`).
4. Dans `budget.csv`, la colonne `mode` est `Cash` (heures/main-d'œuvre) ou `Depense` (achats); `Qui` = qui a avancé/doit être payé. Les notes renvoient à des rapports d'heures externes (« Rapport hrs MS », « rapport hrs JD ») qui ne sont pas dans le repo.
5. Historique des commits: un commit par mise à jour, message court en français (« MAJ des depenses », « hrs Marc »…). Les mises à jour touchent généralement aussi `Archive/*.csv`.
6. Pousser sur `main` pour publier (le site est servi depuis ce repo; l'hébergement exact — probablement GitHub Pages — n'est pas documenté dans le repo).

## Décisions de l'utilisateur

- `Archive/` est un ancien instantané qui a divergé des CSV actifs (dates ISO, lignes « Remise 2000 » séparées). Il n'a pas été mis à jour le 2026-11-23; ne pas le recopier sans demander. Le projet est près de se terminer: ne pas sur-ingénierer.
- Heures de Max: elles viennent du module CRM `RealisationMandat` (deal « Mariana Balcon », id 5493866000023141057). Ignorer l'enregistrement « Vide » (173 h, 7 807,50 $, 2-9 sept. 2026): chronomètre resté ouvert, non valide.
- `ZohoExpenseRapport.csv` (export Zoho Expense, non versionné) contient des courriels: ne jamais le publier sur GitHub (dépôt public).
- **Ne pas modifier `budget.csv` ni `taches.csv`** sans demande explicite: l'utilisateur met à jour l'Excel master (`Balcon Mariana Vmax.xlsx`, Drive) puis régénère les CSV. Les nouvelles informations (heures de Max et de Yves, ER-00234/ER-00236, tâches terminées) sont consignées dans `NOTES_MAJ.md`.
- Publication: via GitHub (push sur `main`).

## Sources externes des données

- Heures: courriels (boîtes Immobilis et Maillon Fort).
- Dépenses: rapports de dépenses Zoho (Immobilis) dont le nom contient « Mariana ».
