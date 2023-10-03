# TP Pandas : Analyse des données COVID-19 avec Jupyter Notebook

Bienvenue dans ce TP dédié à l'utilisation de `pandas` dans un environnement Jupyter Notebook ! Vous allez explorer, traiter et visualiser des données réelles relatives à la pandémie de COVID-19.

## Prérequis

- Assurez-vous d'avoir installé Jupyter Notebook et la bibliothèque `pandas`.
- Si ce n'est pas encore fait, installez ces outils à l'aide de pip :
  ```bash
  conda activate cours
  # et/ou
  pip install jupyter pandas notebook
  ```

## Données

Vous allez travailler sur un fichier JSON accessible à cette URL : https://pomber.github.io/covid19/timeseries.json

**Format du JSON :**
```json
{
  "Afghanistan": [
    {
      "date": "2020-1-22",
      "confirmed": 0,
      "deaths": 0,
      "recovered": 0
    },
    ...
  ]
  ...
}
```

## Instructions

### Étape 1 : Importation des données

Voir le [TP ici](https://ue12-p23-numerique.readthedocs.io/en/latest/2-12-pandas-TP-covid-nb.html)


#### Pour télécharger les données

```python
import pandas as pd

url = "https://pomber.github.io/covid19/timeseries.json"


import requests
response = requests.get(url)

by_countries = response.json()
```

On vérifie que c'est correctement chargé

```python

list(by_countries.keys())[0:4]
```

#### Manipulation pour structurer les données correctements

```python
data = []
for country in by_countries:
    data_for_country = [d | { "country": country } for d in by_countries[country]]
    data += data_for_country
df = pd.DataFrame(data)
```

#### On vérifie que les données sont correctement structurées

On utile `.info` `.head` `.describe` `.dtypes` etc.

Est-ce qu'il n'y a pas un problème de type ? Comment le régler (indice chez vous, `.to_<nouveau_type>...`)

### Étape 2 : On s'intéresse à la France

1. Comment filtrer les données françaises dans un DataFrame `df_france` ?
2. On peut faire de jolie graphe sur le nombre de mort en france

### Etape 3 : Nombre de morts par jour/semaine/mois en france

1. On pense à bien ordonné les colonnes par date
2. On regarde la doc de `df.diff` et on en déduit comment connaitre le nombre de mort d'un jour sur l'autre
3. On créer des nouvelles colonnes 'deaths_by_day' et 'deaths_by_week'
4. On fait des **beaux** graphes avec ces données

#### Etape 4 : On veut maintenant comparer entre les pays.

1. Pourquoi on ne peut pas faire cela directement ?
2. Il y a une base de population disponible en csv ici -> https://raw.githubusercontent.com/datasets/population/main/data/population.csv
3. Comment faire pour l'importer ?
4. Comment lister les pays ?
5. Comment faire pour tracer pour l'évolution de la population en France ? en Italie ? une petite fonction qui nous fait cela ?

#### Etape 5 : Pour aller plus loin
1. Comment faire pour avoir la dernière population par pays (indice, on va voir le cours sur 'groupby')
2. Comment on fait pour merger cela avec nos données précédentes ?
3. On agrège tout cela pour faire un graphe comparé du nombre de mort pour 100000 habitants en france et en italie (idéalement sur le même graphe).
