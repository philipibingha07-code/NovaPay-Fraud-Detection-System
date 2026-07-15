**An end-to-end fraud detection system that combines exploratory data analysis, feature engineering, machine learning, and business intelligence to identify fraudulent cross-border transactions in real time**.

### Table Of Content


### Project Overview
**Financial institutions process thousands of cross-border transactions every day, making fraud detection one of the most critical challenges in modern fintech**. 
    **This project simulates a production fraud detection workflow for NovaPay, a fictional international remittance platform operating across the United States, Canada, and the United Kingdom, supporting 9 currencies and multiple transaction channels**.
    **The objective was to develop a machine learning solution capable of detecting fraudulent transactions with high precision and recall while minimizing false positives and supporting faster fraud investigations**.

### Business Overview
- **Global exposure — remittances move across multiple currencies and corridors, each with its own risk profile**
- **Multi-channel risk — transactions arrive via web, mobile, and ATM, each with different fraud signatures and device trust levels**
- **Cost of missed fraud — undetected fraud drives direct financial loss, chargebacks, and regulatory exposure under KYC obligation**

### Dataset
- **11,200 transactions, 26 raw features, 9 currencies, 3 channels**
- **Target: is_fraud (binary classification)**
- **Feature groups: identity & context, transaction details, device & network signals, behavioral/risk indicators**

### Data Cleaning & Feature Engineerin9
- **Imputed missing values (FX-recomputation, median/mode imputation, column means) across ~300 affected rows per field**
- **Standardized inconsistent categorical labels (channel, KYC tier, country codes)**
- **Extracted time-based features (year, month, hour, day-of-week, weekend flag) from timestamps**
- **Binned account age, transaction amount, and IP risk score into interpretable tiers**
- **Label-encoded categorical fields and scaled 12 numeric columns**

### Key Findings
#### Transaction Velocitu
**accounts performing four or more transactions within a 24-hour period exhibited dramatically higher fraud rates than lower-activity accounts.**

### Devive Trust Score
**Low device trust scores strongly correlated with fraudulent transactions, making device reputation one of the most influential predictors**
#### Account Days
**New accounts carry outsized risk. Accounts under 90 days old account for the large majority of fraud; risk falls below 2% after 90 days**.

**Mid-size transfers are the highest-risk band. Fraud rates peak at 94% in the $2K–$5K range, then drop for transfers over $5K (likely due to stricter manual KYC review at high amounts**.

**Web is the highest-risk channel despite mobile carrying the most overall volume**.

### Modeling Approach
Encode — label-encoded 10 categorical fields
Scale — StandardScaler applied to 12 numeric columns
Balance — SMOTE to correct severe class imbalance (fraud was ~11.9% of raw transactions)
Split — 80/20 train-test split (16,075 train / 4,019 test rows)

### Machine Learning Pipeline
| Model               | Accuracy | Precision |  Recall | F1 Score |
| ------------------- | -------: | --------: | ------: | -------: |
| **Random Forest**   |  **99%** |  **100%** | **98%** |  **99%** |
| XGBoost             |      99% |      100% |     98% |      99% |
| Gradient Boosting   |      97% |      100% |     95% |      97% |
| Decision Tree       |      97% |       97% |     97% |      97% |
| KNN                 |      96% |       93% |    100% |      96% |
| AdaBoost            |      95% |       97% |     92% |      95% |
| Logistic Regression |      93% |       96% |     88% |      92% |
| SVM                 |      92% |       99% |     85% |      92% |

### Final Model
**Random Forest was selected as the final model — tied with XGBoost on accuracy, but chosen for interpretability, native feature importances, and lower tuning complexity in production**.
**The model achieved excellent fraud detection performance while maintaining a very low false-positive rate**.

### Business Recommendations
- ##### Velocity-based real-time holds — auto-flag accounts with 4+ transactions in a rolling 24h window for step-up verification
- #### Weight device & IP trust higher — route low-trust devices or high-risk IPs (score > 0.7) to manual review
- #### ighten controls for new accounts — apply lower limits and extra checks for accounts under 90 days old
- #### Extra scrutiny at $1K–$5K — this band shows the highest fraud concentration
- #### Monitor the early-morning window — fraud rate is roughly 3x baseline between 4am–8am
- #### Deploy the Random Forest model as a real-time pre-authorization risk score in the transaction pipeline

  ### Repository Structure
 **novapay-fraud-detection**
│   └── **NovaPay_Fraud_Detection_Presentation.pdf**   # Full slide deck
├── images/[NovaPay_Fraud_Detection(1). saveed.pdf](https://github.com/user-attachments/files/30050395/NovaPay_Fraud_Detection.1.saveed.pdf)

│   └── dashboard.png                              # Tableau dashboard
└── notebook/                                       # Add your Jupyter notebook / scripts here
  




