# PAW-ANALITICS: From Intake to Outcome 🐾

**A Machine Learning Framework for Predicting Shelter Decisions and Length of Stay (LOS)**

PAW-ANALITICS is an end-to-end predictive operations system developed using the **Dallas Animal Shelter** public dataset (FY 2022-2023). 

This project addresses critical shelter challenges—specifically overcrowding and resource misallocation—by providing staff with real-time, interpretable AI briefings.

---

## Key Features

* **Dual-Model Pipeline**: Combines classification for outcome prediction and regression for stay duration.
* **Agentic AI Layer**: Utilizes **Gemini 2.5 Flash** to translate raw model probabilities into actionable natural language staff briefings.
* **Real-time Decision Support**: Integration with a **Telegram Bot** for mobile alerts and a **PowerBI** dashboard for historical exploration.
* **Transparent Logic**: Implements **SHAP** analysis to explain the "why" behind every prediction.

---

## Technical Deep Dive

### 1. Exploratory Data Analysis (EDA)
We processed over **34,800 observations** using **Power BI** to uncover operational trends.
* **Outcome Distribution**: Adoption is the most frequent outcome (~25%), followed by Euthanasia (~22%).
* **Species Variance**: Stay durations vary significantly by animal type; livestock average the longest stays (~18 days), while wildlife has the shortest (~3 days).
* **Skewness**: Length of Stay (LOS) is highly right-skewed, requiring target transformation for effective modeling.

### 2. Machine Learning Stack
* **Classification (Live vs. Non-Live)**: 
    * **Winner**: **Random Forest** (Selected over Logistic Regression and CatBoost).
    * **Performance**: Achieved a **0.915 ROC-AUC** and **84% Accuracy** on the held-out test set.
* **Regression (Length of Stay)**: 
    * **Winner**: **XGBoost Regressor**.
    * **Performance**: Achieved a Mean Absolute Error (MAE) of **5.56 days** using a $log(1+LOS)$ target transformation to handle skewness.

### 3. Feature Engineering & Selection
* **Feature Engineering**: Transformed 33 raw columns into 13 optimized model features, including engineered datetime predictors like "Weekend Indicator".
* **Data Leakage Mitigation**: A critical fix was implemented to remove outcome-related variables, correcting the baseline ROC-AUC from a biased 0.96 to a realistic 0.86.

---

## Architecture

The solution is a full-stack AI application containerized via **Docker**.

* **Frontend**: Streamlit-based web application for data interaction and prediction visualization.
* **Backend**: **PostgreSQL** for persistent prediction logging and **psycopg3** for database management.
* **Intelligence Layer**: Gemini 2.5 Flash API for reasoning; **RAG** (Retrieval-Augmented Generation) using TF-IDF for project context retrieval.
* **Deployment**: **Telegram Bot** integration for real-time mobile decision support.
---

## Usage

1. **Environment Setup**: Define `GEMINI_API_KEY` and `TELEGRAM_BOT_TOKEN` in a `.env` file.
2. **Database**: Configure PostgreSQL credentials.
3. **Run Application**:
   ```bash
   docker-compose up --build

---

The Team

Bikesh Adhikari   
Venkata Satya Sreeya Chandrapati   
Fiyinfoluwa Seinde-Olaniyi
Sai Tarun Gaddam   

Mentorship: Professor Erol Ozkan, University of Texas at Arlington.

Data Source & License
This project utilizes public records from the Dallas OpenData portal (FY 2022-2023). All code is provided under the MIT License.
