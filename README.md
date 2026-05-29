# 🌱 Carbon Footprint & Food Emission Analysis

> *An end-to-end Data Science project analyzing carbon emissions from food and consumer products to support more sustainable lifestyle choices.*

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Workflow](#-workflow)
- [Key Findings](#-key-findings)
- [Technologies Used](#-technologies-used)
- [How to Run](#-how-to-run)
- [Recommendations](#-recommendations)

---

## 🔍 Overview

Food production contributes approximately **26% of total global greenhouse gas emissions** — from agriculture and processing to distribution and consumption. This project performs a comprehensive analysis of carbon emissions (kg CO₂eq) across various food categories to uncover patterns, identify the highest and lowest emitting foods, and validate differences statistically.

**Business Questions Answered:**

1. Which food categories have the highest average carbon emissions?
2. What are the top 10 highest and lowest carbon-emitting foods?
3. Is there a statistically significant difference between animal-based and plant-based foods?
4. Are the top 3 emission categories significantly higher than the rest?

---

## 📦 Dataset

| File | Description | Rows |
|------|-------------|------|
| `dataset_footprint_emission.csv` | Raw base dataset (original from Kaggle) | 1,300 |
| `dataset_footprint_emission_complete.csv` | Curated complete dataset | 69 |
| `dataset_footprint_emission_final.csv` | Cleaned & merged final dataset (used for analysis) | 290 |

**Source:** [Food and Product Carbon Emission Dataset — Kaggle](https://www.kaggle.com/datasets/azraindrop/food-and-product-carbon-emission-dataset)

### Column Dictionary

| Column | Type | Description |
|--------|------|-------------|
| `no` | int | Sequential row number |
| `nama` | string | Food/product name |
| `emisi` | float | Carbon emission in **kg CO₂eq per kg** of product |
| `kategori` | string | Food category (20 categories) |

### Dataset Statistics (Final)

| Metric | Value |
|--------|-------|
| Total records | 290 |
| Total categories | 20 |
| Min emission | 0.15 kg CO₂eq |
| Max emission | 99.48 kg CO₂eq |
| Mean emission | 3.14 kg CO₂eq |
| Median emission | 0.68 kg CO₂eq |

### Food Categories

`Bakery Products` · `Beverages` · `Condiments & Sauces` · `Dairy Products` · `Eggs` · `Fast Food` · `Fats & Oils` · `Fish & Seafood` · `Fruits` · `Grains & Cereals` · `Legumes` · `Meat & Poultry` · `Mixed Dishes` · `Nuts & Seeds` · `Plant-Based Protein` · `Root Crops` · `Soups` · `Sweeteners` · `Sweets & Desserts` · `Vegetables`

---

## 📁 Project Structure

```
Data Science/
├── dataset_footprint_emission.csv          # Raw base dataset (1,300 rows)
├── dataset_footprint_emission_complete.csv # Curated complete data (69 rows)
├── dataset_footprint_emission_final.csv    # Final cleaned dataset (290 rows)
└── footprint_emission_analysis.ipynb       # Main analysis notebook
```

---

## 🔄 Workflow

This project follows a structured end-to-end Data Science pipeline:

### 1. 🔍 Problem Identification
Defining business questions and objectives around food carbon emissions.

### 2. 📦 Data Gathering
Loading both datasets (`dataset_footprint_emission_complete.csv` and `dataset_footprint_emission.csv`) into Pandas DataFrames.

### 3. 🔎 Assessing Data
- Missing value detection
- Duplicate checking
- Category inconsistency identification (capitalization, spacing)
- Data type validation
- Outlier / anomaly detection

### 4. 🧹 Cleaning Data
- Removed quotation marks from product names
- Standardized category names (Title Case, trimmed whitespace)
- Merged both datasets, keeping all 69 complete records intact
- Sorted alphabetically and reset row numbers
- Exported as `dataset_footprint_emission_final.csv`

### 5. 📊 Exploratory Data Analysis (EDA)
- Descriptive statistics
- Category distribution
- Top 10 highest & lowest emission foods
- Average emission per category
- Distribution analysis (right-skewed)

### 6. 📈 Data Visualization
7 visualizations including bar charts, box plots, scatter plots, and distribution histograms built with **Matplotlib** and **Seaborn**.

### 7. 📖 Data Dictionary
Full documentation of all columns and categories.

### 8. ⚙️ Feature Engineering
New features created on a separate analysis dataframe (`df_fe`):

| Feature | Description |
|---------|-------------|
| `emisi_level` | Emission tier: Low / Medium / High / Very High (quantile-based) |
| `emisi_log` | Log-transformed emission (reduces right skew) |
| `emisi_scaled` | Min-Max scaled emission (0–1) |
| `kategori_encoded` | Label-encoded category |
| `is_animal_based` | Binary flag: 1 = animal-based, 0 = plant-based/other |
| `emisi_zscore` | Z-score of emission value |
| `is_outlier` | Binary flag: 1 if \|z-score\| > 3 |

### 9. 🧪 Statistical Testing (A/B Testing)

| Test | Groups | Method | Result |
|------|--------|--------|--------|
| Test 1 | Animal-Based vs Plant-Based | T-Test + Mann-Whitney U | ✅ Significant difference |
| Test 2 | Top-3 Categories vs Others | Mann-Whitney U | ✅ Significant difference |
| Test 3 | Emission level groups | Kruskal-Wallis H-Test | ✅ Significant difference |

### 10. 🏁 Conclusion
Summary of findings and actionable recommendations.

---

## 💡 Key Findings

- **Meat & Poultry** dominates carbon emissions — beef alone reaches **33–99 kg CO₂eq/kg**
- The top highest-emitting foods are: beef, lamb & mutton, cheese, and farmed prawns
- The lowest-emitting foods are: mineral water, most vegetables, and fruits
- Emission data is **highly right-skewed** — the majority of foods emit below 1 kg CO₂eq/kg
- Animal-based foods have **statistically significantly higher** emissions than plant-based foods (p < 0.05)

---

## 🛠️ Technologies Used

| Library | Version | Purpose |
|---------|---------|---------|
| `pandas` | latest | Data manipulation & analysis |
| `numpy` | latest | Numerical computing |
| `matplotlib` | latest | Data visualization |
| `seaborn` | latest | Statistical visualization |
| `scipy` | latest | Statistical testing (T-Test, Mann-Whitney, Kruskal-Wallis) |
| `scikit-learn` | latest | Feature engineering (LabelEncoder, MinMaxScaler) |

---

## 🚀 How to Run

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn jupyter
```

### Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/Muhammad-Daffa-Alghifari/Dicoding-Data-Science.git
   cd Dicoding-Data-Science
   ```

2. **Place all dataset files** in the same directory as the notebook:
   - `dataset_footprint_emission.csv`
   - `dataset_footprint_emission_complete.csv`
   - `dataset_footprint_emission_final.csv`

3. **Launch Jupyter Notebook**
   ```bash
   jupyter notebook footprint_emission_analysis.ipynb
   ```

4. **Run all cells** from top to bottom (`Kernel → Restart & Run All`)

> ⚠️ The notebook uses local relative paths for datasets. Ensure all CSV files are in the same folder as the `.ipynb` file.

---

## 🌱 Recommendations

### For Consumers
1. **Reduce red meat consumption** — especially beef, which produces up to 99 kg CO₂eq/kg
2. **Switch to plant-based protein** — tofu, tempeh, and legumes emit 10–50× less than meat
3. **Choose local vegetables and fruits** — lowest emission and widely available
4. **Limit fast food** — combines multiple high-emission ingredients

### For Researchers / Analysts
1. Expand dataset with **water footprint** and **land use** data for full Life Cycle Assessment (LCA)
2. Incorporate **regional emission factors** for more localized insights
3. Develop a **carbon footprint calculator** using this dataset as the base

---

## 📄 License

This project is open-source. Dataset sourced from Kaggle under its respective license — see the [dataset page](https://www.kaggle.com/datasets/azraindrop/food-and-product-carbon-emission-dataset) for details.

---

<p align="center">
  Made with 🌍 for a more sustainable future
</p>
