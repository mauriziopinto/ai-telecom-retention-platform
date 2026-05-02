# Project 7 — Implementation Progress

**Started:** May 2, 2026

---

## Phase 1: Project Setup & Data Loading — COMPLETE

- [x] uv init + venv + dependencies (jupyter, numpy, pandas, matplotlib, seaborn, scipy, scikit-learn, openai, python-dotenv)
- [x] .gitignore created (standard Python/Jupyter + .env + report drafts)
- [x] .env with OPENAI_API_KEY
- [x] Telco dataset copied from P3 (7,043 rows, 21 columns)
- [x] Git repo initialized (main + dev branches)
- [x] Notebook created: retention_system.ipynb (title, setup, data loading, inspection)
- [x] Notebook executes without errors
- [x] Class distribution verified: No Churn 5,174 (73.5%), Churn 1,869 (26.5%)

## Phase 2: Statistical Analysis (Component 1) — COMPLETE

- [x] Chi-squared test: Contract type vs. Churn — χ²=1184.60, p=5.86e-258 (significant)
- [x] Churn rates by contract: Month-to-month 42.7%, One year 11.3%, Two year 2.8%
- [x] Welch's t-test: MonthlyCharges by Churn — t=18.41, p=8.59e-73 (significant)
- [x] Churners mean=$74.44 vs. non-churners mean=$61.27
- [x] Assumption checks: Shapiro-Wilk (non-normal), Levene (unequal variance) → Welch's appropriate
- [x] Descriptive stats by Contract, InternetService, PaymentMethod
- [x] Visualization 1: Churn rate by contract type (bar chart)
- [x] Visualization 2: MonthlyCharges by churn group (box plot)
- [x] Visualization 3: Churn rate heatmap (InternetService × Contract)
- [x] Committed to dev branch

## Phase 3: ML Churn Prediction (Component 2) — COMPLETE

- [x] Preprocessing pipeline: drop customerID, convert TotalCharges, binary/multi-class encoding, stratified split, scaling
- [x] 30 features after encoding; train=5,634, test=1,409; churn rate 26.5% preserved in both sets
- [x] Logistic Regression trained (max_iter=1000, random_state=42)
- [x] Random Forest trained (n_estimators=100, random_state=42)
- [x] LR accuracy=0.806, precision=0.657, recall=0.559, F1=0.604
- [x] RF accuracy=0.787, precision=0.628, recall=0.487, F1=0.548
- [x] LR outperforms RF (consistent with P3)
- [x] predict_proba extracted for all 7,043 customers (mean=0.266, min=0.002, max=0.855)
- [x] Confusion matrices visualized (LR + RF side-by-side)
- [x] Feature importance chart (top 10 from RF)
- [x] Calibration assessment: predicted vs. observed rates track closely across all deciles
- [x] Committed to dev branch

## Phase 4: Risk-Adjusted CLV (Component 3) — COMPLETE

- [x] Simple CLV = MonthlyCharges × tenure (mean $2,279.58)
- [x] Expected CLV = MonthlyCharges / churn_probability (mean $1,011.28)
- [x] CLV by segment: Two-year mean=$2,889.99, Month-to-month mean=$197.10
- [x] Top-10 rank comparison: 0 overlap between simple vs. expected CLV rankings
- [x] Scatter plot: churn_probability vs. expected CLV, colored by MonthlyCharges tier
- [x] Key finding: low-risk customers mean CLV=$2,308.43 vs. high-risk $125.94
- [x] Committed to dev branch

## Phase 5: Agentic Retention Advisor (Component 4) — COMPLETE

- [x] OpenAI client setup with gpt-4o-mini
- [x] Agent config dict: model, confidence_threshold=0.7, max_iterations=10, valid_actions
- [x] Retention policy database: 6 categories (price_sensitivity, contract_lock_in, service_quality, loyalty_reward, low_engagement, minimum_service)
- [x] 5 tool functions: lookup_customer_profile, assess_churn_risk, calculate_clv, lookup_retention_policy, recommend_action
- [x] 5 OpenAI tool schemas with enums for constrained parameters
- [x] System prompt (retention advisor persona with decision guidelines)
- [x] ReAct agent loop: analyze_retention(customer_id, verbose=True)
- [x] 4 safeguards: iteration limit, confidence threshold, minimum-service guarantee, high-CLV+high-risk escalation
- [x] Quick test: customer 7590-VHVEG → retain action, contract_lock_in, confidence 0.85, 4 iterations, no safeguards triggered
- [x] Committed to dev branch

## Phase 6: Test Cases, Demo & Evaluation — PENDING

## Phase 7: Documentation & Repo Finalization — PENDING

## Phase 8: Reflective Synthesis Paper — PENDING
