# Projet_Sell4All_Exploration
Exploration et nettoyage des données clients de Sell4All avec Python, et l'utilisation des biblio Pandas et Matplotlib.

## 1. Présentation du besoins

L'entreprise **Sell4All**, spécialisée dans la vente en ligne de vêtements d'occasion, souhaite intégrer une première fonctionnalité d'intelligence artificielle sur son site web afin de **recommander automatiquement des produits** à ses utilisateurs (selon le pays, l'âge, le genre, le montant dépensé, etc.).

Avant de développer cette fonctionnalité, il est nécessaire d'**explorer, comprendre et nettoyer** les données clients disponibles (`dataset-sell4all.csv`) afin de vérifier leur qualité et leur adéquation avec un futur projet d'IA.

Ce dépôt contient le notebook Jupyter réalisant cette première exploration ainsi que le fichier de données nettoyées.

## 2. Étapes suivies

1. Installation de l'environnement (Miniconda, Jupyter Notebook, bibliothèques `pandas` et `matplotlib`).
2. Chargement du fichier `dataset-sell4all.csv` avec `pandas` et sauvegarde d'une copie du dataset d'origine.
3. Exploration initiale : affichage des 5 premières lignes (`head()`), de la forme du dataset (`shape`), du résumé statistique (`describe()`) et du résumé technique (`info()`).
4. Explication du résumé technique (nombre d'entrées, signification de "non-null", types de données) dans une cellule Markdown.
5. Vérification des valeurs manquantes (`isna().sum()`) et des types de colonnes (`dtypes`).
6. Nettoyage / mise en forme de certaines colonnes :
   - conversion de `Last time of connection` et `Last date of connection` en types datetime ;
   - harmonisation de la colonne `Gender` (valeurs `Women`/`Woman`).
7. Analyse exploratoire (EDA) :
   - calcul de la médiane et de la moyenne des colonnes `Age` et `Customer spendings` ;
   - question bonus : médiane de l'âge par pays (`groupby`) ;
   - visualisation en diagramme à barres des dépenses médianes des clients par pays.
8. Nettoyage des données :
   - suppression des lignes avec moins de 10 € de dépenses (`Customer spendings < 10`) ;
   - suppression des doublons (`drop_duplicates`).
9. Sélection des colonnes finales (`Country`, `Age`, `Gender`, `Customer spendings`) et export du résultat dans `dataset-sell4all-clean.csv`.
10. Rédaction d'une conclusion finale résumant la qualité du dataset et son adéquation pour la suite du projet.

## 3. Fonctionnalités développées / éléments finalisés

- Chargement et inspection du dataset (`head`, `shape`, `describe`, `info`, `dtypes`).
- Explication pédagogique du résumé technique (`info()`) dans une cellule Markdown.
- Calcul de statistiques descriptives (médiane, moyenne) sur `Age` et `Customer spendings`.
- Calcul bonus de la médiane d'âge par pays.
- Visualisation des dépenses clients par pays sous forme de diagramme à barres (`matplotlib`).
- Nettoyage des données : suppression des dépenses < 10 €, suppression des doublons, harmonisation de la colonne `Gender`.
- Export du dataset nettoyé (`dataset-sell4all-clean.csv`) contenant uniquement les colonnes `Country`, `Age`, `Gender`, `Customer spendings`.

## 4. Difficultés rencontrées et solutions mises en place

- **Formats de date hétérogènes** dans la colonne `Last date of connection` (ex. `5-Apr-21` et `oct. 10, 2021`) : résolu en utilisant `pd.to_datetime(..., format='mixed')`.
- **Colonne heure au format texte** (`Last time of connection`) : convertie via `pd.to_datetime(..., format='%H:%M').dt.time`.
- **Incohérence dans la colonne `Gender`** (mélange singulier/pluriel `Women`/`Woman`) : harmonisée par remplacement des valeurs.
- **Compréhension du résumé technique `info()`** : clarifiée dans une cellule Markdown dédiée (nombre d'entrées, signification de "non-null", types de données `object`/`int64`).

## 5. Mode d'exécution du projet

### Prérequis

- Python installé via [Miniconda](https://docs.conda.io/en/latest/miniconda.html)
- Jupyter Notebook
- Bibliothèques Python : `pandas`, `matplotlib`

### Installation

```bash
conda create -n sell4all python=3.13   #Crée un nouvel environnement virtuel Conda nommé sell4all, isolé du reste du système, avec la        version  3.13 de Python installée dedans. Cela évite les conflits avec d'autres projets Python.
conda activate sell4all  #Active (bascule vers) l'environnement sell4all qu'on vient de créer. Une fois activé, toutes les commandes conda install ou python suivantes s'exécutent à l'intérieur de cet environnement isolé (son nom apparaît généralement entre parenthèses dans le terminal, ex: (sell4all)).
conda install pandas matplotlib jupyter #Installe dans l'environnement actif (sell4all) les trois bibliothèques/outils nécessaires au projet :

         # pandas : pour lire et manipuler les données du CSV ;
         # matplotlib : pour créer le diagramme à barres ;
         # jupyter : pour lancer et utiliser Jupyter Notebook.
```

### Lancement

1. Cloner le dépôt :
   ```bash
   git clone <lien-du-depot>
   cd <nom-du-dossier>
   ```
2. S'assurer que le fichier `dataset-sell4all.csv` se trouve dans le même dossier que le notebook.
3. Lancer Jupyter Notebook :
   ```bash
   jupyter notebook
   ```
4. Ouvrir le fichier `Exploration_Anayse_sell4all.ipynb` et exécuter les cellules dans l'ordre (menu **Cell > Run All**).
5. Le fichier nettoyé `dataset-sell4all-clean.csv` sera généré automatiquement dans le même dossier.

## 6. Contenu du dépôt

- `Exploration_Anayse_sell4all.ipynb` : notebook contenant le code, les résultats et les explications.
- `dataset-sell4all-clean.csv` : fichier CSV nettoyé (colonnes `Country`, `Age`, `Gender`, `Customer spendings`).
- `README.md` : ce fichier globalement tous les etapes realiser dans l'exploration de cette ensemble de données.
