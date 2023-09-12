# TD : Analyse de données avec Python et Pandas

## Objectif

Dans ce TD, nous allons utiliser Python et la bibliothèque Pandas pour analyser les données recueillies à partir d'un formulaire Google. Vous allez apprendre à charger, nettoyer et analyser des données pour en extraire des informations pertinentes.

## Données

Les données proviennent d'un formulaire Google que vous avez rempli. Les résultats sont disponibles [ici](https://docs.google.com/spreadsheets/d/1Mr-gVp_I2VZCVHyb8Oo7U4dr4o9zMCLXOXrnPrTgeTg/edit?resourcekey#gid=810928449).

## Étapes

0. **Setup** : Installation
1. **Récupération des données** : Importez les données du Google Sheet dans un notebook Jupyter.
2. **Nettoyage des données** : Assurez-vous que les données sont propres et prêtes à être analysées.
3. **Analyse des données** : Répondez aux questions posées ci-dessous en utilisant Pandas.

---

### 0. Setup

Dans un nouveau repertoire (ou le repertoire du cours), on install conda avec un nouvelle environnement.

```bash
$ conda create --name num
$ conda activate num
```

On peut alors lancer un notebook.

### 1. Récupération des données

Pour récupérer les données depuis Google Sheets, vous pouvez exporter le fichier en format CSV et le charger dans Jupyter. Une autre méthode consiste à utiliser la bibliothèque `gspread` pour importer directement les données dans Jupyter.

#### Méthode avec CSV :

D'accord, si les données sont accessibles publiquement, nous pouvons utiliser `pandas` pour lire directement le fichier CSV depuis l'URL.

```python
import pandas as pd

url = "https://docs.google.com/spreadsheets/d/1Mr-gVp_I2VZCVHyb8Oo7U4dr4o9zMCLXOXrnPrTgeTg/export?format=csv&gid=810928449"
data = pd.read_csv(url)
```

### 2. Nettoyage des données

Avant de commencer l'analyse, il est essentiel de vérifier la propreté des données.

```python
# Afficher les premières lignes du dataframe
data.head()

# Vérifier s'il y a des valeurs manquantes
data.isnull().sum()

# Si nécessaire, remplacez les valeurs manquantes ou supprimez les lignes/colonnes concernées
```

### 3. Analyse des données

**Questions :**

1. Combien d'étudiants ont répondu au formulaire ?
```python
nb_students = data.shape[0]
print(f"{nb_students} étudiants ont répondu au formulaire.")
```

2. Quelle est la moyenne d'âge des étudiants ?
```python
# Convertir la colonne "Ma date de naissance (jj/mm/aaaa)" en type datetime
data['Date de naissance'] = pd.to_datetime(data['Ma date de naissance (jj/mm/aaaa)'], format='%d/%m/%Y')
data['Age'] = (pd.Timestamp.now() - data['Date de naissance']).astype('<m8[Y]')
mean_age = data['Age'].mean()
print(f"L'âge moyen des étudiants est de {mean_age:.2f} ans.")
```

3. Quelle est la distribution des niveaux de connaissance en Python ?
```python
distribution = data['Votre niveau en programmation/Python'].value_counts()
print(distribution)
```

4. Quelle est la taille moyenne et le poids moyen des étudiants ?
```python
mean_height = data['Je mesure (en cm)'].mean()
mean_weight = data['Mon poids (en kg)'].mean()
print(f"La taille moyenne des étudiants est de {mean_height:.2f} cm et le poids moyen est de {mean_weight:.2f} kg.")
```

5. Combien d'étudiants pensent utiliser la programmation dans leur vie professionnelle future ?
```python
future_use = data[data['Selon vous, dans votre vie professionnelle future, vous utiliserez la programmation ?'] == 'Oui'].shape[0]
print(f"{future_use} étudiants pensent utiliser la programmation dans leur vie professionnelle future.")
```

---

**Exercices supplémentaires :**

- Analysez la distribution des matières préférées.
- Découvrez les sujets d'analyse de données les plus populaires suggérés par les étudiants.
- Visualisez la distribution des âges à l'aide d'un histogramme.

---

N'oubliez pas d'encourager les étudiants à explorer davantage les données par eux-mêmes et à poser leurs propres questions pour l'analyse.