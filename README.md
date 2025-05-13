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
- **(Nouveau) Clustering basé sur le Knowledge_Score :**  
  À partir des réponses aux questions Q8 à Q14, on calcule un score composite (**Knowledge_Score**). Ce score, après standardisation, est soumis à l'algorithme **KMeans** (avec *k = 3*) afin de segmenter les patients en trois classes :
  - **Poor (faibles connaissances)**
  - **Moderate (connaissances modérées)**
  - **Good (bonnes connaissances)**
  
  L'objectif est d'obtenir une segmentation similaire à celle de l'article, où environ 7,8 % des patients présentent une bonne compréhension, 67,4 % une compréhension modérée, et environ 25 % des patients ont de faibles connaissances.
  
- (Optionnel) La réalisation d'un clustering global sur l'ensemble des variables (après encodage one-hot et standardisation) et une réduction de dimension par **PCA** pour la visualisation, ainsi que le profilage des clusters (exprimé par des moyennes pour des variables clés).

## Table des Matières

- [Installation](#installation)
- [Utilisation](#utilisation)
- [Structure du Projet](#structure-du-projet)
- [Classes Principales](#classes-principales)
- [Références](#références)

## Installation

### Prérequis

- Python 3.6 ou version supérieure
- Bibliothèques requises :
  - `pandas`
  - `seaborn`
  - `matplotlib`
  - `scikit-learn`

Pour installer les dépendances, utilisez la commande suivante :

```bash
pip install pandas seaborn matplotlib scikit-learn

Origine du Dataset

Le dataset est obtenu sur Mendeley Data via ce lien.

Téléversement du Dataset

Ce projet est conçu pour être exécuté dans Google Colab ou dans un environnement local. Le fichier Excel doit être téléversé lors de l'exécution du script.

Utilisation

Chargement et Nettoyage des DonnéesLa classe DataAnalyzer charge le fichier Excel et nettoie le dataset en remplissant les valeurs manquantes (médiane pour les variables numériques et mode pour les variables catégorielles).

Création de Colonnes CompositesAprès nettoyage, le programme calcule :

Le Knowledge_Score en sommant les réponses aux questions Q8 à Q14.

Le Age_Group par regroupement de la variable Age (par exemple : <=30, 31-40, 41-50 et >=51).

Analyse ExploratoireUn histogramme de la variable Age est généré pour examiner la distribution avant d'appliquer d'autres méthodes d'analyse.

Clustering Basé sur le Knowledge_ScoreLa nouvelle fonctionnalité de clustering extrait et standardise la variable Knowledge_Score puis applique l'algorithme KMeans en utilisant k = 3.Les clusters obtenus sont classés selon leurs centroïdes afin de leur attribuer les labels suivants :

Poor : Cluster avec le centroïde le plus faible.

Moderate : Cluster avec le centroïde intermédiaire.

Good : Cluster avec le centroïde le plus élevé.

Ce clustering segmentera idéalement les patients en trois groupes, par exemple environ 25 % de patients avec de faibles connaissances, 67,4 % avec des connaissances modérées, et 7,8 % affichant une bonne compréhension.

Visualisation des RésultatsLa classe Visualizer est utilisée pour générer :

Un histogramme de la variable Age.

Un histogramme du Knowledge_Score coloré en fonction des clusters (Knowledge_Cluster) afin d’illustrer la répartition des groupes.

Structure du Projet

├── Male Infertility Data.xlsx
├── README.md
└── programme_POO.ipynb

main.py : Contient l'ensemble du code source, incluant les classes DataAnalyzer, Visualizer, KnowledgeClustering et (optionnellement) FullDatasetClustering, ainsi que la fonction principale orchestrant le processus.

README.md : Ce document, qui présente le projet et ses fonctionnalités.

Male Infertility Data.xlsx: Le dataset utilisé qui doit être téléversé au démarrage.

Classes Principales

DataAnalyzer

load_data() :Lit le fichier Excel et charge les données dans un DataFrame.

clean_data() :Remplit les valeurs manquantes (médiane pour les numériques, mode pour les catégorielles).

descriptive_statistics() & missing_values_report() :Génèrent des statistiques descriptives et un rapport sur les valeurs manquantes.

compute_composite_columns() :Calcule le Knowledge_Score (somme des réponses aux questions Q8 à Q14) et crée la variable Age_Group.

Visualizer

plot_histogram() :Affiche un histogramme pour une variable numérique (ex. Age).

plot_knowledge_clusters() :Génère un histogramme du Knowledge_Score avec les barres colorées en fonction des clusters (Knowledge_Cluster).

KnowledgeClustering

run_clustering() :Extrait la variable Knowledge_Score, la standardise et applique l’algorithme KMeans (avec k = 3).Les clusters sont ensuite triés par ordre croissant de centroïdes et assignés aux labels "Poor", "Moderate" et "Good".

print_cluster_frequencies() :Affiche la répartition en pourcentage des trois clusters obtenus.

FullDatasetClustering (Optionnel)

preprocess() :Combine les variables numériques et les variables catégorielles après encodage one-hot.

run_clustering() :Standardise les données et applique l'algorithme KMeans.

visualize_clusters() :Réduit la dimension via PCA pour visualiser les clusters dans un scatter plot en 2D.

Profilage des clusters :Regroupe le DataFrame par cluster et calcule la moyenne de valeurs pour des variables clés (affichées via une heatmap).

Références

Article de Référence :Knowledge, Attitudes, Beliefs, and Practices Towards the Causes of Male Infertility Among Urology Outpatients in Abuja HospitalsTitilola T. Obilade, Peter O. Koleoso, Oluchi A. Eke, Faizat F. Adeniran, Nabila S. Musa, Sa'adah G. IbrahimDOI

Documentation :

Pandas

Scikit-learn

Seaborn

Matplotlib

Instructions pour l'Exécution

Cloner ou télécharger le dépôt GitHub.

Ouvrir le fichier main.py dans Google Colab ou un environnement de développement adapté.

Téléverser le fichier Male Infertility Data.xlsx lors de l'exécution du script.

Lancer le script. Le programme chargera et nettoiera les données, affichera un histogramme pour la variable Age, puis (optionnellement) exécutera le clustering sur le Knowledge_Score pour segmenter les patients en trois groupes ("Poor", "Moderate", "Good") et visualisera les résultats.

