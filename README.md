# 🧹 Data Cleaning Pipeline — Crime Incident Dataset

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Data Cleaning](https://img.shields.io/badge/Data-Cleaning-22c55e?style=for-the-badge)

---

## 📌 Overview

A comprehensive **data cleaning and preprocessing pipeline** built in Python that takes messy crime incident data and transforms it into analysis-ready structured data. This project handles missing values, duplicates, inconsistent formatting, outliers, and data type conversions — with detailed logging and validation at every step.

Real-world crime data is often messy with inconsistent formats, missing values, and outliers. This pipeline automates the tedious process of identifying and fixing data quality issues, saving hours of manual work and ensuring your analysis starts from a solid foundation.

---

## 📊 Dataset Information

| Feature | Description |
|---------|-------------|
| **Source** | Crime Incidents Dataset |
| **Original Shape** | 5,250 rows × 33 columns |
| **Final Shape** | 4,244 rows × 33 columns |
| **Cleaning Impact** | ~19% rows removed (missing critical data) |

### Columns Overview
- **Incident Details**: `incident_id`, `crime_type`, `district`, `city`, `state`, `address`, `incident_datetime`
- **Location Data**: `latitude`, `longitude`
- **Officer Information**: `officer_id`, `officer_first_name`, `officer_last_name`, `badge_number`
- **Suspect Information**: `suspect_id`, `suspect_first_name`, `suspect_last_name`, `suspect_age`, `suspect_gender`, `suspect_race`
- **Victim Information**: `victim_id`, `victim_first_name`, `victim_last_name`, `victim_age`, `victim_gender`, `victim_phone`
- **Case Details**: `weapon_used`, `severity`, `case_status`, `resolution`, `num_arrests`, `property_loss_usd`, `reported_online`, `notes`

---

## 🖼️ Workflow Overview

![Data Cleaning Workflow](./data_cleaning_preview.png)

---

## ⚙️ How It Works

1. **Data Loading** — Load the messy CSV file into a Pandas DataFrame for processing
2. **Initial Inspection** — Analyze data structure, missing values, and basic statistics
3. **Duplicate Removal** — Identify and remove duplicate records based on `incident_id`
4. **Handle Missing Values** — Implement strategic imputation for each column type:
   - Drop rows with missing critical location/time data
   - Fill categorical columns with appropriate placeholders
   - Fill numerical columns with median/mode values
5. **Fix Inconsistent Formatting** — Standardize text across all categorical columns:
   - Title case conversion
   - Abbreviation standardization (`M` → `Male`, `F` → `Female`)
   - Typo corrections (`Investgation` → `Investigation`)
6. **Data Type Validation** — Convert columns to appropriate data types
7. **Outlier Treatment** — Cap extreme age values (>100 years) to realistic maximum
8. **Export Clean Data** — Save cleaned dataset for analysis and reporting

---

## 🧩 Key Operations

### Missing Values Treatment
| Column | Missing % | Strategy |
|--------|-----------|----------|
| `suspect_race` | 30.5% | Filled with "Unknown" |
| `suspect_gender` | 26.9% | Filled with mode |
| `suspect_age` | 20.9% | Filled with median |
| `victim_phone` | 20.1% | Filled with "000-000-0000" |
| `notes` | 20.4% | Filled with "No Available Notes" |
| `latitude`, `longitude`, `incident_datetime` | 5-6.5% | Rows dropped |

### Inconsistency Fixes
- **District Names**: Standardized abbreviations (`Sou` → `South`, `Cen` → `Central`, `Nor` → `North`, etc.)
- **Gender Values**: Converted `M`/`F` to `Male`/`Female`
- **Case Status**: Fixed misspellings (`Investgation` → `Investigation`, `Pendng` → `Pending`)
- **Severity**: Standardized values (`1` → `Low`, `2` → `Medium`, `3` → `High`, `4` → `Critical`)
- **Phone Numbers**: Reformatted to `XXX-XXX-XXXX` pattern
- **Reported Online**: Converted `True`/`False`/`1`/`0` to `Yes`/`No`

### Outlier Treatment
- **Age Capping**: Any age > 100 years capped at 100
- **Arrests**: Negative values converted to absolute values
- **Property Loss**: Fixed corrupted decimal formatting and converted to float

---

## 💡 Key Design Decisions

- **Strategic Null Handling** — Critical location/time columns with missing values were dropped rather than imputed to maintain data integrity
- **Consistent Categorical Standards** — All text fields standardized to title case for uniformity
- **Age Capping** — Realistic age bounds (0-100) implemented to remove impossible values
- **Preserving Integrity** — `incident_id` used as primary key for duplicate detection
- **Phone Number Standardization** — Uniform formatting for better analysis and readability

---

## 🎯 Use Case

Built for **crime incident data analysis** — perfect for law enforcement agencies, criminology researchers, or urban planners looking to analyze crime patterns without spending hours on data preprocessing.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Pandas** | Data manipulation and cleaning |
| **NumPy** | Numerical operations |
| **Matplotlib** | Data visualization (optional) |
| **Jupyter Notebook** | Interactive development environment |
| **Python** | Core programming language |

---

## 📂 Repository Structure

```
data-cleaning-pipeline/
│
├── crime_incidents_messy.csv          # Raw messy dataset
├── Clean_Crime_Incident.csv           # Cleaned output dataset
├── data_cleaning_pipeline.ipynb       # Jupyter notebook with all code
├── data_cleaning_preview.png          # Workflow visualization
├── requirements.txt                   # Required Python packages
└── README.md                          # This file
```

---

## ▶️ How to Use This Project

1. **Clone the repository:**
   ```bash
   git clone https://github.com/BhadurAli/data-cleaning-pipeline.git
   cd data-cleaning-pipeline
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Open the Jupyter Notebook:**
   ```bash
   jupyter notebook data_cleaning_pipeline.ipynb
   ```

4. **Run all cells** to execute the cleaning pipeline from start to finish

5. **Check the output:** The cleaned dataset will be saved as `Clean_Crime_Incident.csv`

---

## 📈 Results

| Metric | Before Cleaning | After Cleaning |
|--------|----------------|----------------|
| Rows | 5,250 | 4,244 |
| Missing Values | Multiple columns >20% missing | 0% missing in all columns |
| Duplicate Rows | 200 | 0 |
| Inconsistent Categories | Multiple formats | Standardized formats |
| Data Types | Mixed/incorrect | Properly typed |

---

## 🔄 Customization

To adapt this pipeline for your own dataset:

1. **Replace input file** — Update `df = pd.read_csv("your_dataset.csv")`
2. **Adjust columns** — Modify column names to match your dataset
3. **Customize imputation** — Change fill strategies based on your data characteristics
4. **Update validation rules** — Modify age limits, standardization rules, etc.

---

## 👨‍💻 Author

**Bhadur Ali** — Data Analyst & Junior Data Scientist

MS Data Science · PAF-IAST

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/bhadur-ali)
[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:alikhansalar5@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/BhadurAli)

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).
