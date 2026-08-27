# Projet de sélection — Exploration de données avec Python

## 1. Présentation du besoin

L'entreprise **Sell4All**, spécialisée dans la vente en ligne de vêtements d'occasion, souhaite intégrer une première fonctionnalité d'intelligence artificielle sur son site web afin de **recommander automatiquement des produits** à ses utilisateurs.

Les recommandations pourraient notamment être basées sur différentes informations concernant les clients, telles que :

* le pays ;
* l'âge ;
* le genre ;
* le montant dépensé ;
* et d'autres caractéristiques disponibles dans les données.

Avant de développer cette fonctionnalité, il est nécessaire d'**explorer, comprendre et nettoyer les données clients disponibles** afin de vérifier leur qualité, leur cohérence et leur adéquation avec un futur projet d'intelligence artificielle.

L'objectif de ce projet est donc de réaliser une première **exploration, analyse et préparation des données** à partir du fichier :

`dataset-sell4all.csv`

Le résultat final est un dataset nettoyé et structuré pouvant servir de base pour les prochaines étapes du projet.

---

# 2. Organisation du travail sur 3 jours

Le projet a été réalisé sur une durée de **3 jours**, avec une progression allant de la mise en place de l'environnement de travail jusqu'au nettoyage et à l'export des données finales.

---

## 📅 Jour 1 — Mise en place et exploration initiale

### Objectif

Le premier jour était consacré à la préparation de l'environnement de travail et à la compréhension de la structure initiale du dataset.

### 1. Mise en place de l'environnement de travail

Le projet a été réalisé avec **Anaconda Navigator** et **Jupyter Notebook**.

Les étapes réalisées sont :

* ouverture d'Anaconda Navigator ;
* lancement de Jupyter Notebook ;
* création d'un dossier dédié au projet `PROJET_SELL4ALL` ;
* ajout du fichier `dataset-sell4all.csv` dans ce dossier ;
* création du notebook `Exploration&Anayse_sell4all.ipynb`.

Les bibliothèques Python utilisées pour le projet sont principalement :

* **Pandas** : manipulation et analyse des données ;
* **Matplotlib** : création des visualisations.

### 2. Organisation des fichiers

Le dossier de travail a été organisé de la manière suivante :

```text
PROJET_SELL4ALL/
│
├── dataset-sell4all.csv
├── Exploration&Anayse_sell4all.ipynb
├── dataset-sell4all-clean.csv
└── README.md
```

Le fichier `dataset-sell4all-clean.csv` et le fichier `README.md` sont générés ou ajoutés au fur et à mesure de la réalisation du projet.

### 3. Chargement du dataset

Le fichier `dataset-sell4all.csv` a été chargé dans le notebook avec **Pandas**.

Une copie du dataset original a également été conservée afin de pouvoir travailler sur les données sans perdre les données sources.

### 4. Exploration initiale

Les principales fonctions Pandas ont été utilisées :

* `head()` pour afficher les 5 premières lignes ;
* `shape` pour connaître le nombre de lignes et de colonnes ;
* `describe()` pour obtenir un résumé statistique ;
* `info()` pour analyser la structure technique du dataset ;
* `dtypes` pour vérifier les types de données des colonnes.

### 5. Compréhension de `info()`

Une cellule Markdown explicative a été ajoutée au notebook pour expliquer :

* le nombre d'entrées ;
* le nombre de valeurs `non-null` ;
* les types de données ;
* le type `object` ;
* le type `int64`.

### 6. Vérification des valeurs manquantes

La présence de valeurs manquantes a été vérifiée avec :

```python
df.isna().sum()
```

Les types de données ont également été vérifiés avec :

```python
df.dtypes
```

### Résultat du Jour 1

À la fin du premier jour :

* l'environnement de travail était opérationnel ;
* le dataset était chargé ;
* la structure des données était comprise ;
* les types de données avaient été identifiés ;
* les valeurs manquantes avaient été vérifiées ;
* les premières incohérences avaient été repérées.

---

# 📅 Jour 2 — Transformation et analyse exploratoire

### Objectif

Le deuxième jour était consacré à la correction des formats, à l'harmonisation des données et à l'analyse exploratoire.

## 1. Conversion des dates

La colonne `Last date of connection` contenait plusieurs formats de dates.

Par exemple :

* `5-Apr-21`
* `oct. 10, 2021`

Afin d'obtenir un format de date adapté, la conversion a été réalisée avec :

```python
pd.to_datetime(..., format='mixed')
```

Cette transformation permet de gérer les différents formats présents dans la colonne.

## 2. Conversion de l'heure

La colonne `Last time of connection` était initialement enregistrée sous forme de texte.

Elle a été convertie avec :

```python
pd.to_datetime(..., format='%H:%M').dt.time
```

La colonne possède ainsi un format adapté à la représentation des heures.

## 3. Harmonisation de la colonne `Gender`

Une incohérence a été identifiée dans la colonne `Gender`.

Certaines valeurs étaient représentées par :

* `Women`
* `Woman`

Ces valeurs ont été harmonisées afin d'obtenir une représentation cohérente des catégories.

## 4. Analyse statistique de l'âge

Une analyse de la colonne `Age` a été réalisée.

Les statistiques suivantes ont été calculées :

* moyenne de l'âge ;
* médiane de l'âge.

Ces statistiques permettent d'obtenir une première vision de la répartition de l'âge des clients.

## 5. Analyse des dépenses

La colonne `Customer spendings` a également été analysée.

Les valeurs suivantes ont été calculées :

* moyenne des dépenses ;
* médiane des dépenses.

Cela permet de mieux comprendre le comportement d'achat des clients.

## 6. Analyse bonus par pays

Une analyse supplémentaire a été réalisée afin de calculer la **médiane de l'âge des clients pour chaque pays**.

Cette analyse utilise `groupby()` afin de comparer les différents pays.

## 7. Visualisation des dépenses

Un **diagramme à barres avec Matplotlib** a été réalisé afin de visualiser les dépenses des clients selon leur pays.

Cette représentation permet de faciliter la comparaison entre les différents pays.

### Résultat du Jour 2

À la fin du deuxième jour :

* les dates ont été converties ;
* les heures ont été converties ;
* la colonne `Gender` a été harmonisée ;
* les statistiques sur l'âge ont été calculées ;
* les statistiques sur les dépenses ont été calculées ;
* la médiane de l'âge par pays a été étudiée ;
* une visualisation des dépenses par pays a été réalisée.

---

# 📅 Jour 3 — Nettoyage final, validation et export

### Objectif

Le troisième jour était consacré au nettoyage final du dataset, à la sélection des colonnes utiles et à la création du fichier final.

## 1. Suppression des dépenses inférieures à 10 €

Les lignes correspondant aux clients ayant dépensé moins de **10 €** ont été supprimées.

La condition utilisée est :

```python
Customer spendings < 10
```

Cette étape permet de respecter le critère de nettoyage demandé dans le projet.

## 2. Suppression des doublons

Les doublons ont été recherchés puis supprimés avec :

```python
drop_duplicates()
```

Cela permet d'éviter d'avoir plusieurs fois les mêmes observations dans le dataset final.

## 3. Vérification après nettoyage

Après les opérations de nettoyage, le dataset a été vérifié afin de s'assurer que les transformations ont été correctement appliquées.

Les éléments suivants ont notamment été vérifiés :

* nombre de lignes restantes ;
* nombre de colonnes ;
* présence de doublons ;
* types des données ;
* valeurs manquantes ;
* cohérence générale des données.

## 4. Sélection des colonnes finales

Pour préparer le dataset à une future utilisation dans un système de recommandation, seules les colonnes demandées et utiles ont été conservées :

* `Country`
* `Age`
* `Gender`
* `Customer spendings`

## 5. Export du dataset nettoyé

Le dataset final a été exporté dans :

```text
dataset-sell4all-clean.csv
```

Ce fichier contient uniquement les colonnes sélectionnées après le nettoyage.

## 6. Vérification du résultat final

Une dernière vérification du fichier nettoyé a été réalisée afin de s'assurer que :

* les colonnes attendues sont présentes ;
* les doublons ont été supprimés ;
* les clients ayant des dépenses inférieures à 10 € ont été retirés ;
* les données sont correctement structurées.

### Résultat du Jour 3

À la fin du troisième jour :

* le nettoyage final a été réalisé ;
* les doublons ont été supprimés ;
* les dépenses inférieures à 10 € ont été filtrées ;
* les colonnes finales ont été sélectionnées ;
* le dataset final a été exporté ;
* le résultat a été vérifié.

---

# 3. Fonctionnalités développées / éléments finalisés

Le projet comprend les fonctionnalités suivantes.

## Exploration des données

* Chargement du fichier CSV avec Pandas.
* Affichage des 5 premières lignes avec `head()`.
* Analyse de la forme du dataset avec `shape`.
* Calcul des statistiques descriptives avec `describe()`.
* Analyse technique avec `info()`.
* Vérification des types avec `dtypes`.
* Vérification des valeurs manquantes avec `isna().sum()`.

## Transformation des données

* Conversion de `Last date of connection`.
* Conversion de `Last time of connection`.
* Harmonisation de `Gender`.

## Analyse exploratoire

* Calcul de la moyenne de `Age`.
* Calcul de la médiane de `Age`.
* Calcul de la moyenne de `Customer spendings`.
* Calcul de la médiane de `Customer spendings`.
* Calcul bonus de la médiane de l'âge par pays.
* Utilisation de `groupby()`.
* Création d'un diagramme à barres avec Matplotlib.

## Nettoyage des données

* Suppression des lignes avec `Customer spendings < 10`.
* Suppression des doublons avec `drop_duplicates()`.
* Vérification du dataset après nettoyage.

## Export

Les colonnes finales suivantes ont été conservées :

```text
Country
Age
Gender
Customer spendings
```

Le résultat a été enregistré dans :

```text
dataset-sell4all-clean.csv
```

---

# 4. Difficultés rencontrées et solutions mises en place

## 4.1. Formats de date hétérogènes

### Difficulté

La colonne `Last date of connection` contenait différents formats de dates, par exemple :

* `5-Apr-21`
* `oct. 10, 2021`

Une conversion classique pouvait donc générer des erreurs ou des valeurs incorrectes.

### Solution

La conversion a été réalisée avec :

```python
pd.to_datetime(..., format='mixed')
```

Cette solution permet de gérer les différents formats présents dans la colonne.

---

## 4.2. Colonne heure au format texte

### Difficulté

La colonne `Last time of connection` était enregistrée sous forme de texte.

### Solution

La colonne a été convertie avec :

```python
pd.to_datetime(..., format='%H:%M').dt.time
```

Cela permet d'obtenir un format horaire adapté.

---

## 4.3. Incohérence dans la colonne `Gender`

### Difficulté

La colonne `Gender` contenait différentes écritures pour une même catégorie :

* `Women`
* `Woman`

### Solution

Les valeurs ont été harmonisées afin d'avoir une représentation cohérente des catégories.

---

## 4.4. Compréhension du résumé technique `info()`

### Difficulté

Il était nécessaire de comprendre les informations retournées par `info()` avant de commencer les transformations.

### Solution

Une cellule Markdown explicative a été ajoutée dans le notebook afin d'expliquer :

* le nombre d'entrées ;
* `non-null` ;
* les types `object` ;
* les types `int64` ;
* le nombre de colonnes.

---

## 4.5. Organisation du travail avec Anaconda Navigator

### Difficulté

Il était nécessaire de disposer d'un environnement simple permettant de travailler avec Python, Jupyter Notebook et les bibliothèques nécessaires.

### Solution

**Anaconda Navigator** a été utilisé comme outil de gestion et de lancement de l'environnement de travail.

Jupyter Notebook a ensuite été utilisé pour développer et exécuter le projet.

---

# 5. Mode d'exécution du projet

## 5.1. Prérequis

Pour exécuter ce projet, il faut disposer de :

* **Anaconda**
* **Anaconda Navigator**
* **Python**
* **Jupyter Notebook**
* **Pandas**
* **Matplotlib**

---

# 6. Installation et préparation

## Étape 1 — Installer Anaconda

Installer **Anaconda** sur l'ordinateur.

Anaconda permet notamment d'utiliser Anaconda Navigator ainsi que les outils nécessaires pour travailler avec Python.

## Étape 2 — Ouvrir Anaconda Navigator

Lancer :

**Anaconda Navigator**

## Étape 3 — Lancer Jupyter Notebook

Depuis Anaconda Navigator, lancer :

**Jupyter Notebook**

## Étape 4 — Créer le dossier du projet

Créer un dossier nommé par exemple :

```text
PROJET_SELL4ALL
```

## Étape 5 — Ajouter le fichier CSV

Placer le fichier :

```text
dataset-sell4all.csv
```

dans le dossier `PROJET_SELL4ALL`.

## Étape 6 — Créer le notebook

Dans Jupyter Notebook :

**New → Python 3 (ipykernel)**

Puis renommer le notebook :

```text
Exploration&Anayse_sell4all.ipynb
```

## Étape 7 — Installer les bibliothèques si nécessaire

Les bibliothèques utilisées sont :

```text
pandas
matplotlib
```

Elles peuvent être installées depuis l'environnement Python utilisé par Jupyter si elles ne sont pas déjà disponibles.

---

# 7. Lancement du projet

Pour exécuter le projet :

### Étape 1

Ouvrir **Anaconda Navigator**.

### Étape 2

Lancer **Jupyter Notebook**.

### Étape 3

Accéder au dossier :

```text
PROJET_SELL4ALL
```

### Étape 4

Vérifier que le fichier suivant est présent :

```text
dataset-sell4all.csv
```

### Étape 5

Ouvrir :

```text
Exploration&Anayse_sell4all.ipynb
```

### Étape 6

Exécuter les cellules du notebook dans l'ordre.

Il est également possible d'utiliser :

**Cell → Run All**

### Étape 7

Après l'exécution complète du notebook, le fichier nettoyé sera généré :

```text
dataset-sell4all-clean.csv
```

---

# 8. Structure du projet

Le dépôt final contient les fichiers suivants :

```text
PROJET_SELL4ALL/
│
├── Exploration&Anayse_sell4all.ipynb
├── dataset-sell4all.csv
├── dataset-sell4all-clean.csv
└── README.md
```

## Description des fichiers

### `Exploration&Anayse_sell4all.ipynb`

Notebook Jupyter contenant :

* le chargement des données ;
* l'exploration initiale ;
* les explications ;
* les transformations ;
* l'analyse statistique ;
* les visualisations ;
* le nettoyage ;
* l'export du dataset ;
* la conclusion.

### `dataset-sell4all.csv`

Fichier contenant le dataset original fourni pour le projet.

### `dataset-sell4all-clean.csv`

Fichier contenant le dataset nettoyé avec uniquement les colonnes :

* `Country`
* `Age`
* `Gender`
* `Customer spendings`

### `README.md`

Documentation du projet contenant :

* la présentation du besoin ;
* l'organisation du travail sur 3 jours ;
* les étapes réalisées ;
* les fonctionnalités développées ;
* les difficultés et leurs solutions ;
* les prérequis ;
* le mode d'exécution ;
* la structure du dépôt ;
* la conclusion.

---
# 9. Conclusion

Ce projet a permis de réaliser une première étape de **préparation et d'exploration des données** pour l'entreprise Sell4All.Ce travail constitue donc une première étape essentielle avant la mise en place d'un modèle d'intelligence artificielle.
