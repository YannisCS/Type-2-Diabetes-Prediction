# Abstract
## Result
Increased Sensitivity from 51.6% to 72% to predict diabetes, taking [relevant research paper](https://www.cdc.gov/pcd/issues/2019/19_0109.htm) findings as reference which used survey data of 2014.

## Introduction
As one of the most prevalent chronic diseases in the United States, diabetes has widely among people with various aging groups, even the young kids. Diabetes not only puts a heavy burden on the shoulders of patients and their family, impacts life quality, but also on the national economy that it costs about three hundred thousand dollars annually. The majority of prediabetics, according to the CDC, are ignorant of the risk and might pass up the ideal chance for early intervention. Early diabetes detection and classification is essential for improving the condition and implementing effective treatment.

## Problem statement
•	Predict if someone has diabetes using survey questions from the BRFSS.
•	Find the risk factors that most accurately predict the risk of diabetes.

## Dataset Selection
Data Description
We choose to analyze with publicly available [survey data of BRFSS in 2022](https://www.cdc.gov/brfss/annual_data/annual_2022.html) which consist of 445132 records among 328 variables . While most of the features in the dataset are associated with survey background or health condition not related to diabetes, we are only using small segments of them.

# EDA
<img width="468" alt="image" src="https://github.com/YannisCS/Diabetes-Prediction/assets/34790986/13b8faf8-9cba-45e2-8207-835bae493deb">  

From the heatmap we look at the Diabetes column can find out some attributes that are highly correlated to the predict label. Self-evaluated general health attributes have the most positive correlation, meaning when people think they are health they tend to be health.

# Feature Engineering & Selection
There are two steps of feature selection throughout the process. First, we chose the original unprocessed dataset of 16 features from 328 survey answer variables by referring to the published study report. The second step was carried out after examining chosen characteristics and selecting just those that are directly connected to the diabetes outcome with help of PCA and filter.

We used PCA analysis not to extract features, but to decide which factors contributed the most to the diabetes variable. Looking at the PC variable indices, we discover that BMI and number of drinks are the least associated variables, which supports the visualization's results. Other three non-related variables are mental health condition, smoking habit, and asthma history.

Another method used for feature selection is filter method. A subset of features is chosen by filter method in accordance with how they relate to the target variable, that PCA does not take into consideration. Selection is independent of any algorithm based on machine learning. Conversely, filter methods use statistical tests to find how "relevant" the features are to the output. The results show that Asthma and Gender are least related to the target variable, which also supports the visualization. Other three non-related variables are mental health condition, drinking and smoking habit.  

<img width="1090" alt="image" src="https://github.com/YannisCS/Diabetes-Prediction/assets/34790986/6df6401b-000f-45c5-bba4-4049395498b1">

## Recommended features
After applying PCA and Filter, a list of features that diabetes records possibily depend on:  
age, gender, education level, income level, exercise habit, self-recognized health status, heart disease and arthritis history.

# Model Performace
Naive Bayes has a higher accuracy compared to Decision Tree, and it demonstrates slightly higher precision for class label 1 compared to Decision Tree. Decision Tree exhibits significantly higher recall for class label 1 compared to Naive Bayes and it achieves a higher F1-score, indicating better overall performance in terms of precision and recall trade-off.

Considering the emphasis on detecting class label 1, the Decision Tree model appears to be more suitable due to its significantly higher recall and higher F1-score for this class. However, it's important to consider other factors such as computational resources, interpretability, and the specific requirements of the task before making a final decision.  

<img width="746" alt="image" src="https://github.com/YannisCS/Diabetes-Prediction/assets/34790986/b0c77e03-845b-4d55-9998-2ce55e76a7e0">  

<img width="416" alt="image" src="https://github.com/YannisCS/Diabetes-Prediction/assets/34790986/a6d7198f-b4c8-4d2b-8d8e-5e330504eda9">  

<img width="245" alt="image" src="https://github.com/YannisCS/Diabetes-Prediction/assets/34790986/78c2a7fb-e5e6-4610-987b-2514831eed52">  

When reach to predict Diabetes, we debated about should we care about type I error more or type II error more. A type I error in medical area can lead to unnecessary treatments, surgeries, or emotional distress. In such cases, precision is crucial to minimize the number of false positives. While for diseases like sepsis, meningitis, or acute myocardial infarction, missing a diagnosis can be fatal. Recall is crucial to ensure that as many true positives as possible are detected.

In our case, since Diabetes is a relatively common disease, affecting over 400 million people worldwide. As such, the cost of false positives (e.g., unnecessary testing or treatment) is relatively low compared to the cost of false negatives (e.g., missing a diagnosis). This is because Diabetes is a serious disease that can lead to severe complications if left untreated. Missing a diagnosis can result in delayed treatment, which can lead to serious health consequences, including organ damage, blindness, and even death. Also having the fact that Diabetes treatment, such as medication and lifestyle changes, is generally safe and effective. As such, it is important to detect as many cases of diabetes as possible, even if some false positives occur.

Another argument occurred about should we focus on Diabetes class only or should we aim for an overall high performance matric. Trace back to our problem statement and dataset distribution, we aim to provide a basic insight on Diabetes prediction from an extremely imbalanced dataset where 83% of the records are no Diabetes. Considering the large amount of negative class record, there will be a high volume in false negative section, which we do not care about. Thus, it is better that we only compare the accuracy of Diabetes class when choosing model.

Having the idea that we want a model with high recall on classification output on class 1, we evaluate all our models by looking at classification report and choose the class-weighted decision tree to be our final model since it has the highest recall of classifying class 1.

# Conclusion
From the feature engineering we found some factors that contribute to Diabetes result very much: age, Arthritis condition, education level, exercise routine, general health condition, gender, heart disease condition, income level and how the patients think their physical health condition are.

These factors can interact with each other and with diabetes in complex ways. For example: An older adult with arthritis may be more likely to develop diabetes due to chronic inflammation and reduced physical activity. Someone with a lower education level and lower income may face barriers to accessing healthcare and healthy food options, increasing their risk of developing diabetes. A person with a family history of heart disease and diabetes may be more likely to develop diabetes due to shared genetic risk factors.

In diabetes prediction, a high recall ensures that most individuals with diabetes are correctly identified, even if some individuals without diabetes are incorrectly identified as having the disease. This is particularly important in high-risk populations, such as those with a family history of diabetes or those who are overweight or obese.

Our final model is a class weighted decision tree which has a recall of 0.72 which means it can identify Diabetes patients in most of the cases even though we have a low precision of 0.27 at same time meaning many people might be identifying as Diabetes patients when they are not. Considering the above debate between precision and recall we conclude that our model has an overall good performance on achieving our problem objective of identifying Diabetes patients.


# Reflection
- take more features in the survey into consideration
- try more models
- deal with the problem of imbalance ( we tried some methods, but the results were worse)
