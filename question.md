# Instructions

Below are a set of questions in relation to the churn prediction task. Please do your best to answer them and don't be afraid to add detail to your responses.

# Questions

1. The client uses Snowflake for storing a majority of their customer data. They wish to use the churn predictive model to make daily predictions on their customers and use derived output tables in Snowflake to build dashboards in Tableau for end-user interaction and wider stakeholder reporting. What would you recommend for deploying the model you have built / will build?

a. We will create a pipeline that will extract the data from Snowflake, then process the data using our model for prediction before loading the predictions back into Snowflake (can be done using Astro Cloud IDE). Using Astro Cloud IDE we can schedule the model. This will allow us to set a daily schedule (using Apache Airflow) that pulls the snowflake data before using our model to generate a daily churn predicition dtaa which can then be written back into snowflake. Once we have the data in snowflake we can do some transformation using SQL or Snowpark for more advanced situations. This will ensure our data is prepared for use within Tableau.

Connect Tableau to Snowflake and set up dashboards to visualize the output tables with churn predictions and insights.

2. The client is cautious of needing to maintain the model after project completion. In particular, they are worried the model will gradually lose predictive capability due to changes in data over time. What systems and processes do you recommend implementing to support model maintenance? How can the client retain their confidence in the model and its outputs?

a.
 - Model Monitoring: Implement a monitoring system to track model performance metrics such as accuracy, precision, recall, and AUC. We need to also monitor drift in model inputs and predictions over time.
 - Data Quality Checks: Establish automated data quality checks to ensure the model is fed high-quality, relevant data. E.g. we are missing a lot of data that would boost our model performance.
 - Re-Training Pipeline: Next we need to setup an automated pipeline for periodic re-training of the model with new data, which can help the model adapt to changes over time.
 - Changing the type of algorithm we use could also help determine if our model has been behaving as well as we had hoped. Maybe using A/B testing to find out what model is the best .
 - We need to ensure we have measures for model versions. Just to ensure we can role back model iterations.
 - Documentation and training: This isimportant as it helps future collegues understand the current process and ways to imporove on it.

3. During the delivery of the churn prediction project you will need to provide progress updates on model development. How would you seek to validate the model performance from a development perspective, and how would you use these results to inform wider non-technical stakeholders?

a. 
 - In our model we used cross validation to assess the models performance across different subsets of the data.
 - We evaluated the model using relevant metrics e.g. accracy, prevision, recall F1-score and more.
 - We analysed the feature importance metrics
 - Next steps would be to do model diagnostics to assess model performance.

 During the churn prediction project, regular progress updates will be provided at key milestones, including the completion of data preprocessing, model training, and validation phases. To ensure clarity for non-technical stakeholders, technical metrics will be translated into business-oriented outcomes, such as the projected increase in customer retention rates. Model performance will be depicted through easy-to-understand charts and graphs.The significance of influential features will be conveyed by showing how customer behavior patterns may influence churn, thereby tying model developments to core business goals like revenue growth and customer satisfaction. To keep developing the model we will also note to stakeholders potential risks and data limitations whilst providing possible solutions.


4. The client is investing in capturing more data points on their customers with the intention of using this new data in the model at some point in the near future. What recommendations would you make to the client in regards to including these new features? For context, they have limited expertise in machine learning, but do have resource in business analytics and analytics engineering.

a.
Document the process and impact of adding new features, and provide training for the BA & Analytical Engeering team on how to implement new Features and interpreting machine learning model outputs. We will also have to document how to retrain the model with the new data. Engage the business analytics team to analyze the new features with respect to the business context. They should look for trends, correlations, and potential insights that could inform the model's predictive capability. Start by incrementally adding new features to the model. This allows for the monitoring of the impact each feature has on the model's performance. Once this has been done it is important to implement a model explainability tool and technique for stakeholders to better understand how the new features are influencing predictions. We will need to develop a monitoring system to detect concept drift over time as new data, this will help the BAs and Analytical Engineers to understand how the new data is affecting the data. All in all a seemless way that can adjust with new data with little modifications by the BA and AE team would be the ideal method. Note to provide to the team is to ensure that before integrating new data, they need to conduct a thorough assessment to understand the datas relevance, quality, and potential impact on the model. Ensure that the data collected is accurate, clean, and formatted correctly. Lastly the new data needs to follow legal and ethical considerations.