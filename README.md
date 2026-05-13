# 🩺 Diabetes Analysis — Exploration & Preprocessing

Analyse exploratoire et préparation des données du dataset Pima Indians Diabetes.

---

## 📋 Description

Ce projet effectue une analyse exploratoire (EDA) et un nettoyage complet d'un dataset
médical de prédiction du diabète. Il constitue la première étape d'un pipeline
de Machine Learning : comprendre les données, détecter les anomalies, et les corriger
avant toute modélisation.

---

## 📁 Structure du projet

```
diabetes_analysis/
├── 01_data_exploration.ipynb   # Notebook principal : EDA + nettoyage + normalisation
├── diabetes.csv                # Dataset brut original
├── diabetes_clean.csv          # Dataset nettoyé et normalisé (généré par le notebook)
└── README.md
```

---

## 📊 Dataset

**Source :** Pima Indians Diabetes Database (UCI / Kaggle)

**Dimensions :** 768 observations × 9 variables

| Variable | Description |
|---|---|
| `Pregnancies` | Nombre de grossesses |
| `Glucose` | Concentration en glucose (test oral) |
| `BloodPressure` | Pression artérielle diastolique (mm Hg) |
| `SkinThickness` | Épaisseur du pli cutané tricipital (mm) |
| `Insulin` | Insuline sérique 2h (mu U/ml) |
| `BMI` | Indice de masse corporelle (kg/m²) |
| `DiabetesPedigreeFunction` | Score génétique du diabète |
| `Age` | Âge (années) |
| `Outcome` | **Variable cible** — 1 = diabétique, 0 = non diabétique |

---

## 🔧 Étapes du notebook

### 1. Chargement & exploration initiale
- Aperçu du dataset (`head`, `describe`)
- Distribution de la variable `Glucose` (histogramme + KDE)
- Pairplot coloré par `Outcome`
- Heatmap de corrélation

### 2. Nettoyage des données
- Détection des **valeurs aberrantes encodées comme zéros** dans les colonnes médicales :
  `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`
- Remplacement des zéros par la **médiane** de chaque colonne
- Traitement des **valeurs extrêmes** par clipping (percentiles 1% / 99%) sur `Insulin`, `Pregnancies`, `BMI`

### 3. Normalisation
- Séparation features / cible (`X` / `y`)
- Normalisation avec **StandardScaler** (moyenne=0, écart-type=1)
- Sauvegarde du dataset nettoyé → `diabetes_clean.csv`

### 4. Analyse des corrélations
- Heatmap de corrélation après nettoyage
- Ranking des variables par corrélation avec `Outcome`

---

## 🚀 Installation & lancement

```bash
# Cloner le dépôt
git clone https://github.com/<TON_USERNAME>/diabetes_analysis.git
cd diabetes_analysis

# Installer les dépendances
pip install pandas scikit-learn matplotlib seaborn jupyter

# Lancer le notebook
jupyter notebook 01_data_exploration.ipynb
```

---

## 📦 Dépendances

| Librairie | Usage |
|---|---|
| `pandas` | Manipulation des données |
| `scikit-learn` | Normalisation (StandardScaler) |
| `matplotlib` | Visualisations |
| `seaborn` | Visualisations statistiques |

---

## 📈 Résultats clés

Variables les plus corrélées avec le diabète (`Outcome`) :

1. **Glucose** — corrélation la plus forte
2. **BMI**
3. **Age**
4. **Pregnancies**
5. **DiabetesPedigreeFunction**

> `Insulin` et `SkinThickness` présentent le plus de valeurs manquantes (encodées comme zéros),
> ce qui justifie le nettoyage par médiane.
