

## 🛠️ Project Workflow (ML + UI Integrated)

### ⚙️ PHASE 1: Data Foundation

📍 *Goal: Build a solid dataset with weather + AQI + geo-coordinates*

| Step | Task                                                        | Tool                              |
| ---- | ----------------------------------------------------------- | --------------------------------- |
| 1    | Select a Kaggle/open dataset (`weather`, `AQI`, `location`) | Kaggle/OpenAQ API                 |
| 2    | Preprocess: clean missing, timestamp sync, normalize        | Pandas, NumPy                     |
| 3    | Optional: Label each location (e.g., "Safe", "Danger")      | Manual or rule-based              |
| 4    | Save processed CSV + geo-coordinates                        | `.csv` for ML, `.geojson` for map |

✅ **Deliverable**: Clean dataset for modeling + map use

---

### 🤖 PHASE 2: ML Model Training

📍 *Goal: Train models that can forecast, classify, cluster, and explain environmental status*

| Model                               | Purpose                              | Tool / Lib                |
| ----------------------------------- | ------------------------------------ | ------------------------- |
| 🔮 **Time Series (LSTM / Prophet)** | Forecast AQI or Temp                 | PyTorch, Facebook Prophet |
| ⚠️ **Anomaly Detection**            | Detect weird spikes or outliers      | Isolation Forest, Z-Score |
| 🧠 **Classifier**                   | Label Safe/Moderate/Unsafe zones     | XGBoost, RandomForest     |
| 🔍 **Clustering (Unsupervised)**    | Group similar regions without labels | KMeans, DBSCAN, HDBSCAN   |
| 💬 **XAI**                          | Explain model predictions            | SHAP, LIME                |

---

### 💡 What Clustering Adds:

* Discover **natural groupings** of areas (e.g. clean, mixed, toxic zones)
* Useful when labeled data (safe/unsafe) is missing or noisy
* Can **visualize clusters** on your map for city planning / alerts
* Use **PCA / t-SNE / UMAP** for dimensionality reduction before clustering

---

### 📌 Example Use Case:

> “Cluster locations into 3 groups based on last 24-hour AQI, temp, humidity — label them as Clean, Caution, Dangerous — and color the map accordingly.”

---

### ✅ New Deliverables:

* Trained `.pkl` clustering model (e.g., `aqi_clusters.pkl`)
* GeoJSON layer for clustered zones on map
* Optional: Live cluster switching UI on dashboard

---

### 🔌 PHASE 3: Backend API (Python Flask / Node.js Express)

📍 *Goal: Serve real-time predictions to frontend*

| Step | Task                                                           |
| ---- | -------------------------------------------------------------- |
| 1    | Create Flask/Express API (`/predict`, `/classify`, `/explain`) |
| 2    | Connect with trained ML models                                 |
| 3    | Accept POST req: `{lat, lon, timestamp}`                       |
| 4    | Respond: prediction + XAI + status                             |

✅ **Deliverable**: Running ML backend (can deploy on Render, Vercel, or Railway)

---

### 🌐 PHASE 4: UI Integration (Your Existing HTML+JS)

📍 *Goal: Integrate ML results into the awesome UI you already built*

| Feature          | What to Add                                         |
| ---------------- | --------------------------------------------------- |
| 🧠 Predictions   | Show future AQI/Temp (e.g. “AQI in 1 hr: 142 🔴”)   |
| ⚠️ Anomaly Flags | Highlight spikes in red, log them                   |
| 🧭 Status Badge  | Use ML classification to tag zone: “Safe / Danger”  |
| 💬 XAI           | Tooltip: “AQI High because PM2.5 = 143, Wind = Low” |
| 🔥 Heatmap       | Use prediction confidence to render in Leaflet      |

✅ **Deliverable**: Smart ML-driven frontend, alerting, chart overlays


## 🧠 Project Name:

**EnviroCast: AI-Powered Environmental Monitoring & Model Comparison Dashboard for Dhaka**

---

## 🎯 Final Output Summary:

* Cleaned datasets (AQI + weather)
* 6 trained models (LSTM, Prophet, RF, XGBoost, Isolation Forest, AutoEncoder)
* FastAPI backend (`/predict`, `/classify`, `/explain`, `/drift-check`, `/compare`)
* Dashboard (Tailwind + Leaflet + Chart.js) with:

  * Forecasts
  * Classification
  * Anomaly detection
  * Drift alerts
  * SHAP explanations
  * 📊 Bar + Pie Charts for model comparisons
* `README.md` + system docs

---

## 🧩 Dataset Links

| Name                                    | Description                                                                     | Kaggle Link                                                                           |
| --------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Air Quality Data Set for Dhaka City** | Daily AQI, PM2.5, coordinates (used for forecasting, classification, anomalies) | [🔗 Link](https://www.kaggle.com/datasets/mahdilu/air-quality-dataset-for-dhaka-city) |
| **Weather Data in Dhaka (2008–2018)**   | Temp, humidity, wind speed — used for correlation & drift detection             | [🔗 Link](https://www.kaggle.com/datasets/ashrafulhaque/weather-data-in-dhaka-city)   |

---

## ⚙️ Tech Stack

* **Backend**: Python (FastAPI, MLflow, Evidently)
* **Frontend**: HTML + TailwindCSS + Chart.js + Leaflet.js
* **ML Libraries**: scikit-learn, XGBoost, TensorFlow/Keras, Prophet, SHAP, DVC (optional)
* **Visualization**: SHAP plots, Chart.js
* **Deployment (optional)**: Render / HuggingFace Spaces / Docker

---

## 🗓️ ADHD-Friendly 3-Day Plan (\~16–18 hrs)

---

### 🚀 **Day 1: Dataset Cleaning & Model Training** (\~6h)

#### ✅ Task 1: Clean AQI Dataset (1.5h)

* Load CSV
* Drop missing/nulls
* Normalize PM2.5
* Label AQI: Safe (<50), Moderate (50–150), Danger (>150)
* Save as `aqi_cleaned.csv`

#### ✅ Task 2: Forecasting – LSTM vs Prophet (2h)

* LSTM:

  * Seq2Seq (past 24h ➜ next 24h AQI)
  * Normalize series, reshape to \[samples, timesteps, features]
* Prophet:

  * Fit `ds` (timestamp) + `y` (AQI)
* Compare MAE on test split

#### ✅ Task 3: Classification & Anomaly Models (1.5h)

* RF + XGBoost → Label prediction

  * Input: AQI, PM2.5
  * Output: Safe/Moderate/Danger
  * Metric: Accuracy, F1
* Isolation Forest + AutoEncoder → Anomalies (PM2.5 > 200)

  * Metric: Precision, recall
* Save models as `.pkl`

#### ✅ Task 4: Drift Detection Baseline (1h)

* Evidently:

  * Calculate mean, std, quantiles
  * Save as JSON baseline

#### 🧾 Deliverables:

* `aqi_cleaned.csv`
* 6 models
* MAE, accuracy, F1, precision, recall
* Drift baseline `.json`

---

### 🧪 **Day 2: XAI, Few-Shot Learning, API** (\~6h)

#### ✅ Task 1: Correlate Weather Data (1.5h)

* Join `aqi_cleaned.csv` + Weather data on timestamp
* Compute Pearson correlation: AQI vs. temp, humidity
* Save `merged.csv`

#### ✅ Task 2: Few-Shot Learning (1.5h)

* Manually label 20 new points
* Fine-tune RandomForest with `PEFT` concept (simulate few-shot)
* Compare before/after F1

#### ✅ Task 3: SHAP XAI (1.5h)

* Use `TreeExplainer` on RandomForest
* Visual: Force plots, bar plots
* Save SHAP values as `.json`, images as `.png`

#### ✅ Task 4: FastAPI Setup (1.5h)

* `/predict` – AQI forecast (LSTM, Prophet)
* `/classify` – Classifier output
* `/explain` – SHAP json/plots
* `/drift-check` – PM2.5 drift warning
* `/compare` – Model metrics JSON

#### 🧾 Deliverables:

* `merged.csv`
* SHAP files
* Fine-tuned model
* FastAPI with 5 working endpoints

---

### 📊 **Day 3: Dashboard + Graphs + Final Polish** (\~5–6h)

#### ✅ Task 1: Chart.js Model Graphs (1.5h)

* Fetch from `/compare`
* Bar Chart: LSTM vs Prophet (MAE)
* Bar Chart: RF vs XGBoost (Acc, F1)
* Pie: Isolation Forest vs AutoEncoder (Precision)

#### ✅ Task 2: Full Dashboard Integration (1.5h)

* Prediction card: “Next AQI: 175 🔴 Danger”
* Map with Leaflet (flag anomalies)
* SHAP: “PM2.5=185 → AQI 175”
* Model comparison section (graphs)
* Drift alerts

#### ✅ Task 3: Backend Finalization & Drift Logic (1.5h)

* Add drift threshold logic (Evidently)
* Alert if PM2.5 shifts >20%
* Log API calls

#### ✅ Task 4: Testing + README (0.5h)

* Manual tests (API, frontend, graphs)
* Write `README.md` with:

  * Dataset links
  * Model details
  * How to run API
  * Graph explanation

#### 🧾 Final Deliverables:

* Dashboard HTML/CSS/JS (Chart.js)
* API backend (FastAPI)
* SHAP plots, prediction cards
* Drift alert engine
* `README.md`

---

## 🧠 Bonus: Real-World Use Case & CV Boost

| Aspect                       | Value                                                        |
| ---------------------------- | ------------------------------------------------------------ |
| 📍 **City**                  | Dhaka, Bangladesh                                            |
| 🧪 **Use Case**              | Pollution prediction, early anomaly detection                |
| 🔍 **XAI**                   | SHAP explains predictions (trust + accountability)           |
| ⚡ **Few-Shot + Drift**       | Adapts to new data, real-world deployable                    |
| 📊 **Graphs**                | Transparent model performance comparisons                    |

---


