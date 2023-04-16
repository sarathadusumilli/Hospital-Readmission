# Hospital-Readmission

# 1	Problem Statement 
Hospital readmissions are becoming a more expensive and noticeable problem for the general public and hospitals in terms of both money and patient care. A hospital readmission occurs when a patient who has been discharged from hospital is later readmitted within a predetermined time frame. The Hospital Readmissions Reduction Program (HRRP) is a Medicare value-based buying initiative that pushes hospitals to enhance care coordination and communication to better involve patients and caregivers in discharge plans and, as a result, lower avoidable readmission rates. By tying hospital service quality to funding, the initiative promotes the national objective of bettering Americans' access to healthcare.
Diabetes is a major contributing factor to kidney disease, heart attacks, strokes, lower limb amputation and blindness. As a result, many patients with diabetes are hospitalized to hospitals and given medication. According to the Agency for Healthcare Research and Quality (AHRQ), hospitals spent $41.3 billion between January and November 2011 treating patients who were readmitted within 30 days of being discharged. In which, diabetes led to 23,700 readmissions and cost $251 million. As this is a huge burden on both hospitals, governments, patients and insurance companies, we try solving this problem by answering the below questions:
•	How well can we predict hospital readmission? This helps hospital aims to improve quality of care for patients and lower healthcare spending. Early prediction can also help to lessen the severity of the situation and lessen the economical strain on the families. We want to employ a number of classification models, choosing the most suitable one for our forecast based on the Recall Score(Explanation for considering Recall is explained in section 5)

 
# 2	Dataset
The dataset represents clinical treatment provided over a ten-year period (1999–2008) at 130 US hospitals and integrated delivery networks. More than 50 features that represent patient and hospital outcomes are available. In our project we will specifically look for data that satisfies give us insights on hospital readmissions for diabetes. This information includes features like patient number, race, gender, and age; admission type, length of stay in the hospital; admitting physician's medical specialty; the number of lab tests conducted; the HbA1c test result; the diagnosis; the number of medications; the number of diabetic medications; and the number of outpatient, inpatient, and emergency visits in the year prior to the hospitalization.
(The dataset is taken from UCI - https://archive.ics.uci.edu/ml/datasets/Diabetes+130-US+hospitals+for+years+1999-2008 )
The data is submitted on behalf of the Center for Clinical and Translational Research, Virginia Commonwealth University, a recipient of NIH CTSA grant UL1 TR00058 and a recipient of the CERNER data. John Clore (jclore '@' vcu.edu), Krzysztof J. Cios (kcios '@' vcu.edu), Jon DeShazo (jpdeshazo '@' vcu.edu), and Beata Strack (strackb '@' vcu.edu). This data is a de-identified abstract of the Health Facts database (Cerner Corporation, Kansas City, MO).

# 3	Dataset Description:
Input Variables:
•	Encounter ID Unique identifier of an encounter

•	Patient number Unique identifier of a patient

•	Race Values: Caucasian, Asian, African American, Hispanic, and other

•	Gender Values: male, female, and unknown/invalid

•	Age Grouped in 10-year intervals: 0, 10), 10, 20), …, 90, 100)

•	Weight Weight in pounds

•	Admission type Integer identifier corresponding to 9 distinct values, for example, emergency, urgent, elective, newborn, and not available

•	Discharge disposition Integer identifier corresponding to 29 distinct values, for example, discharged to home, expired, and not available

•	Admission source Integer identifier corresponding to 21 distinct values, for example, physician referral, emergency room, and transfer from a hospital

•	Time in hospital Integer number of days between admission and discharge

•	Payer code Integer identifier corresponding to 23 distinct values, for example, Blue Cross/Blue Shield, Medicare, and self-pay Medical

•	Medical specialty Integer identifier of a specialty of the admitting physician, corresponding to 84 distinct values, for example, cardiology, internal medicine, 
family/general practice, and surgeon

•	Number of lab procedures Number of lab tests performed during the encounter

•	Number of procedures Numeric Number of procedures (other than lab tests) performed during the encounter

•	Number of medications Number of distinct generic names administered during the encounter

•	Number of outpatient visits Number of outpatient visits of the patient in the year preceding the encounter

•	Number of emergency visits Number of emergency visits of the patient in the year preceding the encounter

•	Number of inpatient visits Number of inpatient visits of the patient in the year preceding the encounter

•	Diagnosis 1 The primary diagnosis (coded as first three digits of ICD9); 848 distinct values

•	Diagnosis 2 Secondary diagnosis (coded as first three digits of ICD9); 923 distinct values

•	Diagnosis 3 Additional secondary diagnosis (coded as first three digits of ICD9); 954 distinct values

•	Number of diagnoses Number of diagnoses entered to the system 0%

•	Glucose serum test result Indicates the range of the result or if the test was not taken. Values: “>200,” “>300,” “normal,” and “none” if not measured

•	A1c test result Indicates the range of the result or if the test was not taken. Values: “>8” if the result was greater than 8%, “>7” if the result was greater than 
7% but less than 8%, “normal” if the result was less than 7%, and “none” if not measured.

•	Change of medications Indicates if there was a change in diabetic medications (either dosage or generic name). Values: “change” and “no change”

•	Diabetes medications Indicates if there was any diabetic medication prescribed. Values: “yes” and “no”

•	24 features for medications For the generic names: metformin, repaglinide, nateglinide, chlorpropamide, glimepiride, acetohexamide, glipizide, glyburide, 
tolbutamide, pioglitazone, rosiglitazone, acarbose, miglitol, troglitazone, tolazamide, examide, sitagliptin, insulin, glyburide-metformin, glipizide-metformin, glimepiride- pioglitazone, metformin-rosiglitazone, and metformin- pioglitazone, the feature indicates whether the drug was prescribed or there was a change in the dosage. Values: “up” if the dosage was increased during the encounter, “down” if the dosage was decreased, “steady” if the dosage did not change, and “no” if the drug was not prescribed

Target Variable:

•	Readmitted Days to inpatient readmission. Values: “<30” if the patient was readmitted in less than 30 days, “>30” if the patient was readmitted in more than 30 days, 
and “No” for no record of readmission


# 4	Pre-processing:
To improve the feature set for modeling, we will perform a thorough pre-processing process and some feature engineering steps like below:

•	Install and import necessary packages

•	Loading the Data

•	Data Exploration

  o	Identification of variables and data types: 
  Understanding variables is the core of any data analysis. A smart place to begin is with a brief study of the column names. Analyzing data catalogues, field           definitions, and metadata in greater detail can shed light on what each field means.
  
  o	Analyzing the basic metrics
  
  o	Data Cleaning
     o Clean up column names if there are some leading whitespace characters.
     
     o Drop the columns we are not using as predictors 
     o Handling Missing Values.
     o Data Encoding: 
        We need to transform or encode categorical data to numeric values. Before we get there, we will understand different types of categorical data(Nominal Scale or         Ordinal Scale). We know that most of our models work exclusively with numeric data. That is why we need to encode categorical features into a representation           compatible with the models. Hence, we will use some encoding approaches like Label encoding/One-hot encoding/Ordinal Encoding.

•	Addressing the issue of Multicollinearity: 
    
    o	Multicollinearity occurs when independent variables in a regression model are correlated. This correlation is a problem because independent variables should be         independent. If the degree of correlation between variables is high enough, it can cause problems when you fit the model and interpret the results. We will             handle them by removing some of the highly correlated independent variables.

•	Data Balancing
    
    o	Two approaches to make a balanced dataset out of an imbalanced one are under-sampling and over-sampling. We would like to use over-sampling Technique to handle         it.
•	Standardization

# 5	Modeling and Analysis:
In this Dataset, our target has 3 different classes:

•	Readmission in less than 30 days (this situation is not good, because maybe your treatment was not appropriate).

•	Readmission in more than 30 days  

•	No readmission.

As per our problem statement we need to predict whether patients are readmitting in less than 30 days or not. So, we can combine these three classes in to two and consider this as Binary class classifier.
Since this is a binary classification problem we plan to implement below models and hyper tune them to achieve better metrics. We are not restricting only to these models, we would like to start with these and will to try apply other binary classification models as well if needed.

•	Logistic Regression

•	Decision Tree

•	Random Forest

•	K-Nearest Neighbours

•	XGBoost

•	AdaBoost

•	GradientBoosting

Below are the high level steps which we would like to perform while modeling.

•	Splitting the data into Training and Validation Sets:

The data is divided into a 70/30 ratio, with 70% of the data being used for training and the remaining 30% being used for testing.

•	Train the model using train data

•	Measure the performance of model using test/validation data.

•	Using confusion matrix to determine True Positives(TP), True Negatives(TN), False Positives (FP) and False Negatives(FN).

•	Will calculate Recall, Accuracy, Precision and F1 Scores.

•	We will perform Hyperparameter tuning to find out best metrics

•	We will perform model comparison using Recall and will find out best model.

In our case, below are our equations for False Negatives and False Positives. 
FN: Patient Readmitted but model predicted as not readmitted (More Damage)
FP: Patient didn’t readmit but predicted as readmitted (Less damage)
Here after thorough brainstorming, we could see that FN has more weightage, we will consider Recall as our metric and will evaluate models based on that.
Three main findings can be drawn from our project:
First, using the proper pre-processing techniques, particularly when working with unbalanced data, can have a major impact on the models' outputs and offer more knowledge about readmission predictors.
Second, though there was previous work done on this dataset which we listed in section 6 below, we are not limiting ourselves with the predictors they used. We would like to explore all the possible chances to find out best model.
Third, based on the outcome of prediction, we would like to suggest a model that helps hospitals to reduce readmissions. With this we could save millions of dollars in the form of readmissions and patient will experience higher-quality treatment.  
