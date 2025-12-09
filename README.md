# 🌱 NPK & pH Based Fertilizer Recommendation System

This project processes soil images to estimate **Nitrogen (N)**, **Phosphorus (P)**, **Potassium (K)**, **pH level**, identifies **soil type**, and generates a **fertilizer recommendation**.

It is designed as a backend-friendly pipeline that can be hosted as a service or integrated directly by ML/API teams.

---

## 🚀 Features

✔ Predicts NPK + pH from soil image  
✔ Classifies soil type  
✔ Detects whether uploaded image actually contains soil  
✔ Generates fertilizer recommendation for a selected crop  
✔ Ready for backend integration

---

│
├── app.py # Main API / inference script
├── requirements.txt # Python dependencies
│
├── models/
│ ├── npk_ph_predictor_model.pkl # Regression model for NPK + pH estimation
│ ├── model_unquant.tflite # Soil type classification (TFLite)
│ ├── model_unquant2.tflite # Soil vs Non-soil detector (TFLite)
│ ├── labels.txt # Class labels for model_unquant
│ ├── labels2.txt # Class labels for model_unquant2
│
├── utils/
│ ├── preprocessing.py # Image preprocessing & feature extraction helpers (if applicable)
│ ├── inference.py # Centralized inference pipeline functions
│
├── sample_data/
│ ├── sample_soil.jpg # Demo input for testing
│ └── example_output.json # Expected API result example
│
└── README.md # Documentation


---

## 🧠 System Workflow



Image Input
↓
Soil/Non-soil Check (model_unquant2)
↓ if valid
Soil Type Classification (model_unquant)
↓
Feature Extraction
↓
NPK + pH Prediction (npk_ph_predictor_model.pkl)
↓
Fertilizer Recommendation Layer


---

## 🛠 Installation & Setup

### 1. Create virtual environment
```bash
python -m venv venv
source venv/bin/activate     # Windows → venv\Scripts\activate

2. Install required dependencies
pip install -r requirements.txt

3. Run application
python app.py

📌 API Specification
🔹 1. Predict NPK + pH + Soil Type

Endpoint: /predict_npk
Method: POST
Request: multipart/form-data

file: <soil_image.jpg/png>


Response Example:

{
  "nitrogen": 45.2,
  "phosphorus": 20.7,
  "potassium": 32.1,
  "ph": 6.3,
  "soil_type": "Alluvial"
}

🔹 2. Generate Fertilizer Recommendation

Endpoint: /recommend_fertilizer
Method: POST
Request JSON:

{
  "nitrogen": 45.2,
  "phosphorus": 20.7,
  "potassium": 32.1,
  "ph": 6.3,
  "soil_type": "Alluvial",
  "crop": "Wheat"
}


Response Example:

{
  "recommendation_text": "Apply NPK 10-26-26 at 100kg/acre before sowing.",
  "n_deficiency": "Low",
  "p_deficiency": "Adequate",
  "k_deficiency": "Low"
}
