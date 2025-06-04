# BGP Network Mapping with Logistic Regression

This project applies **logistic regression** to classify **Autonomous System (AS) relationships** using BGP data, specifically identifying whether a relationship is **peer-to-peer (P2P)** or **customer-to-provider (C2P)**.

## 📁 Project Structure

```
├── bgp_network_mapping_with_logistic_regression.py
├── rib.20250501.0000.bz2 (optional input)
├── feature_names_final.txt (output)
├── bgp_as_relationships_processed_final.csv (output)
└── README.md
```

## 🌐 Data Sources

- **CAIDA AS Relationships**:  
  [https://publicdata.caida.org/datasets/as-relationships/](https://publicdata.caida.org/datasets/as-relationships/)
- **RouteViews BGP Data**:  
  [http://archive.routeviews.org/](http://archive.routeviews.org/)

## 📦 Requirements

Ensure the following Python packages are installed:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn requests
```

Optional for full BGP parsing:
```bash
pip install bgpkit-parser
```

## 🚀 How to Run

1. **Download a RouteViews RIB file** manually or allow the script to download a sample.
2. **Update the script** to set `USER_PROVIDED_RIB_FILE_PATH` to your file location (optional).
3. Run the main script:
```bash
python bgp_network_mapping_with_logistic_regression.py
```

## 🧠 Methodology

1. **Data Collection**:  
   Downloads CAIDA relationship data and optionally BGP RIB files.

2. **Feature Engineering**:  
   - Path length difference  
   - Prefix ratios  
   - AS degrees  
   - Geographic distance  
   - Community similarity  
   - Path prepending  
   - Common neighbors  
   - Route stability  
   - Path diversity

3. **Preprocessing**:  
   - Missing value handling  
   - Feature scaling via `StandardScaler`  
   - Class imbalance handled with `class_weight='balanced'`

4. **Model Training**:  
   Logistic regression via `scikit-learn` with stratified train-test split.

5. **Evaluation Metrics**:  
   - Accuracy  
   - Precision / Recall / F1-Score  
   - ROC AUC  
   - Coefficient-based feature importance

## 📊 Outputs

- `bgp_as_relationships_processed_final.csv`  
  Final feature-enriched dataset
- `feature_names_final.txt`  
  List of features used
- Console output includes:
  - Classification report
  - ROC AUC
  - Top feature importances (logistic regression coefficients)

## 📈 Interpretability

Logistic regression provides interpretable coefficients to explain:
- Which features increase the likelihood of a C2P relationship.
- Which features are indicative of peer relationships.

## 🔬 Limitations & Future Work

- Real BGP feature enrichment requires `bgpkit-parser` and significant compute resources.
- Consider more advanced models (e.g., Random Forest, XGBoost) for non-linear interactions.
- Evaluate performance using grouped or time-aware cross-validation to avoid leakage.

## 📄 License

This project is for academic and educational use as part of a logistic regression assignment. All data used is public and research-safe.
