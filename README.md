
## Table of Contents
- [Overview](#overview)
- [Project Structure](#project-structure)
- [Key Findings](#key-findings)
- [Feature Importance](#feature-importance-for-modeling)
- [Setup Instructions](#setup-instructions)
- [Next Steps](#next-steps)


# Fraud Detection Project

## Overview
End-to-end fraud detection system using Databricks medallion architecture (Bronze → Silver → Gold) with comprehensive exploratory data analysis.

## Project Structure

### Notebooks
- **fraud_bronze_ingestion.ipynb** - Raw data ingestion (5 tables)
- **fraud_silver_transformation.ipynb** - Data cleaning & geographic categorization (6 tables)
- **fraud_gold_build.ipynb** - Analytics-ready tables (2 tables)
- **fraud_eda_day1.ipynb** - Comprehensive EDA (66 cells, 10 sections)

### Data Schema
**Catalog:** `workspace`  
**Schema:** `fraud`

**Bronze Layer:** Raw data (5 tables)
**Silver Layer:** Cleaned data (6 tables)
**Gold Layer:** Analytics-ready (2 tables)
**Volume:** `raw` - Source data files

## Key Findings

### High-Risk Patterns
- **Cross-border transactions:** 43x higher fraud rate (4.85% vs 0.11%)
- **Online transactions:** 53x higher fraud rate than physical (0.84% vs 0.016%)
- **Italy:** 65% fraud rate, accounts for 23% of all fraud cases
- **Haiti:** 95.8% fraud rate (low volume outlier)

### Temporal Patterns
- **Online fraud peaks:** 10 AM - 1 PM (1.80% fraud rate)
- **Physical fraud peaks:** 6 PM - 7 PM (0.13% fraud rate)
- **Seasonal effect:** Minimal (1.04x), December and August slightly higher

### Dataset Characteristics
- **Total transactions:** 8.9M (training) + 4.4M (scoring)
- **Fraud rate:** 0.15% (severe class imbalance 1:668)
- **Time period:** 2010-2019 (10 years)
- **Geography:** US-based synthetic data with international transactions
- **Features:** 37 columns (transactions, users, cards, merchants)

## Feature Importance for Modeling

### Tier 1 (Critical)
- `is_cross_border` - 43x fraud rate difference
- `location_type` - International vs US vs Online
- `merchant_state` - Italy, Haiti high-risk
- `hour_x_type` - Time + transaction type interaction

### Tier 2 (Important)
- `card_on_dark_web` - Strong fraud indicator
- `mcc` / `mcc_description` - High-risk merchant categories
- `amount` - Fraud avg 2.6x higher
- `use_chip` - Chip vs swipe patterns

### Tier 3 (Moderate)
- `hour_of_day`, `day_of_week` - Temporal patterns
- `credit_score`, `yearly_income` - Demographics

## Setup Instructions

### Prerequisites
- Databricks workspace access
- GitHub account
- Git configured in Databricks

### Getting Started
1. Accept GitHub invitation
2. Configure Git in Databricks (Settings → Linked accounts)
3. Clone this repository to your Databricks workspace
4. Verify access: `SELECT * FROM workspace.fraud.tx_train_gold LIMIT 10`

### Collaboration Workflow
1. Create feature branch (`yourname-feature`)
2. Make changes in your workspace
3. Commit and push to GitHub
4. Create pull request for review
5. Merge after approval
6. Pull latest changes regularly

## Next Steps
- [ ] Model development (Random Forest, XGBoost, LightGBM)
- [ ] Feature engineering (`hour_x_type`, `is_business_hours`, time buckets)
- [ ] Address class imbalance (SMOTE, class weights)
- [ ] Model evaluation (Precision, Recall, F1, AUC-ROC)
- [ ] Production deployment

## Team
- Cathy, Felicia, Hailey, Han, Zoey
