# TikTok Claims Classification: Mitigating Misinformation

## Project Overview
The goal of this project is to build a machine learning model that helps TikTok identify if a video is a "claim" or an "opinion". By finding claims accurately, the platform can prioritize them for human review and stop misinformation faster.

**[Read the Executive Summary for Stakeholders](reports/Executive_Summary.md)**

## Project Workflow
### 1. Exploratory Data Analysis (EDA) & Data Cleaning
Notebook: [01_Exploratory_Data_Analysis.ipynb](01_Exploratory_Data_Analysis.ipynb)

I analyzed about 19,000 videos to see how engagement metrics (likes, views, shares) relate to the claim status.

**Key Findings:**
* The dataset is balanced with about 50.3% claims and 49.7% opinions.
* Engagement is the most important predictor because claim videos get much higher views and likes than opinion videos.
* Authors with a "Banned" status show higher engagement for every view when they post a claim.

<p align="center">
  <img src="images/view_count_by_claim_status.png" alt="View count by claim status" width="46.5%">
  <img src="images/view_count_by_ban_status.png" alt="View count by ban status" width="49%">
</p>


### 2. Feature Engineering & Machine Learning
Notebook: [02_Machine_Learning_Classifier_vectorized.ipynb](02_Machine_Learning_Classifier_vectorized.ipynb)

I built a classification model to automate how TikTok detects claims.

**Modeling Strategy:**
* I created new features by measuring transcription text length and used CountVectorizer to turn words into numbers.
* I split the data into 60% training, 20% validation, and 20% testing sets.
* I built and compared two models: Random Forest and XGBoost.
* After comparing their performance against the validation data, I selected the best-fitting model as the "champion".
* Finally, I ran this champion model against the unseen test data to confirm its real-world performance.

**Results:**
* The Random Forest model was chosen as the champion model.
* The model achieved high recall to avoid missing claims, as missing a claim is worse than accidentally flagging an opinion.
* Engagement metrics were the strongest predictors, while the transcription text was less helpful for the model.

<p align="center">
  <img src="images/cm_rf_test.png" alt="alt text">
</p>

## Tech Stack
* Languages: Python (Pandas, NumPy)
* Frameworks: Scikit-Learn, XGBoost
* NLP Tools: CountVectorizer and Text Length Extraction
* Validation: 60/20/20 Train/Validation/Test split
* To run this notebook locally, please refer to the [requirements.txt](requirements.txt) for environment dependencies.

## Key Insights for Stakeholders
* High engagement (lots of views and shares) is the biggest "red flag" for a claim.
* This model makes the team more efficient by correctly identifying nearly half of the content as "opinions".

## Strategic Recommendations
* Move all videos predicted as "opinions" to a low-priority queue to save moderator time.
* Use "High-Engagement Triggers" to flag any video that starts to go viral very quickly.
* In the future, we should try sentiment analysis to see if the tone of the video helps improve the model.