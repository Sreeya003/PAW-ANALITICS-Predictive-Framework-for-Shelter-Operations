# PAW-ANALITICS: From Intake to Outcome 🐾

**A Machine Learning Framework for Predicting Shelter Decisions and Length of Stay (LOS)**

[cite_start]PAW-ANALITICS is an end-to-end predictive operations system developed using the **Dallas Animal Shelter** public dataset (FY 2022-2023)[cite: 55]. [cite_start]This project addresses critical shelter challenges—specifically overcrowding and resource misallocation—by providing staff with real-time, interpretable AI briefings[cite: 27, 28].

---

## Key Features

* [cite_start]**Dual-Model Pipeline**: Combines classification for outcome prediction and regression for stay duration[cite: 16].
* [cite_start]**Agentic AI Layer**: Utilizes **Gemini 2.5 Flash** to translate raw model probabilities into actionable natural language staff briefings[cite: 23, 448, 470].
* [cite_start]**Real-time Decision Support**: Integration with a **Telegram Bot** for mobile alerts and a **Streamlit** dashboard for historical exploration[cite: 85, 452].
* [cite_start]**Transparent Logic**: Implements **SHAP** analysis to explain the "why" behind every prediction[cite: 77, 317].

---

## Technical Deep Dive

### 1. Exploratory Data Analysis (EDA)
[cite_start]We processed over **34,800 observations** using **Power BI** to uncover operational trends[cite: 56, 84].
* **Outcome Distribution**: Adoption is the most frequent outcome (~25%), followed by Euthanasia (~22%).
* **Species Variance**: Stay durations vary significantly by animal type; livestock average the longest stays (~18 days), while wildlife has the shortest (~3 days).
* [cite_start]**Skewness**: Length of Stay (LOS) is highly right-skewed, requiring target transformation for effective modeling[cite: 90].

### 2. Machine Learning Stack
* **Classification (Live vs. Non-Live)**: 
    * [cite_start]**Winner**: **Random Forest** (Selected over Logistic Regression and CatBoost)[cite: 212].
    * **Performance**: Achieved a **0.915 ROC-AUC** and **84% Accuracy** on the held-out test set.
* **Regression (Length of Stay)**: 
    * [cite_start]**Winner**: **XGBoost Regressor**[cite: 288].
    * [cite_start]**Performance**: Achieved a Mean Absolute Error (MAE) of **5.56 days** using a $log(1+LOS)$ target transformation to handle skewness[cite: 294, 314].

### 3. Feature Engineering & Selection
* [cite_start]**Feature Engineering**: Transformed 33 raw columns into 13 optimized model features, including engineered datetime predictors like "Weekend Indicator"[cite: 64, 148].
* [cite_start]**Data Leakage Mitigation**: A critical fix was implemented to remove outcome-related variables, correcting the baseline ROC-AUC from a biased 0.96 to a realistic 0.86[cite: 151, 186].

---

## Architecture

[cite_start]The solution is a full-stack AI application containerized via **Docker**[cite: 431].

* [cite_start]**Frontend**: Streamlit-based web application for data interaction and prediction visualization[cite: 430].
* [cite_start]**Backend**: **PostgreSQL** for persistent prediction logging and **psycopg3** for database management[cite: 454, 461].
* **Intelligence Layer**: Gemini 2.5 Flash API for reasoning; [cite_start]**RAG** (Retrieval-Augmented Generation) using TF-IDF for project context retrieval[cite: 456, 458].
* [cite_start]**Deployment**: **Telegram Bot** integration for real-time mobile decision support[cite: 452, 455].

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
