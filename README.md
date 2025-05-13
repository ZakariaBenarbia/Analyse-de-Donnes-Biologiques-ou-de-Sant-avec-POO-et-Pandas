Voici la version mise à jour du fichier README.md, incluant des explications détaillées sur le diagramme de score (c’est-à-dire la manière dont le **Knowledge_Score** est calculé et utilisé pour assigner des groupes de connaissances) ainsi qu'une explication sur la nature optionnelle de la classe **FullDatasetClustering**.

---

```markdown
# TP-Programmation-Orient-e-Objet

# Analyse de Données Biologiques ou de Santé avec POO et Pandas

## Description

Ce projet analyse un dataset de santé portant sur l'infertilité masculine en appliquant les principes de la Programmation Orientée Objet (POO) et la bibliothèque **Pandas**. Le dataset (*Male Infertility Data.xlsx*) comporte de nombreuses variables couvrant des aspects démographiques, biologiques et comportementaux de l'infertilité masculine. Le dataset provient de Mendeley Data et est accessible via le lien suivant : [https://data.mendeley.com/datasets/fyk47fnhfs/1](https://data.mendeley.com/datasets/fyk47fnhfs/1).

Ce projet s'inspire de l'article suivant :

> **Knowledge, Attitudes, Beliefs, and Practices Towards the Causes of Male Infertility Among Urology Outpatients in Abuja Hospitals**  
> Titilola T. Obilade, Peter O. Koleoso, Oluchi A. Eke, Faizat F. Adeniran, Nabila S. Musa, Sa'adah G. Ibrahim  
> [DOI](https://doi.org/10.21203/rs.3.rs-5902036/v1)

Les objectifs incluent :

- Charger et nettoyer un dataset Excel à l'aide de **Pandas**.
- Explorer les données via des statistiques descriptives et la génération d'un histogramme pour la variable `Age`.
- Organiser le code en adoptant les principes de la Programmation Orientée Objet à travers l'utilisation de classes :
  - La classe `DataAnalyzer` gère le chargement, le nettoyage et la création de colonnes composites (notamment le **Knowledge_Score** et le **Age_Group**).
  - La classe `Visualizer` permet de visualiser les données (histogrammes, visualisation des clusters, etc.).
- **(Nouveau) Clustering basé sur le Knowledge_Score et diagramme de score :**  
  À partir des réponses aux questions Q8 à Q14, on calcule un score composite appelé **Knowledge_Score**. Ce score représente la compréhension du patient des causes de l’infertilité masculine.  
  **Diagramme de score** : Le score est obtenu en faisant la somme des réponses (supposées binaires ou codées numériquement) aux questions Q8 à Q14. Ce Knowledge_Score sert ensuite d'entrée pour l'algorithme de clustering KMeans, qui subdivise les patients en trois groupes distincts.  
  Les clusters obtenus sont triés selon leurs centroïdes, permettant ainsi d'attribuer les labels suivants :
  - **Poor (faibles connaissances)** : Cluster avec le centroïde le plus faible.
  - **Moderate (connaissances modérées)** : Cluster avec le centroïde intermédiaire.
  - **Good (bonnes connaissances)** : Cluster avec le centroïde le plus élevé.  
  L'objectif est d'obtenir une répartition proche de celle rapportée dans l'article (environ 7,8 % Good, 67,4 % Moderate et 25 % Poor).

- (Optionnel) La réalisation d'un clustering global sur l'ensemble des variables (après encodage one-hot et standardisation) ainsi que la réduction de dimension par **PCA** pour la visualisation, avec un profilage des clusters (exprimé par des moyennes pour des variables clés).

> **Pourquoi la classe FullDatasetClustering est-elle optionnelle ?**  
> La classe **FullDatasetClustering** représente une analyse complémentaire qui va au-delà de l'objectif principal du projet. Le cœur de l'analyse se concentre sur le **Knowledge_Score** pour segmenter les patients en trois groupes (Poor, Moderate, Good). L'utilisation de **FullDatasetClustering**, qui réalise un clustering sur l'ensemble des variables du dataset (numériques et encodées), permet d'explorer d'autres patterns et de réaliser une analyse plus globale. Toutefois, cette étape complexifie le pipeline en ajoutant des étapes d’encodage, de standardisation et de réduction dimensionnelle. Ainsi, elle est proposée en option aux utilisateurs souhaitant approfondir l'analyse du dataset dans son ensemble, sans être indispensable pour atteindre l'objectif principal.

## Table des Matières

- [Installation](#installation)
- [Utilisation](#utilisation)
- [Structure du Projet](#structure-du-projet)
- [Classes Principales](#classes-principales)
- [Diagramme de Score et Explications](#diagramme-de-score-et-explications)
- [Références](#références)

## Installation

### Prérequis

- Python 3.6 ou version supérieure.
- Bibliothèques requises :
  - `pandas`
  - `seaborn`
  - `matplotlib`
  - `scikit-learn`

Installation des dépendances avec la commande suivante :

```bash
pip install pandas seaborn matplotlib scikit-learn
```

### Origine du Dataset

Dataset obtenu sur Mendeley Data via [ce lien](https://data.mendeley.com/datasets/fyk47fnhfs/1).

### Téléversement du Dataset

Le projet est conçu pour une exécution dans [Google Colab](https://colab.research.google.com/) ou dans un environnement local. Le fichier Excel devra être téléversé lors de l'exécution du script.

## Utilisation

1. **Chargement et Nettoyage des Données**  
   La classe `DataAnalyzer` charge le fichier Excel et nettoie le dataset en remplissant les valeurs manquantes (médiane pour les variables numériques et mode pour les variables catégorielles).

2. **Création de Colonnes Composites**  
   Après nettoyage, le programme calcule :
   - Le **Knowledge_Score** en sommant les réponses aux questions Q8 à Q14.
   - Le **Age_Group** par regroupement de la variable `Age` (exemples : `<=30`, `31-40`, `41-50`, `>=51`).

3. **Analyse Exploratoire**  
   Un histogramme de la variable `Age` est généré afin d'examiner la distribution avant l'application d'autres méthodes d'analyse.

4. **Clustering Basé sur le Knowledge_Score**  
   La nouvelle fonctionnalité de clustering extrait et standardise la variable **Knowledge_Score** puis applique l'algorithme **KMeans** en utilisant **k = 3**.  
   Les clusters obtenus sont triés par ordre croissant de centroïdes pour leur assigner les labels suivants :  
   - **Poor** : Cluster avec le centroïde le plus faible.
   - **Moderate** : Cluster avec le centroïde intermédiaire.
   - **Good** : Cluster avec le centroïde le plus élevé.

   Ce clustering segmentera les patients en trois groupes, visant idéalement une répartition d'environ 25 % avec de faibles connaissances, 67,4 % avec des connaissances modérées, et 7,8 % avec de bonnes connaissances.

5. **Visualisation des Résultats**  
   La classe `Visualizer` génère :
   - Un histogramme pour la variable `Age`.
   - Un histogramme du **Knowledge_Score** dont les barres sont colorées en fonction des clusters (Knowledge_Cluster).

6. **(Optionnel) Clustering Global sur L'ensemble des Variables**  
   La classe **FullDatasetClustering** permet d'effectuer une analyse globale en combinant l'encodage one-hot de variables catégorielles, la standardisation et l'application de **KMeans** sur l'ensemble du dataset.  
   *Cette étape est optionnelle* car elle offre une analyse complémentaire et approfondie qui n'est pas indispensable pour segmenter les patients selon la compréhension des causes de l'infertilité masculine (objectif principal du projet).

## Structure du Projet

```
├── Male Infertility Data.xlsx
├── README.md
└── programme_POO.ipynb
```

- **main.py :** Contient l'ensemble du code source, incluant les classes `DataAnalyzer`, `Visualizer`, `KnowledgeClustering` et (optionnellement) `FullDatasetClustering`, ainsi que la fonction principale orchestrant le processus.
- **README.md :** Ce document.
- **Male Infertility Data.xlsx:** Le dataset qui doit être téléversé lors de l'exécution.

## Classes Principales

### DataAnalyzer
- **load_data() :**  
  Charge le fichier Excel et crée un DataFrame.
- **clean_data() :**  
  Remplit les valeurs manquantes (médiane pour les numériques, mode pour les catégorielles).
- **descriptive_statistics() & missing_values_report() :**  
  Fournissent des statistiques descriptives et un rapport sur les valeurs manquantes.
- **compute_composite_columns() :**  
  Calcule le **Knowledge_Score** (somme des réponses aux questions Q8 à Q14) et crée la variable **Age_Group**.

### Visualizer
- **plot_histogram() :**  
  Affiche un histogramme pour une variable numérique (ex. `Age`).
- **plot_knowledge_clusters() :**  
  Génère un histogramme du **Knowledge_Score** dont les barres sont colorées en fonction des clusters (Knowledge_Cluster).

### KnowledgeClustering
- **run_clustering() :**  
  Extrait la variable **Knowledge_Score**, la standardise et applique l'algorithme **KMeans** (avec *k = 3*).
  Les clusters sont triés par ordre croissant de centroïdes et assignés aux labels "Poor", "Moderate" et "Good".
- **print_cluster_frequencies() :**  
  Affiche la répartition en pourcentage des clusters obtenus.

### FullDatasetClustering (Optionnel)
- **preprocess() :**  
  Combine les variables numériques et les variables catégorielles après encodage one-hot.
- **run_clustering(n_clusters: int) :**  
  Standardise les données et applique l'algorithme **KMeans**.
- **visualize_clusters(n_components: int) :**  
  Réduit la dimension via **PCA** pour visualiser les clusters dans un scatter plot en 2D.
- **Pourquoi est-ce optionnel ?**  
  Cette classe offre une analyse complémentaire du dataset global, permettant de segmenter les données sur l'ensemble des variables. Toutefois, le focus principal du projet étant la compréhension du **Knowledge_Score** et son utilisation pour la segmentation (en Poor, Moderate, Good), cette analyse globale n'est pas indispensable. Elle est donc présentée en option pour ceux qui souhaitent explorer davantage le dataset.

## Références

1. **Article de Référence :**  
   *Knowledge, Attitudes, Beliefs, and Practices Towards the Causes of Male Infertility Among Urology Outpatients in Abuja Hospitals*  
   Titilola T. Obilade, Peter O. Koleoso, Oluchi A. Eke, Faizat F. Adeniran, Nabila S. Musa, Sa'adah G. Ibrahim  
   [DOI](https://doi.org/10.21203/rs.3.rs-5902036/v1)

2. **Documentation :**  
   - [Pandas](https://pandas.pydata.org/docs/)  
   - [Scikit-learn](https://scikit-learn.org/stable/documentation.html)  
   - [Seaborn](https://seaborn.pydata.org/)  
   - [Matplotlib](https://matplotlib.org/stable/contents.html)

## Instructions pour l'Exécution

1. Cloner ou télécharger le dépôt GitHub.
2. Ouvrir le fichier `main.py` dans Google Colab ou dans un environnement de développement adapté.
3. Téléverser le fichier `Male Infertility Data.xlsx` lors de l'exécution du script.
4. Lancer le script. Le programme chargera et nettoiera les données, affichera un histogramme pour la variable `Age`, puis (optionnellement) exécutera le clustering sur le **Knowledge_Score** pour segmenter les patients en trois groupes ("Poor", "Moderate", "Good") et visualisera les résultats.
