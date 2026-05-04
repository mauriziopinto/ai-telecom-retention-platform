# AI-Powered Telecom Customer Retention Platform

An integrated AI system that combines statistical analysis, machine learning, risk-adjusted Customer Lifetime Value (CLV), and an agentic retention advisor to predict and prevent telecom customer churn. CLV estimates the total revenue a business can expect from a customer over the duration of their relationship. In this system, CLV is adjusted by the predicted churn probability so that high-risk customers are valued differently than stable ones, changing how the business prioritizes retention efforts.

## Project Overview

This is Project 7 (Industry Integrated AI Systems Synthesis) for the AI Master's program at Udacity / Woolf University. It integrates methods from three prior capstone projects into an end-to-end pipeline:

1. **Statistical Analysis** (from Project 2) - Chi-squared test and Welch's t-test validate that churn patterns are statistically significant
2. **ML Churn Prediction** (from Project 3) - Logistic Regression and Random Forest predict individual churn probabilities
3. **Risk-Adjusted CLV** (new) - Combines ML probabilities with revenue data to produce risk-aware customer valuations
4. **Agentic Retention Advisor** (from Project 6) - ReAct agent with OpenAI function calling recommends personalized retention actions

## Setup

```bash
# Clone the repository
git clone https://github.com/mauriziopinto/ai-telecom-retention-platform.git
cd ai-telecom-retention-platform

# Create virtual environment and install dependencies
uv venv
source .venv/bin/activate
uv sync

# Add your OpenAI API key
echo "OPENAI_API_KEY=your-key-here" > .env
```

## Running the Notebook

```bash
# Activate the environment (if not already active)
source .venv/bin/activate
jupyter notebook retention_system.ipynb
```

Run all cells top-to-bottom. The agent section makes real API calls to OpenAI (gpt-4o-mini, ~$0.03 total cost).

## Dataset

The Telco Customer Churn dataset (7,043 rows, 21 columns) is included in `dataset/`. It contains customer demographics, service subscriptions, contract details, and churn labels for a fictional telecommunications company.

**Source:** IBM Cognos Analytics sample data module. Available at:
- IBM Documentation: https://www.ibm.com/docs/en/cognos-analytics/12.1.x?topic=samples-telco-customer-churn
- Kaggle mirror: https://www.kaggle.com/datasets/blastchar/telco-customer-churn

**License:** Apache License 2.0. See https://github.com/IBM/telco-customer-churn-on-icp4d/blob/master/LICENSE for full terms.

## System Architecture

```
            Telco Customer Data
                    │
                    ▼
         Statistical Analysis
      (from Capstone Project 2)
      Chi-squared, Welch's t-test
                    │
                    ▼
          ML Churn Prediction
      (from Capstone Project 3)
      Logistic Regression + RF
                    │
                    ▼
       Risk-Adjusted CLV Score
       MonthlyCharges / churn_prob
                    │
                    ▼
    Agentic Retention Advisor
      (from Capstone Project 6)
    ReAct loop, 5 tools, 4 safeguards
                    │
                    ▼
           Retention Action
       retain / escalate / monitor
```

### Prior Capstone Projects Integrated

| Project | Contribution | Repository |
|---------|-------------|------------|
| Project 2 — Statistical Analysis | Hypothesis testing framework (chi-squared, Welch's t-test) | [statistical-analysis-project](https://github.com/mauriziopinto/statistical-analysis-project) |
| Project 3 — ML Model Design | Churn prediction pipeline (Logistic Regression, Random Forest) | [ml-churn-project](https://github.com/mauriziopinto/ml-churn-project) |
| Project 6 — Agentic AI Systems | ReAct agent architecture, tool calling, safeguards | [agentic-moderation-system](https://github.com/mauriziopinto/agentic-moderation-system) |

The agentic advisor uses 5 tools (lookup profile, assess risk, calculate CLV, lookup policy, recommend action) and 4 safeguards (confidence threshold, iteration limit, minimum-service guarantee, high-CLV escalation).

## Bias Awareness

The dataset contains demographic features (gender, senior citizen status) that could introduce bias if used carelessly. These features are included in the ML model for prediction accuracy but should be excluded from retention decision-making to prevent discriminatory outcomes. The agent's policy database ensures all customers receive at least a minimum-service outreach regardless of predicted value.

## Dependencies

See `pyproject.toml` for dependency definitions. Key packages: pandas, scikit-learn, scipy, matplotlib, seaborn, openai, python-dotenv.
