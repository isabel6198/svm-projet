# Projet : Prédiction du isque et de la progression du cancer des ovaires

## Objectif
Ce projet vise à appliquer des méthodes de machine learning sur un dataset médical afin de prédire :

- **Une classification du risque de cancer des ovaires** 
- **Une probabilité de progression** (régression sur [0, 1])

Nous utilisons un dataset synthétique complet (200 000+ observations horaires) contenant des variables cliniques, d'imagerie, génétiques et démographiques.

---

## Pourquoi modéliser deux cibles ?
Le dataset inclut deux informations essentielles mais distinctes :

| Variable cible | Type de problème  | Description |
|----------------|--------------------|-------------|
| `RiskLabel`    | Classification     | Niveau de risque (aucun, faible, moyen, élevé) |
| `ProgressionProbability` | Régression | Probabilité continue de progression de la maladie |

En modélisant **les deux**, on peut :
- Comparer les performances sur différents types de modèles (SVM, linéaire, forêts)
- Explorer des différences ou similarités dans les variables explicatives
- Appliquer différentes approches d'interprétation globale et locale (SHAP, LIME, PDP, etc.)

---

### Présentation des variables

- **Timestamp** : Date et heure d’enregistrement de l’observation
- **Age** : Âge du patient au moment du diagnostic  
- **BMI** : Indice de masse corporelle du patient  
- **Comorbidity** : Présence d’une ou plusieurs comorbidités associées  
- **Symptom** : Présence de symptômes typiques (ex. douleurs abdominales, ballonnements) 
- **CA125** : Dosage du marqueur tumoral CA-125, souvent utilisé pour détecter le cancer des ovaires 
- **CancerStage** : Stade clinique du cancer (de 0 à IV)  
- **Histopathology** : Sous-type histologique du cancer (séreux, mucineux, clear cell) 
- **PreviousTreatment** : Indique si un traitement antérieur (chimio, radio, chirurgie) a été effectué 
- **MenstrualHistory** : Régularité des cycles menstruels (régulier/irrégulier)  
- **Ethnicity** : Origine ethnique du patient  
- **Smoking** : Indique si le patient fume
- **Alcohol** : Indique si le patient consomme de l’alcool
- **Residence** : Type de lieu de résidence (urbain ou rural)  
- **SocioeconomicStatus** : Niveau socio-économique (bas, moyen, élevé)  
- **BRCA_Mutation** : Présence d’une mutation BRCA1 ou BRCA2
- **GeneExpression** : Valeur normalisée de l’expression génique 
- **SNP_Status** : Présence de polymorphismes nucléotidiques simples (SNP)  
- **DNAMethylation** : Niveau de méthylation de l’ADN  
- **miRNA** : Expression des microARN  
- **TumorSize** : Taille de la tumeur détectée 
- **TumorLocation** : Localisation anatomique de la tumeur (ovaire, trompe, péritoine)  
- **EnhancementPattern** : Motif de rehaussement sur l’imagerie médicale 
- **RadiomicTexture** : Indice de texture tumorale issu de l’imagerie  
- **RadiomicIntensity** : Mesure de l’intensité radiomique  
- **RadiomicShape** : Mesure de la forme tumorale en imagerie  
- **DopplerVelocity** : Vitesse du flux sanguin mesurée en Doppler  
- **Parity** : Nombre de grossesses du patient  
- **OralContraceptives** : Utilisation passée ou actuelle de contraceptifs oraux  
- **HormoneTherapy** : Utilisation d’un traitement hormonal substitutif  
- **MenarcheAge** : Âge au début des règles 
- **MenopauseAge** : Âge à la ménopause  
- **RiskLabel** : Niveau de risque de cancer (aucun, faible, moyen, élevé) 
- **ProgressionProbability** : Probabilité estimée de progression de la maladie


**Synthèse des définitions**:

###  Quelques définitions médicales et biologiques

- **Comorbidités** :Présence simultanée de plusieurs maladies chez un même individu, indépendamment de leur lien causal

- **CA-125** :Protéine présente dans le sang, utilisée comme marqueur tumoral, notamment dans le suivi du cancer de l'ovaire

- **Sous-types histologiques du cancer de l'ovaire** :
  - **Séreux** :Carcinome épithélial fréquent, souvent de haut grade
  - **Mucineux** :Carcinome produisant du mucus, généralement de bas grade
  - **Clear cell (à cellules claires)** :Carcinome rare, caractérisé par des cellules à cytoplasme clair

  ***Le carcinome est une lésion cancéreuse à la surface de l'épiderme de l'être humain***

- **Mutations BRCA1 et BRCA2** :Altérations génétiques augmentant significativement le risque de cancers du sein et de l'ovaire

- **Expression génique normalisée** :Processus par lequel l'information génétique est utilisée pour synthétiser des protéines, avec des données ajustées pour éliminer les variations techniques

- **Polymorphismes nucléotidiques simples (SNP)** :Variations d'une seule base dans l'ADN, fréquentes dans la population, pouvant influencer la susceptibilité aux maladies

- **Méthylation de l'ADN** :Ajout de groupes méthyle à l'ADN, modulant l'expression des gènes sans en modifier la séquence

***La méthylation de l'ADN est une marque épigénétique associée à la régulation des gènes. Elle joue un rôle clé dans un certain de nombre de processus biologiques comme l'embryogenèse, le vieillissement, la carcinogenèse ou encore l'immunité dans les maladies infectieuses***

- **Expression des microARN (miARN)** :Petits ARN non codants régulant l'expression des gènes au niveau post-transcriptionnel

- **Rehaussement en imagerie médicale** :Augmentation du signal d'un tissu en imagerie, souvent après injection d'un agent de contraste, pour améliorer la visualisation

- **Texture tumorale en imagerie** :Analyse des variations d'intensité des pixels dans une image médicale, fournissant des informations sur l'hétérogénéité tumorale

- **Intensité radiomique** :Mesure quantitative de l'intensité des signaux dans les images médicales, utilisée pour caractériser les tissus

- **Flux sanguin mesuré en Doppler** :Technique d'imagerie utilisant l'effet Doppler(examen médical échographique en deux dimensions non invasif) pour évaluer la vitesse et la direction du flux sanguin dans les vaisseaux


------------








## Approche globale du projet

1. **Nettoyage des données**  
   - Typage des colonnes (booléens, catégorielles)

2. **Analyse exploratoire**  
   - Distribution des variables continues et catégorielles
   - Corrélations et inspection des dates

3. **Modélisation**
   - **Classification :**
     - On commence par une version binaire du problème (`0: aucun risque` vs `1: risque`) .... 

   - **Régression :**
     - Modèles : régression linéaire, SVR, Random Forest Regressor

4. **Comparaison des modèles**  
   - Métriques : Accuracy, F1-score, RMSE, R² selon la tâche

5. **Interprétabilité globale**  
   - Permutation Feature Importance
   - PDP / ALE

   - H-statistic (interaction des variables)

6. **Interprétabilité locale**  
   - SHAP (Waterfall & Force Plot)
   - LIME
   - ICE plots








