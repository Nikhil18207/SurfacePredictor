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

### ⚙️ Final Model Configuration (from Optuna)


XGBClassifier(
    max_depth=10,
    learning_rate=0.0617,
    n_estimators=216,
    subsample=0.8088,
    colsample_bytree=0.8504,
    eval_metric='mlogloss'
)

📈 Accuracy Improvement Summary
| Phase                          Nasdaq: GBNB
| Initial RandomForest        | ~26%      |
| Raw XGBoost (1 feature)     | ~69%      |
| + Feature Engineering       | ~70%      |
| + Optuna Hyperparameter Tuning | 70.76% ✅ |

🧪 Evaluation on Unseen GLOVE_2.csv
Created a separate GLOVE_2.csv for real-world simulation
Model predicted GLOVE correctly for 126 out of 139 samples
Accuracy on GLOVE_2: 90.65%
Confusions mostly occurred with similar surfaces (e.g., ACRYLIC, SMOOTH WOODEN)
🔮 Real-Time Inference
Live prediction works with:

python

Copy
sample = np.array([[resistance, diff, mean, std]])
prediction = model.predict(sample)
✔️ Integrates well with Arduino/Raspberry Pi sensor feeds

💾 Deployment Ready
✅ Model can be saved with joblib
✅ Can be embedded in a Flask API, desktop app, or microcontroller interface
✅ Feature pipeline standardized for any incoming sensor data
📌 Next Steps
🧪 Collect more samples per surface for even better accuracy
📈 Visualize t-SNE and feature importances
🚀 Deploy with edge ML on Raspberry Pi
🧠 Try 1D CNN or LSTM for sequence-based learning


