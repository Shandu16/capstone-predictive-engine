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
