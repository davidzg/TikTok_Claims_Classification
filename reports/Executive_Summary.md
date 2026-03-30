# 🛡️ TikTok Claims Classification: Executive Summary
Status: Ready for Production Implementation

Objective: Develop a machine learning system to categorize user-generated content as "claims" or "opinions" to prioritize high-risk videos for human moderation.

## The Problem
TikTok faces a massive volume of daily uploads, making manual review of every video impossible. Misinformation is more likely to be spread through "claims" than "opinions", yet the current moderation queue is undifferentiated.

- High Resource Strain: Without a filter, moderators spend ~50% of their time reviewing "opinion" videos that do not require fact-checking.

- Engagement as a Risk Factor: Our analysis shows that "claim" videos generate significantly higher engagement (views and shares) than opinions, meaning misinformation spreads faster than it can currently be flagged.

- The Identification Gap: Human-only moderation cannot keep pace with the 50/30/20 split of claims, opinions, and unverified content without technical assistance.

## The Insight
The most powerful predictor of whether a video is a "claim" is not actually what is said (the text), but how the audience reacts to it (the metrics).
- Behavior Over Text: While we utilized Natural Language Processing (CountVectorizer), the model found that video_view_count, video_like_count, and video_share_count were the dominant indicators of a claim.

- Recall is King: In this business context, a "False Negative" (letting a claim slip through as an opinion) is a high-risk failure. Our Random Forest Champion Model was specifically tuned for high recall to ensure maximum platform safety.

## Strategic Recommendations
To transform these findings into a functional moderation shield, I recommend the following:

- Automated Queue Prioritization: Implement the Random Forest model to "de-prioritize" videos predicted as opinions. This will effectively double the moderation team's capacity to review potential misinformation.

- Threshold-Based Alerts: Since engagement is the top predictor, set "Velocity Triggers." Any video that exceeds a specific view-to-like ratio should be auto-flagged for the "Claim" queue regardless of content.

- Banned Author Watchlist: Our EDA revealed that "Banned" authors see higher engagement-per-view on claims. These accounts should be subject to a stricter classification threshold in the model.

## Business Impact
By deploying this classification system, TikTok can achieve a 50% increase in moderation efficiency by removing low-risk "opinion" content from the priority queue. This ensures that human moderators spend their time where they are most needed, significantly reducing the "Time-to-Action" for high-velocity misinformation.