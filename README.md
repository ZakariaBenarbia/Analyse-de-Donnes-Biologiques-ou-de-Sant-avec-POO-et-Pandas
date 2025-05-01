# TP-Programmation-Orient-e-Objet
# Analyse de Données Biologiques ou de Santé avec POO et Pandas

## Description

Ce projet analyse un jeu de données de santé portant sur l'infertilité masculine en utilisant les principes de la Programmation Orientée Objet (POO) et la bibliothèque **Pandas**. Le jeu de données (par exemple, *Male Infertility Data.xlsx*) contient de multiples variables couvrant des aspects démographiques, biologiques et comportementaux de l'infertilité masculine. Le projet s'inspire de l'article :

> **Knowledge, Attitudes, Beliefs, and Practices Towards the Causes of Male Infertility Among Urology Outpatients in Abuja Hospitals**  
> Titilola T. Obilade, Peter O. Koleoso, Oluchi A. Eke, Faizat F. Adeniran, Nabila S. Musa, Sa'adah G. Ibrahim  
> [DOI](https://doi.org/10.21203/rs.3.rs-5902036/v1)

Les objectifs comprennent :

- Le chargement et le nettoyage d'un fichier Excel à l'aide de Pandas.
- L'exploration initiale des données par le calcul de statistiques descriptives et la génération d'un histogramme pour la variable `Age`.
- La structure du code en utilisant des classes pour organiser l'analyse (classe `DataAnalyzer`) et la visualisation (classe `Visualizer`).
- (Optionnel) La réalisation d'un clustering sur l'ensemble des variables (après encodage one-hot et standardisation) à l'aide de l'algorithme **KMeans** et une visualisation par réduction de dimension avec **PCA**.
- (Optionnel) Le profilage des clusters par le calcul des moyennes pour un ensemble de variables clés.

## Table des Matières

- [Installation](#installation)
- [Utilisation](#utilisation)
- [Structure du Projet](#structure-du-projet)
- [Classes Principales](#classes-principales)
- [Références](#références)


## Installation

### Prérequis

- Python 3.6 ou version supérieure.
- Bibliothèques requises :  
  - `pandas`  
  - `seaborn`  
  - `matplotlib`  
  - `scikit-learn`

Installation des dépendances avec la commande suivante :

```bash
pip install pandas seaborn matplotlib scikit-learn
```

### Téléversement du Jeu de Données

Le projet est conçu pour être exécuté dans [Google Colab](https://colab.research.google.com/) ou dans un environnement local. Le fichier Excel (par exemple, `Male Infertility Data.xlsx`) sera téléversé lors de l'exécution du script.

## Utilisation

1. **Chargement et Nettoyage des Données :**  
   La classe `DataAnalyzer` charge le fichier Excel et nettoie les données en remplissant les valeurs manquantes (médiane pour les variables numériques et mode pour les variables catégorielles).

2. **Analyse Exploratoire :**  
   Un histogramme de la variable `Age` est généré avant le clustering afin d'examiner la distribution.

3. **(Optionnel) Clustering :**  
   La classe `FullDatasetClustering` convertit l'ensemble des variables en données numériques (après encodage one-hot pour les variables catégorielles), standardise le jeu de données et applique l'algorithme **KMeans** (3 clusters par défaut). La réduction de dimension par **PCA** permet de visualiser les clusters en 2D.

4. **(Optionnel) Profilage des Clusters :**  
   Une fonction regroupe le DataFrame original par cluster et calcule la moyenne de valeurs pour des variables clés, avec une heatmap affichant le profil de chaque cluster.

## Structure du Projet

```
├── main.py
├── README.md
└── Male Infertility Data.xlsx   (à téléverser lors de l'exécution)
```

- **main.py :** Regroupe l'ensemble du code source, incluant les classes `DataAnalyzer`, `Visualizer` et (optionnellement) `FullDatasetClustering`, ainsi que la fonction principale orchestrant le processus.
- **README.md :** Ce document.
- **Male Infertility Data.xlsx :** Jeu de données devant être téléversé lors de l'exécution.

## Classes Principales

### DataAnalyzer

- **load_data() :** Charge le jeu de données depuis un fichier Excel.
- **clean_data() :** Remplit les valeurs manquantes (médiane pour les numériques, mode pour les catégorielles).
- **descriptive_statistics() et missing_values_report() :** Fournissent une analyse exploratoire préliminaire.
- **filter_data() :** Permet le filtrage du DataFrame selon une condition donnée.

### Visualizer

- **plot_histogram() :** Affiche un histogramme pour une variable numérique (ex. `Age`).
- **plot_clusters() :** Génère un scatter plot des clusters après réduction avec PCA.

### FullDatasetClustering (Optionnel)

- **preprocess() :** Combine les données numériques et les variables catégorielles après encodage one-hot.
- **run_clustering() :** Applique la standardisation et exécute l'algorithme **KMeans**.
- **visualize_clusters() :** Réduit les dimensions avec **PCA** et retourne les résultats pour la visualisation des clusters.

## Références

1. **Article de Référence :**  
   *Knowledge, Attitudes, Beliefs, and Practices Towards the Causes of Male Infertility Among Urology Outpatients in Abuja Hospitals*  
   Titilola T. Obilade, Peter O. Koleoso, Oluchi A. Eke, Faizat F. Adeniran, Nabila S. Musa, Sa'adah G. Ibrahim  
   [DOI](https://doi.org/10.21203/rs.3.rs-5902036/v1)

2. **Documentation :**  
   - [Documentation de Pandas](https://pandas.pydata.org/docs/)  
   - [Documentation de Scikit-learn](https://scikit-learn.org/stable/documentation.html)  
   - [Documentation de Seaborn](https://seaborn.pydata.org/)  
   - [Documentation de Matplotlib](https://matplotlib.org/stable/contents.html)


## Instructions pour l'Exécution

1. Cloner ou télécharger le dépôt GitHub.
2. Ouvrir le fichier `main.py` dans Google Colab ou l'environnement de développement préféré.
3. Téléverser le fichier `Male Infertility Data.xlsx` lorsque l'exécution le demande.
4. Lancer le script. Le programme chargera et nettoiera les données, affichera un histogramme de la variable `Age`, puis (optionnellement) exécutera le clustering et la visualisation par PCA.

---
```

