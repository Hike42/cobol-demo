# cobol-demo

Projet COBOL de démonstration pour essayer Cobblestone (tests unitaires COBOL locaux avec GnuCOBOL).

Les sources sont un sous-ensemble **batch** d'[AWS CardDemo](https://github.com/aws-samples/aws-mainframe-modernization-carddemo)
(commit `59cc6c2`), une application mainframe de cartes de crédit publiée par AWS sous licence Apache 2.0.
Les écrans CICS/BMS, JCL, IMS et MQ n'ont pas été repris. Les fichiers sont copiés sans modification.

## Contenu

| Dossier | Rôle |
|---|---|
| `cobol/` | 10 programmes batch |
| `copybooks/` | COPY et déclaration DB2 (`DCLTRTYP.dcl`) utilisés par ces programmes |
| `data/` | Données d'exemple ASCII de CardDemo |
| `cobblestone.config.json` | Configuration du projet pour Cobblestone |

| Programme | Ce qu'il fait | Intérêt pour les tests |
|---|---|---|
| `CBACT01C` | Lit les comptes, écrit plusieurs formats de sortie | Appel `COBDATFT` (assembleur) à bouchonner |
| `CBACT02C`, `CBACT03C`, `CBCUS01C` | Listent cartes, références croisées, clients | Programmes simples, lecture de fichier |
| `CBACT04C` | Calcule les intérêts mensuels par catégorie | Calculs décimaux (`1300-COMPUTE-INTEREST`) |
| `CBTRN01C`, `CBTRN02C` | Valident et comptabilisent les transactions du jour | Règles de rejet, mises à jour de soldes |
| `CBTRN03C` | Produit le rapport des transactions | Totaux, ruptures, fichier de sortie |
| `CSUTLDTC` | Valide une date via `CEEDAYS` | Paramètres LINKAGE, appel LE à bouchonner |
| `COBTUPDT` | Met à jour la table `TRANSACTION_TYPE` | SQL `INSERT` / `UPDATE` / `DELETE` simulé |

La plupart des programmes lisent des fichiers indexés (VSAM) : testez-les paragraphe par paragraphe
en positionnant la WORKING-STORAGE, plutôt qu'en exécution complète.

## Utilisation

Dans Cobblestone, choisissez ce dossier comme projet. Les suites sont créées dans `tests/`.

## Licence

Apache 2.0, voir [`LICENSE`](LICENSE) et [`NOTICE`](NOTICE). © Amazon.com, Inc. or its affiliates.
