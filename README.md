# Temps de parole vs Votes - Présidentielles 2017 & 2022

Analyse du ratio entre le temps de parole médiatique des candidats et le nombre de voix obtenues au premier tour des élections présidentielles françaises de 2017 et 2022.

## Contenu

- **Programme Go** : télécharge les CSV de temps de parole 2022 depuis data.gouv.fr, agrège les données et calcule les ratios
- **Page HTML** : visualisation interactive avec Chart.js (4 graphiques, 3 onglets)

## Structure du projet

```
tempsparole/
├── main.go          # Programme Go principal
├── config.yaml      # URLs des sources de données
├── data.json        # Données statiques (résultats + temps de parole 2017)
├── index.html       # Graphiques interactifs (Chart.js)
├── go.mod
└── go.sum
```

## Utilisation

### Programme Go

```bash
go run main.go
```

Le programme :
1. Lit les URLs depuis `config.yaml`
2. Télécharge les 3 CSV Arcom pour le temps de parole 2022
3. Lit les données statiques depuis `data.json` (résultats élections + temps de parole 2017)
4. Affiche un tableau par élection avec le ratio secondes de parole / voix

### Graphiques

Ouvrir `index.html` dans un navigateur. Trois vues disponibles :
- **2017** / **2022** : graphiques par année
- **Comparaison** : superposition des données pour les 7 candidats présents aux deux scrutins

## Sources de données

| Donnée | Source | Format |
|--------|--------|--------|
| Temps de parole 2022 | [Arcom via data.gouv.fr](https://www.data.gouv.fr/datasets/temps-de-parole-des-candidats-election-presidentielle-2022/) | CSV (téléchargé à l'exécution) |
| Temps de parole 2017 | [CSA via politologue.com](https://www.politologue.com/Presidentielle2017/TempsParole/) | JSON (dans data.json) |
| Résultats 2017 | [Conseil constitutionnel](https://www.conseil-constitutionnel.fr/actualites/resultats-officiels-du-premier-tour-de-l-election-presidentielle) | JSON (dans data.json) |
| Résultats 2022 | [Conseil constitutionnel](https://presidentielle2022.conseil-constitutionnel.fr/les-communiques/resultats-du-premier-tour.html) | JSON (dans data.json) |

Toutes les URLs sont référencées dans `config.yaml`.

## Le ratio

```
ratio = temps_de_parole_en_secondes / nombre_de_voix_au_1er_tour
```

Plus le ratio est élevé, plus le candidat a bénéficié de temps de parole par voix obtenue. Les petits candidats ont mécaniquement un ratio élevé grâce à la règle d'égalité stricte imposée par le CSA/Arcom en fin de campagne.
