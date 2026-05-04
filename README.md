# AI-Powered Telecom Customer Retention Platform

An integrated AI system that combines statistical analysis, machine learning, risk-adjusted CLV, and an agentic retention advisor to predict and prevent telecom customer churn.

## Project Overview

This is Project 7 (Industry Integrated AI Systems Synthesis) for the AI Master's program at Udacity / Woolf University. It integrates methods from three prior capstone projects into an end-to-end pipeline:

1. **Statistical Analysis** (from P2) - Chi-squared test and Welch's t-test validate that churn patterns are statistically significant
2. **ML Churn Prediction** (from P3) - Logistic Regression and Random Forest predict individual churn probabilities
3. **Risk-Adjusted CLV** (new) - Combines ML probabilities with revenue data to produce risk-aware customer valuations
4. **Agentic Retention Advisor** (from P6) - ReAct agent with OpenAI function calling recommends personalized retention actions

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
source .venv/bin/activate
jupyter notebook retention_system.ipynb
```

Run all cells top-to-bottom. The agent section makes real API calls to OpenAI (gpt-4o-mini, ~$0.03 total cost).

## Dataset

The Telco Customer Churn dataset (7,043 rows, 21 columns) is included in `dataset/`. It contains customer demographics, service subscriptions, contract details, and churn labels. Originally from the IBM Watson Analytics sample datasets.

## System Architecture

```
Telco Dataset -> Statistical Analysis -> ML Churn Prediction -> Risk-Adjusted CLV -> Agentic Retention Advisor -> Output
```

The agentic advisor uses 5 tools (lookup profile, assess risk, calculate CLV, lookup policy, recommend action) and 4 safeguards (confidence threshold, iteration limit, minimum-service guarantee, high-CLV escalation).

## Bias Awareness

The dataset contains demographic features (gender, senior citizen status) that could introduce bias if used carelessly. These features are included in the ML model for prediction accuracy but should be excluded from retention decision-making to prevent discriminatory outcomes. The agent's policy database ensures all customers receive at least a minimum-service outreach regardless of predicted value.

## Dependencies

See `pyproject.toml` for dependency definitions. Key packages: pandas, scikit-learn, scipy, matplotlib, seaborn, openai, python-dotenv.
