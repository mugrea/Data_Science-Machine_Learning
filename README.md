# PREDICTING HEART DISEASE..
# Motivation for choosing the project.
According to the World Health Organization, non-communicable diseases (NCDs), including cardiovascular diseases (heart disease), account for approximately 36% of all deaths in Uganda (World Health Organisation, 2023).In 2021, cardiovascular diseases alone caused about 27,121 deaths, with an age-standardized mortality rate of 223 per 100,000 people (World Health Federation, 2025). These figures underscore the urgent need for robust, data-driven models that can predict heart disease risk and help intervene early in at-risk populations.
# About the dataset
This a cleaned version of the 2015 Behavioral Risk Factor Surveillance System (BRFSS), an annual telephone survey conducted by the Centers for Disease Control and Prevention (CDC). The BRFSS collects responses on health-related behaviors and chronic conditions from hundreds of thousands of Americans. This dataset is called " Heart Disease Health Indicators" . It contains 253,680 rows and 22 columns and  was obtained from kaggle.

# Data Description. 

Target Variable: HeartDiseaseorAttack (binary: 1 = has/had heart disease, 0 = no

Feature	Description

1. HighBP-	High blood pressure (0 = No, 1 = Yes)

2. HighChol-	High cholesterol (0 = No, 1 = Yes)

3. CholCheck	-Cholesterol check in past 5 years (0 = No, 1 = Yes)

4. BMI-	Body Mass Index (numeric)

5. Smoker-	Ever smoked at least 100 cigarettes (0 = No, 1 = Yes)

6. Stroke-	Ever had a stroke (0 = No, 1 = Yes)

7. Diabetes-	Diabetes status (0 = No, 1 = Yes)

8. PhysActivity-	Physical activity in past 30 days (0 = No, 1 = Yes)

9. Fruits-	Consumes fruit at least once per day (0 = No, 1 = Yes)

10. Veggies-	Consumes vegetables at least once per day (0 = No, 1 = Yes)

11. HvyAlcoholConsump	-Heavy alcohol consumption (0 = No, 1 = Yes)

12. AnyHealthcare-	Has any form of healthcare coverage (0 = No, 1 = Yes)

13. NoDocbcCost-	Couldn’t see a doctor because of cost (0 = No, 1 = Yes)

14. GenHlth-	General health (1 = Excellent, 5 = Poor)

15. MentHlth-	Days mental health not good (0–30)

16. PhysHlth-	Days physical health not good (0–30)

17. DiffWalk-	Difficulty walking/climbing stairs (0 = No, 1 = Yes)

18. Sex-	0 = Female, 1 = Male

19. Age	(Categorical)- age group (1 = 18–24, …, 13 = 80+)

20. Education-	Education level-(1 = Never attended … 6 = College graduate)

21. Income-	Income category (1 = <$10,000 … 8 = $75,000+)


# Machine Learning Goal.
Our machine learning goal for this project is to build a predictive model that can accurately identify individuals with heart disease using the provided dataset

# Data Processing.
We checked the data types and confirmed that all variables were floats. We then checked for missing values but found none. Duplicate records were identified and subsequently dropped. In addition, we performed Exploratory Data Analysis (EDA) using both univariate and multivariate approaches to better understand the distributions and relationships among the variables.
<img width="389" height="411" alt="image" src="https://github.com/user-attachments/assets/68d3fc5b-0d0b-4fd8-92b8-421ffe37af94" />

<img width="695" height="509" alt="image" src="https://github.com/user-attachments/assets/524556b7-2db6-4878-8fe1-0050eb1ed403" />


<img width="444" height="407" alt="image" src="https://github.com/user-attachments/assets/8405eeb3-82a7-4912-a821-56f3034bd08a" />


<img width="1459" height="1189" alt="image" src="https://github.com/user-attachments/assets/2ab948e4-c793-445b-89d4-e4e9ea3bd5a2" />

# Data Modelling.
We started with identifying our target and features, we then split the data into training,validation and testing sets.
After, we tried diffirent algorithms for traditional model which included: Logistic regression, Decision tree Classifier, Random Forest, and  XGBoost Classifier. But some algoriths more especially Decision Tree and Random Forest performed poorly on the crucial recall metric before tuning them. 

We used hyperparameter tuning to optimize each model for the specific metric that mattered most: recall. The XGBoost Classifier performed best with a high recall of 0.82 which indicates it was the most effective at minimizing false negatives and correctly identifying individuals with heart disease.

We also trained our model using both Untuned Neural Network and Tuned Neural Network(Keras). The Keras Tuner achieved the objective of maximising recall but at the cost of precision and overall accuracy. It is extremely sensitive to heart disease cases (high recall, low false negatives) but produces many false alarms (low precision, high false positives). In a medical screening context where missing true cases is unacceptable, this behaviour may be acceptable, but it leads to unnecessary follow-ups for many healthy individuals.

# Challenges faced.

1. The Challenge of Class Imbalance: The overwhelming majority of your dataset consisted of individuals without heart disease, making it difficult for the models to learn to identify the rare positive cases. An unaddressed model would likely achieve high accuracy by simply predicting "no heart disease" for everyone, but it would be useless in a clinical setting by missing almost every true case.

How we overcame it: We addressed this directly by using techniques such as balanced class weights, Random Undersampling, and SMOTE. This forced the models to pay equal attention to the minority class.

2. Model Selection & Tuning.The initial models tested ( the untuned Decision Tree and Random Forest) performed poorly on the crucial recall metric.

We used hyperparameter tuning to optimize each model for the specific metric that mattered most: recall. This process transformed the untuned models into highly effective screening tools.

# Our model implications

Positive Implications

The model is highly effective as a first-pass screening tool. Its high recall means it will likely catch nearly every person who has heart disease, minimizing the risk of a dangerous missed diagnosis.

Negative Implications

The main negative implication is the high rate of false positives due to the model's low precision. This will cause

Unnecessary Costs: A large number of healthy individuals will be flagged as having heart disease, leading to unnecessary follow-up tests, consultations, and potential treatments.

Patient Anxiety: Being told you may have heart disease can cause significant stress and anxiety for the patient, even if the diagnosis is later disproven.

Overburdened Healthcare System: The high volume of false positives could strain medical resources, including specialists' time and diagnostic equipment.

# Final Conclusion.

Our project's core finding is that the most effective strategy for this imbalanced dataset is to prioritize recall to minimize false negatives. By systematically tuning a range of models, we consistently achieved a highly effective performance profile tailored for a medical screening context.

The Tuned Neural Network (Keras Tuner) emerged as the optimal choice. It achieved the highest recall of 94% and the lowest false negative rate, making it the most reliable tool for identifying true heart disease cases. While this comes with a necessary trade-off of a higher false positive rate, this model is perfectly suited for a hospital triage setting. Its purpose is to efficiently and reliably flag at-risk individuals for further diagnostic testing, ensuring that a life-threatening condition is not missed.

