# Notes de mise à jour (2026-11-23)

Informations recueillies pour mettre à jour l'Excel master (`Balcon Mariana Vmax.xlsx`, Drive). Les CSV (`budget.csv`, `taches.csv`) n'ont **pas** été modifiés: l'utilisateur régénère les CSV depuis l'Excel.

Le dashboard publié reflète l'état du 2026-08-27.

## Heures

- **Max** (CRM, module `RealisationMandat`, deal « Mariana Balcon »): 3 487,50 $ au total (45 $/h), dernière entrée le 2026-09-09. Nouvelles entrées après le 17 août: 3 sept. (3 h, 135 $) et 9 sept. (« Installation garde 1er étage », 5 h 20, 240 $). Solde net après 2 000 $ comptant et 74,69 $ de crédit: **1 412,81 $** (publié: 1 037,81 $).
- **Entrée CRM « Vide »** (2-9 sept., 173 h 30, 7 807,50 $): chronomètre resté ouvert, **à ignorer** et à corriger dans le CRM.
- **Yves**: total de **135 h** (confirmé par Yves). À 45 $/h: 6 075 $, moins 2 000 $ comptant = **4 075,00 $** (publié: 767,50 $, basé sur 61,5 h au 1er août). Suppose que 2 000 $ est le seul paiement.
- **JD** (état de compte de JD daté 2026-09-19, PDF local non versionné): 228,58 h, **12 431,10 $** de travaux (+ 900 $ vs la feuille du 16 août: 1er sept. 371,25 $, 5 sept. 225 $, 6 sept. 303,75 $). Dépenses associées: 1 939,84 $. Acomptes appliqués: 10 665,57 $ (2 000 $ le 31 juil. + 1 285,57 $ « remboursement outils » le 13 juil. + **7 380 $ « compensation » le 5 sept.**). **Solde net à payer à JD: 3 705,37 $** (12 431,10 + 1 939,84 - 10 665,57). Publié: 9 050,36 $ = 11 531,10 + 804,83 (dépenses jusqu'au 14 août) - 3 285,57 (acomptes d'alors), donc l'écart est expliqué. Aucune heure de JD après le 6 sept. dans cet état.
- Le béton de 1 508,47 $ (ligne « Qui = JD » dans `budget.csv`) n'apparaît pas dans les dépenses de JD: il est dans ER-00234 (Max).

## Paiement du 5 sept. 2026 (note de JD)

11 650 $ disponibles, séparés ainsi (soldes de l'époque, arrêtés au 16-27 août):

| | Solde avant | Payé | Reste |
|---|---|---|---|
| Yves | 2 667,47 $ (= 767,50 hrs + 1 899,97 Lab St-Antoine) | 2 650 $ | 17,47 $ |
| Max | 1 627,95 $ (= 1 037,81 hrs + 590,14 ER-00230) | 1 620 $ | 7,95 $ |
| JD | 9 050,36 $ | 7 380 $ | 1 670,36 $ |

- Les lignes « Non Payé » publiées d'Yves, Max et JD (hrs, Lab St-Antoine, ER-00230) étaient donc **réglées le 5 sept.**, sauf les petits restes ci-dessus. Le « Non Payé » du dashboard est périmé pour ces lignes.
- JD: 1 670,36 $ + 900 $ d'heures de sept. + 1 135,01 $ de dépenses après le 14 août = 3 705,37 $ (état du 19 sept.). Concordant.
- **Conflit Yves:** le règlement du 5 sept. utilise 61,5 h (au 1er août). Si Yves a 135 h au total, 73,5 h (3 307,50 $) n'étaient pas dans ce règlement: solde Yves = 6 075 + 1 899,97 - 2 000 - 2 650 = **3 324,97 $**.
- **Max après le 5 sept.** (estimé): 7,95 + 135 (3 sept.) + 240 (9 sept.) + 127,47 (ER-00234 sans béton) + 310,73 (ER-00236) = **821,15 $**. Les heures du 3 sept. n'étaient pas dans son solde du 5 sept.
- Question ouverte: le béton de 1 508,47 $ (ER-00234, ligne « JD, Payé ») n'est dans aucun de ces soldes. Qui l'a avancé et a-t-il été remboursé?

## Reconstitution des paiements de Mariana

| Date | Montant | Pour | Source / fiabilité |
|---|---|---|---|
| ≈ 13-17 juil. 2026 (« avant les vacances »; inscrit au 31 juil. chez JD) | 6 000 $ cash, divisé 3 x 2 000 $ (Max, Yves, JD) | acompte main-d'œuvre | MS_EtatCompte20260827, YVES_EtatCompte20260801, états de JD (compensation datée 2026-07-31). Date réelle approximative. |
| 2026-07-13 | 1 285,57 $ | « remboursement outils » à JD | États de JD. Payeur à confirmer. |
| 2026-09-05 | 11 650 $ (JD 7 380 / Yves 2 650 / Max 1 620) | règlement des soldes | Note de JD + état de JD (compensation 2026-09-05). Date précise. |
| sans date | 4 366,63 $ | Métaux (Acier Picard + galvanisation Corbec), payé directement par Mariana | budget.csv. Commande acier le 2026-07-09: paiement ≈ juillet. |
| sans date | 546,25 $ | Express bac (facture 154896), sur le crédit de Mariana | budget.csv. Conteneur réservé le 2026-07-20. |
| sans date | 3 779,42 $ | Canac 2012900466 (livraison du bois ≈ 27-29 juil.), compte d'Yves | budget.csv. Payeur et date du remboursement à confirmer. |
| sans date | 1 863,75 $ | Hrs Marc (fibre de verre, cash) | budget.csv. Payeur et date à confirmer (travaux 1-12 août). |
| crédit | 74,69 $ | membrane Canac reprise par Max, déduite de son solde | MS_EtatCompte. |

- Simplex: truelle 53,07 $ (facture 184622, payée par la carte de MFI le 2026-06-25) et tapeuse 48,32 $ sont refacturées à Mariana par **MFI-000003** (101,40 $, émise le 2026-08-06, échéance le 2026-08-21, solde dû 101,40 $ à l'émission). **Payée par Mariana** (confirmé par Max le 2026-11-23); date du paiement inconnue (probablement entre le 6 et le 21 août, ou après l'échéance). À lire dans Zoho Books (organisation Maillon Fort, introuvable via le connecteur).
- Tarière portative 98,56 $ (Simplex 210028, 2026-07-27): impayée au relevé Simplex du 2026-08-03. Deux autres factures (149,10 $ et 115,07 $) du même relevé sont d'un autre projet.
- Béton sur mesure 1 508,47 $ (ER-00234): avancé par JD à environ 90 % (dire de Max), à confirmer.

## Dépenses (export Zoho Expense `ZohoExpenseRapport.csv`)

- ER-00229 (808,19 $) et ER-00230 (590,14 $): déjà dans le budget publié.
- ER-00234 « Mariana AutreGars » (1 653,19 $): contient le béton de 1 508,47 $ **déjà publié** (ligne JD), confirmé même dépense. Reste 144,72 $, dont 17,25 $ de gravier déjà dans ER-00229, soit **127,47 $ nouveaux**.
- ER-00236 « mariana 03 » (310,73 $, septembre): **nouveau**.
- Doublon dans ER-00229: deux lignes de 5,05 $ (2025-06-21 et 2026-06-21), probablement une seule dépense.
- Dates douteuses (2021, 2022, 2025): Home Depot 66,27 $ et Canac 2,20 $ dans ER-00234 pourraient ne pas être de ce chantier.
- Tous les rapports sont au statut `draft` dans Zoho.

## Total

Avec ces ajustements (Max, Yves, JD à 3 705,37 $, nouvelles dépenses), le total « reste à payer + payé » serait de **25 194,15 $** (49,2 % de 51 237,09 $). Publié: 26 418,44 $. Attention: la ligne de JD est maintenant un solde après un acompte de 7 380 $, donc ce total n'est plus comparable au coût total des travaux (qui inclut les acomptes).

## Budget

- `Vmax`: 51 299,30 $. Constante `BUDGET` de `index.html`: 51 237,09 $ (écart de 62,21 $).

## Tâches

Terminées par confirmation de l'utilisateur: installation des clôtures métalliques, installation des marches, mur d'intimité (encore « À faire » dans `taches.csv`).
