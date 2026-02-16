# Income Prediction and Customer Segmentation

## 1. Project Overview

This project builds two machine learning solutions for a retail marketing client using 1994–1995 U.S. Census survey data.

- **Task 1 – Income Classification**: Predict whether an individual's income is **> 50K** or **≤ 50K** using 40+ demographic and employment variables.
- **Task 2 – Customer Segmentation**: Create **actionable customer segments** for targeted marketing using demographic, employment, financial, and household characteristics.

**Deliverables:**

- Jupyter notebook: `Income_prediction_and_customer_segmentation.ipynb` (end-to-end code)
- Client report: `Income_prediction_and_customer_segmentation_report.docx`
- Raw data files: `census-bureau.data`, `census-bureau.columns`
- This `README.md`

**The notebook includes:**

- Data exploration, feature engineering, and quality checks
- Model training, evaluation, and threshold optimization for the classifier
- K-Means customer segmentation and detailed segment profiling for marketing

---

## 2. Project Structure

```text
.
├── Income_prediction_and_customer_segmentation.ipynb
├── Income_prediction_and_customer_segmentation_report.docx
├── census-bureau.data
├── census-bureau.columns
└── README.md
```

---

## 3. Environment Setup

### 3.1 Prerequisites

- Python **3.9+**
- Jupyter support (via `jupyter` or VS Code's Jupyter extension)
- Recommended: virtual environment (`venv` or `conda`)

### 3.2 Install Dependencies

From the project folder:

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS/Linux
source venv/bin/activate

pip install --upgrade pip
pip install -r requirements.txt
```

If `requirements.txt` is not provided, a minimal set consistent with the notebook is:

```text
pandas
numpy
scikit-learn
matplotlib
seaborn
```

---

## 4. Data Files

Place the following in the **same folder** as the notebook (or adjust paths inside the notebook):

- `census-bureau.data` – main dataset (comma-delimited Census records)
- `census-bureau.columns` – header file mapping column names to positions

The notebook reads these files and constructs the feature matrix and target label (income > 50K vs ≤ 50K).

---

## 5. How to Run the Notebook

1. **Activate the environment** (if using one):

   ```bash
   # Windows
   venv\Scripts\activate
   # macOS/Linux
   source venv/bin/activate
   ```

2. **Open the project in VS Code**:
   - `File` → `Open Folder…` → choose the folder containing the notebook and data.

3. **Open the notebook**:
   - In VS Code Explorer, open `Income_prediction_and_customer_segmentation.ipynb`.

4. **Select the Python interpreter**:
   - Click the interpreter selector at the top-right of the notebook and choose the environment where you installed the dependencies.

5. **Run all cells**:
   - Use **"Run All"** or run cells sequentially from top to bottom.

**The notebook will:**

- Perform data preparation and feature engineering (age groups, capital indicators, education level, etc.)
- Validate feature ranges and correlations, and remove highly collinear engineered features
- Create a stratified 80/20 train–test split with survey weights
- Train and compare three classifiers: Logistic Regression, Random Forest, and Histogram Gradient Boosting
- Select Histogram Gradient Boosting as the final model and perform threshold optimization (precision/recall, profit, ROI, lift)
- Filter to viable marketing targets and run K-Means segmentation (K=6) with PCA diagnostics and silhouette analysis
- Generate plots and segment profiles summarizing key characteristics and marketing recommendations

---

## 6. Key Results (Reproducible from the Notebook)

**Classification** — using the final Histogram Gradient Boosting model:

- Test ROC-AUC ≈ **0.9533**
- Accuracy ≈ **87.5%**, Precision ≈ **31.9%**, Recall ≈ **89.1%** at threshold 0.5
- 5-fold stratified CV ROC-AUC ≈ **0.9506** with low variance, indicating excellent generalization

Threshold analysis shows that **0.5** is a good default threshold for balancing coverage, precision, and ROI for the premium marketing scenario.

**Customer Segmentation:**

- ~**92,601** viable customers after filtering
- **6 segments** (K=6) with modest silhouette score (~0.189), interpreted as business-oriented groupings
- Segments include premium groups like "Affluent Investors" and "High-Earning Professionals", and value segments such as "Domestic Partners", "Immigrant Workforce", and "Young Singles"

---

## 7. Notes

- All models use `class_weight="balanced"` and survey weights to account for class imbalance and survey design.
- PCA is used **only for visualization**; clustering uses the full 13-dimensional feature space.
- The separate report file (`Income_prediction_and_customer_segmentation_report.docx`) summarizes the approach, results, and business implications for a non-technical client audience.
```