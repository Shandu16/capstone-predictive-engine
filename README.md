# capstone-predictive-engine
Predictive activation engine to optimize the STADIOEquities onboarding funnel.

## Project Overview
This repository contains the data, code, and experimental results for the STADIOEquities activation funnel optimization project. The objective of this study is to predict the likelihood of new platform users making their first deposit, identifying key behavioural friction points to inform targeted onboarding interventions.

## Repository Structure
This repository is organized to separate data, experimental setups, and modular code scripts as follows:

* **`/data`**: Contains the datasets used for training and testing. *(Note: Raw client data is `.gitignore`d for privacy; synthetic/anonymized samples are provided here).*
* **`/models`**: Houses serialized, trained machine learning models resulting from the experiments. 
* **`/experiments`**: Contains the **Experimental Setup**, including Jupyter notebooks detailing the exploratory data analysis, feature engineering, and model training pipelines.
* **`/results`**: Contains the **Experimental Results**, including performance metrics (accuracy, F1-score, ROC-AUC), classification reports, and cross-validation logs.
* **`/scripts`**: Contains modular Python scripts to support the main experiments:
    * `stats_helpers.py`: **Statistical helper and comparison scripts** for testing feature significance and evaluating model distributions.
    * `visualizations.py`: **Visualisation scripts** for rendering funnel drop-offs, feature importance charts, and correlation matrices.

## Tools & Libraries
* Python 
* Pandas & NumPy (Data manipulation)
* Scikit-learn (Machine learning & predictive modeling)
* Matplotlib & Seaborn (Data visualization)

## Setup Instructions
1. Clone the repository: `git clone [Your-Repo-Link-Here]`
2. Install the required dependencies: `pip install -r requirements.txt`
3. Run the initial data processing notebook located in `/experiments`.

#MOTIVATION

By quickly growing to 2.3 million registered accounts, STADIOEquities has effectively eliminated the conventional obstacles to retail investment. However, a growing "activation gap" between account registration and initial investment poses a serious structural danger to the platform's fundamental business model. In the last two years, sign-up to first-deposit conversion rate has declined from 64% to 59%. On the other hand, 41% of all registered accounts remained inactive. Additionally, in the first 6 months of onboarding, early account dormancy increased to 31%.  

An inactive account earns zero revenue while still incurring operating and regulatory costs because the platform's revenue is solely dependent on funded activity, notably assets under management (38%), brokerage fees (29%), and interest margins (17%). 

This issue has a serious financial impact. The 41% of accounts that are still vacant amount to hundreds of millions of Rands in lost marketing expenditures, considering the R180 cost of acquiring each new user. According to the briefing data, onboarding abandonment is concentrated around particular behaviors, acquisition channels, and KYC friction points rather than occurring randomly. However, the fixed-schedule, "one-size-fits-all" communication approach used in current interventions ignores the various reasons why users stall. The board's main 2030 strategic goal, "Activate the accounts that are already present," is precisely aligned with fixing this inefficiency, which is crucial for long-term growth. 

This initiative is crucial because it bases our knowledge of user attrition on actual data rather than conjecture. It offers insight into the precise causes of squandered acquisition expenditures, pinpointing the areas where the most promising customers are lost. It shows exactly when and why users leave the funnel by substituting unambiguous behavioral cues for conjecture. The activation funnel won't be automatically fixed by this project, but it will offer the fundamental analysis needed to do so.  

This study will identify the specific friction points leading to desertion by examining past app behavior, KYC progression, and funding delays. In the end, these results will assist data-driven decisions to increase the R180 cost-recovery rate and create a more engaged clientele by giving product leadership and marketing teams the evidence they need to create focused, context-aware onboarding interventions.

# PROBLEM STATEMENT

During the client onboarding lifecycle, STADIOEquities encounters a significant income bottleneck: 41% of its 2.3 million registered users do not make a first deposit, resulting in hundreds of millions of Rands in unrecovered acquisition costs (at R180 per user). Because unfilled accounts earn no platform or brokerage fees while continuing to incur continuous regulatory and operational costs, this activation gap effectively undermines the firm's primary economic model.  

The specific, individual-level behavioral triggers and friction points that precede departure are unclear, despite leadership monitoring macro-level drop-off measures, such as a decrease in sign-up-to-deposit conversion from 64% to 59% over the previous two years. Product and marketing teams are forced to rely on a generic, fixed-schedule intervention strategy that fails to meet a variety of user demands since the company is currently unable to differentiate between a user who needs more time and one who is permanently stalled.  

Thankfully, STADIOEquities has up to six years of clean, digital-native data that includes demographic profiles, acquisition channels, KYC process timestamps, and granular app and online session habits. The goal of this research is to find the multivariate drivers of onboarding abandonment by mining this historical dataset. The company needs to shift from speculative, one-size-fits-all communications to evidence-based insights, which is why this study is essential. This research will help design the focused, real-time interventions required to dramatically enhance the 59% baseline activation rate and create a sustainable, revenue-generating client base by identifying precisely which behavioral sequences predict a failure to pay. 

## RAAIDD log
# RISKS
Data Privacy: POPIA compliance restrictions may delay access to granular user demographic data.
Class Imbalance: With 41% of accounts unfunded, models may become biased toward predicting failure.
Concept Drift: Historical user behavior from 4 years ago may no longer accurately represent new, younger investors.
If the model's precision is low, it could trigger too many false-positive interventions, overwhelming clients.

# Actions
Extract, clean, and anonymize the last 4-6 years of app session, KYC, and funding data.
Engineer behavioral features, specifically calculating time spent on each KYC step and session durations.
Train and tune machine learning classification models (e.g., Random Forest, XGBoost).
Design an A/B testing framework to measure the impact of model-driven interventions against the current fixed-schedule emails.

# Assumptions
The behavioral friction markers that caused drop-offs in the past will remain reliable predictors for future users.
The R180 Customer Acquisition Cost (CAC) will remain relatively stable over the project lifecycle.
Users who stall during KYC do so because of UI friction or confusion, rather than simply not having money to deposit.
The marketing and engineering teams have the technical capability to integrate real-time API triggers based on the model's output.
 
# Issues 
Client identities currently span isolated app, web, and marketing databases, requiring immediate, complex data engineering to establish a single unified client_id before modeling can begin.

# Decisions
The analytical scope is strictly limited to predicting the first deposit ("activation gap"), specifically excluding long-term portfolio churn or premium tier upselling.

# Dependencies 
Feature engineering is entirely dependent on successfully joining the behavioral dataset with the marketing/acquisition dataset.
Designing targeted onboarding interventions depends on achieving a high ROC-AUC score on the final classification model.
Deployment of real-time nudges depends on strict approval from the STADIOEquities compliance and risk teams.
The initial exploratory data analysis (EDA) phase depends on the IT department providing timely access to the secure data warehouse.
