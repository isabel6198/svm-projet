# Projet Ovarian Cancer Risk & Progression

## Contexte du projet

Ce projet vise à exploiter un ensemble de données cliniques, génétiques, démographiques et d’imagerie pour modéliser deux objectifs principaux :

1. **Classification du risque** d’ovarian cancer (aucun, faible, moyen, élevé)
2. **Prédiction de la probabilité de progression** de la maladie (valeur continue entre 0 et 1)

Les modèles envisagés incluent des classificateurs multiclasses (p. ex. SVM, Random Forest) et des régressions pour estimer la progression. L’accent est mis sur l’interprétabilité des modèles et la fiabilité des prédictions.

## Description du jeu de données  

Le dataset « Ovarian Cancer Risk and Progression Data » regroupe **200 100 observations horaires** collectées à Munich (Allemagne). Toutes les informations personnelles ont été supprimées pour garantir la confidentialité des patients. 
https://www.kaggle.com/datasets/datasetengineer/ovarian-cancer-risk-and-progression-data


### Caractéristiques disponibles

- **Cliniques** :  
  - Age (18–90 ans)  
  - BMI (15–50)  
  - Comorbidités (présence ou non)  
  - Symptômes (douleur abdominale, ballonnements)  
  - Taux de CA-125 (0–200)  
  - Stade du cancer (0–IV)  
  - Histopathologie (séreux, mucineux, clear cell)  
  - Traitements antérieurs (chimiothérapie, chirurgie, radiothérapie)  
  - Antécédents menstruels (régulier/irrégulier)

- **Démographiques** :  
  - Ethnie (Caucasien, Asiatique, Africain, Hispaniques)  
  - Habitudes (tabac, alcool)  
  - Type de résidence (urbain/rural)  
  - Statut socio-économique (bas, moyen, élevé)

- **Génétiques** :  
  - Mutations BRCA1/BRCA2 (oui/non)  
  - Expression génique normalisée  
  - Statut SNP  
  - Methylation de l’ADN & niveaux de miRNA

- **Imagerie** :  
  - Taille et localisation de la tumeur (ovaire, trompe, péritoine)  
  - Radiomics (texture, intensité, forme)  
  - Motifs de rehaussement  
  - Vitesse Doppler sanguine

- **Reproductives et hormonales** :  
  - Parité (0–3)   (nombre de grossesses ??)
  - Contraceptifs oraux & hormonothérapie (oui/non)  
  - Âge de ménarche & ménopause


  Timestamp contient l’horodatage de chaque enregistrement (chaque heure entre janvier 2019 et décembre 2024)

### Variables cibles

1. **Risk Label** : classification  (0 – Pas de risque, 1 – Faible risque, 2 – Risque moyen, 3 – Haut risque)  
2. **Progression Probability** : probabilité continue de progression (0.0–1.0)

## Organisation du dépôt

```
├── data/                       # Jeux de données bruts et prétraités
│   └── ovarian_cancer.csv      # Export du dataset principal
│
├── notebooks/                  # Cahiers Jupyter pour exploration et modélisation
│   ├── 01_exploration.ipynb    # Analyse descriptive et nettoyage
│   ├── 02_baseline_models.ipynb# Régressions et SVM de base
│   ├── 03_random_forest.ipynb  # Construction et tuning de Random Forest
│   └── 04_interpretation.ipynb # Explicabilité (SHAP, LIME, PDP…)
│
├── src/                        # Modules Python réutilisables
│   ├── data_loader.py          # Chargement et prétraitement des données
│   ├── models.py               # Définitions des modèles ML
│   └── explainability.py       # Fonctions pour PDP, ALE, SHAP, LIME
│
├── requirements.txt            # Dépendances Python
├── README.md                   # Présentation du projet
└── LICENSE                     # Licence du projet
```



## Utilisation

- **Exploration des données** :  Pour explorer les données et les comprendre `notebooks/01_exploration.ipynb`.  
- **Modèles de base** : Nous permet de tester plusieurs modeles  `notebooks/02_models.ipynb`.  
- **Optimisation** : configurer et optimiser dans `notebooks/03_optimisation.ipynb`.  
- **Explicabilité** : interpréter modèles et prédictions avec `notebooks/04_interpretation.ipynb`.

## Auteurs et contact

- **Équipe de projet**
Emma LABRE-BLANC
Isabel PALACIO


- Pour toute question : projet@ibe-munich.org

---

*Dernière mise à jour : avril 2025*

