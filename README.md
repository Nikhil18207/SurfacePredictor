# Surface Recognition Using Pressure Sensor Data

This project focuses on detecting different surface types (e.g., acrylic, glove, metal, marble) based on resistance values collected using an electronic pressure sensor. It integrates machine learning with real-world IoT data, aiming to enable smart surface identification in embedded systems.

## 🧠 Objective

To classify various surfaces using resistance readings captured from a pressure sensor and predict the correct surface in real-time using a machine learning model.

## 📁 Dataset Summary

- **10 surface classes**:  
  ACRYLIC, BUBBLEWRAP BACK, BUBBLEWRAP FRONT, CARDBOARD, GLASS, GLOVE, MARBLE, METAL, PAPER, SMOOTH WOODEN
- Each class has approximately **30–70 resistance samples**
- Data collected via pressure sensors, stored in **CSV files (.csv)**
- Resistance readings range from **~3000 to ~210000 ohms**

## 🔧 Preprocessing Steps

- Replaced "?" with NaN, dropped empty and Unnamed columns
- Removed outliers (e.g., Resistance > 50000)
- Extracted numerical features:
  - Resistance
  - Resistance_diff (rate of change)
  - Rolling_mean_5 (local trend)
  - Rolling_std_5 (local variation)
- Applied **SMOTE** to balance underrepresented classes

## 🧠 Model Architecture

We used the following models and enhancements:

| Model         | Notes                                      |
|---------------|--------------------------------------------|
| RandomForest  | Initial baseline (~26% accuracy)           |
| XGBoost       | Boosted performance significantly          |
| Optuna Tuning | Found best XGBoost hyperparameters         |
| SMOTE         | Balanced the dataset classes               |

## ⚙️ Final Model Configuration (from Optuna)

```python
XGBClassifier(
    max_depth=10,
    learning_rate=0.0617,
    n_estimators=216,
    subsample=0.8088,
    colsample_bytree=0.8504,
    eval_metric='mlogloss'
)
```

## 📈 Accuracy Improvement Summary

"Phase","Accuracy"
"Initial RandomForest","~26%"
"Raw XGBoost (1 feature)","~69%"
"+ Feature Engineering","~70%"
"+ Optuna Hyperparameter Tuning","70.76% ✅"
