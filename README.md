# Diabetes Dataset Analysis Project

## Overview

This project explores dataset of diabetic patient encounters. The goal is to analyze patient demographics, clinical factors, and readmission patterns by applying clustering techniques. This analysis helps potentially guiding targeted interventions and improving patient care.

## Dataset Description

The dataset includes multiple variables grouped into three main categories:

- **Identifiers:**  
  - `encounter_id`: Unique identifier for each encounter.  
  - `patient_nbr`: Unique identifier for each patient.

- **Demographic and Clinical Features:**  
  - **Demographics:** `race`, `gender`, `age` (grouped in intervals), and `weight`.  
  - **Hospitalization Details:** Variables such as `admission_type_id`, `discharge_disposition_id`, `admission_source_id`, and `time_in_hospital`.  
  - **Clinical Procedures and Tests:** `num_lab_procedures`, `num_procedures`, `num_medications`, `number_outpatient`, `number_emergency`, and `number_inpatient`.  
  - **Diagnostic Information:** Primary and secondary diagnoses (`diag_1`, `diag_2`, `diag_3`) and `number_diagnoses`.  
  - **Lab Results and Medications:** Variables like `max_glu_serum`, `A1Cresult`, and several medication-related features that indicate if a drug was prescribed or if there was a change in dosage.

- **Target Variable:**  
  - `readmitted`: Indicates the patient’s readmission status with values such as `<30` (readmitted within 30 days), `>30`, and `No`.

## Complete List of Variables

| Variable Name              | Role    | Type        | Demographic | Description                                                                                                                                                                                                                                                                                           | Units | Missing Values |
|----------------------------|---------|-------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|----------------|
| encounter_id               | ID      |             |             | Unique identifier of an encounter                                                                                                                                                                                                                                                                    |       | no             |
| patient_nbr                | ID      |             |             | Unique identifier of a patient                                                                                                                                                                                                                                                                        |       | no             |
| race                       | Feature | Categorical | Race        | Values: Caucasian, Asian, African American, Hispanic, and other                                                                                                                                                                                                                                       |       | yes            |
| gender                     | Feature | Categorical | Gender      | Values: male, female, and unknown/invalid                                                                                                                                                                                                                                                             |       | no             |
| age                        | Feature | Categorical | Age         | Grouped in 10-year intervals: [0, 10), [10, 20), ..., [90, 100)                                                                                                                                                                                                                                      |       | no             |
| weight                     | Feature | Categorical |             | Weight in pounds.                                                                                                                                                                                                                                                                                     |       | yes            |
| admission_type_id          | Feature | Categorical |             | Integer identifier corresponding to 9 distinct values, for example, emergency, urgent, elective, newborn, and not available                                                                                                                                                                           |       | no             |
| discharge_disposition_id   | Feature | Categorical |             | Integer identifier corresponding to 29 distinct values, for example, discharged to home, expired, and not available                                                                                                                                                                                    |       | no             |
| admission_source_id        | Feature | Categorical |             | Integer identifier corresponding to 21 distinct values, for example, physician referral, emergency room, and transfer from a hospital                                                                                                                                                                  |       | no             |
| time_in_hospital           | Feature | Integer     |             | Integer number of days between admission and discharge                                                                                                                                                                                                                                              |       | no             |
| payer_code                 | Feature | Categorical |             | Integer identifier corresponding to 23 distinct values, for example, Blue Cross/Blue Shield, Medicare, and self-pay                                                                                                                                                                                     |       | yes            |
| medical_specialty          | Feature | Categorical |             | Integer identifier of a specialty of the admitting physician, corresponding to 84 distinct values, for example, cardiology, internal medicine, family/general practice, and surgeon                                                                                                               |       | yes            |
| num_lab_procedures         | Feature | Integer     |             | Number of lab tests performed during the encounter                                                                                                                                                                                                                                                  |       | no             |
| num_procedures             | Feature | Integer     |             | Number of procedures (other than lab tests) performed during the encounter                                                                                                                                                                                                                           |       | no             |
| num_medications            | Feature | Integer     |             | Number of distinct generic names administered during the encounter                                                                                                                                                                                                                                   |       | no             |
| number_outpatient          | Feature | Integer     |             | Number of outpatient visits of the patient in the year preceding the encounter                                                                                                                                                                                                                       |       | no             |
| number_emergency           | Feature | Integer     |             | Number of emergency visits of the patient in the year preceding the encounter                                                                                                                                                                                                                        |       | no             |
| number_inpatient           | Feature | Integer     |             | Number of inpatient visits of the patient in the year preceding the encounter                                                                                                                                                                                                                        |       | no             |
| diag_1                     | Feature | Categorical |             | The primary diagnosis (coded as first three digits of ICD9); 848 distinct values                                                                                                                                                                                                                    |       | yes            |
| diag_2                     | Feature | Categorical |             | Secondary diagnosis (coded as first three digits of ICD9); 923 distinct values                                                                                                                                                                                                                       |       | yes            |
| diag_3                     | Feature | Categorical |             | Additional secondary diagnosis (coded as first three digits of ICD9); 954 distinct values                                                                                                                                                                                                            |       | yes            |
| number_diagnoses           | Feature | Integer     |             | Number of diagnoses entered to the system                                                                                                                                                                                                                                                           |       | no             |
| max_glu_serum              | Feature | Categorical |             | Indicates the range of the result or if the test was not taken. Values: >200, >300, normal, and none if not measured                                                                                                                                                                                  |       | no             |
| A1Cresult                  | Feature | Categorical |             | Indicates the range of the result or if the test was not taken. Values: >8 if the result was greater than 8%, >7 if the result was greater than 7% but less than 8%, normal if the result was less than 7%, and none if not measured.                                                   |       | no             |
| metformin                  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| repaglinide                | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| nateglinide                | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| chlorpropamide             | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| glimepiride                | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| acetohexamide              | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| glipizide                  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| glyburide                 | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| tolbutamide               | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| pioglitazone              | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| rosiglitazone             | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| acarbose                  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| miglitol                  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| troglitazone              | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| tolazamide                | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| examide                   | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| citoglipton               | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| insulin                   | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| glyburide-metformin       | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| glipizide-metformin       | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| glimepiride-pioglitazone  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| metformin-rosiglitazone   | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| metformin-pioglitazone    | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| change                    | Feature | Categorical |             | Indicates if there was a change in diabetic medications (either dosage or generic name). Values: change and no change                                                                                                                                                                                  |       | no             |
| diabetesMed               | Feature | Categorical |             | Indicates if there was any diabetic medication prescribed. Values: yes and no                                                                                                                                                                                                                        |       | no             |
| readmitted                | Target  | Categorical |             | Days to inpatient readmission. Values: <30 if the patient was readmitted in less than 30 days, >30 if readmitted in more than 30 days, and No for no record of readmission.                                                                                                                      |       | no             |


## Data Preprocessing

Before analysis, the dataset underwent several preprocessing steps:
- **Handling Missing Values:** Missing entries were addressed based on the variable’s importance and distribution.
- **Encoding Categorical Variables:** Categorical variables were encoded by ordinalEncoder
- **Normalization:** Continuous variables were scaled by StandardScaler

## Clustering Analysis

Two types of unsupervised clustering (K-means Model and DBScan Model) was applied to the dataset and has been compared by the results.

### Summary of Clustering Results

The clustering analysis produced the following clusters:

| Cluster | Size | <30 Day Readmissions | Readmission Rate |
|---------|------|----------------------|------------------|
| 0       | 593  | 50                   | 8.43%            |
| 1       | 440  | 55                   | 12.50%           |
| 2       | 111  | 31                   | 27.93%           |
| 3       | 3    | 1                    | 33.33%           |
| 4       | 210  | 26                   | 12.38%           |
| 5       | 214  | 21                   | 9.81%            |
| 6       | 105  | 11                   | 10.48%           |
| 7       | 2    | 1                    | 50.00%           |
| 8       | 146  | 14                   | 9.59%            |
| 9       | 302  | 11                   | 3.64%            |
| 10      | 1    | 0                    | 0.00%            |
| 11      | 14   | 1                    | 7.14%            |
| 12      | 29   | 2                    | 6.90%            |
| 13      | 390  | 54                   | 13.85%           |


## Patient Cluster Characteristics

Based on the clustering results, here are some high-level observations on the patient characteristics in each cluster:

- **Cluster 0:**  
  - **Demographics:** Mostly Caucasian with a mix of genders.  
  - **Age & Weight:** Patients aged between ~50–80, commonly with weight in the [75–100) range 
  - **Hospital Stay:** Moderate length of stay (3–6 days) with a low readmission rate

- **Cluster 1:**  
  - **Demographics:** Mostly Caucasian with some patients in their 20s 
  - **Hospital Stay:** Around 1–12 days

- **Cluster 2 & 3:**  
  - **Demographics:** Older patients with higher readmission rates (up to 27–33%)  
  - **Clinical Notes:** These clusters may require closer follow-up 

- **Cluster 4:**  
  - **Demographics:** Older population with varied weight ranges and moderate hospital stays.  
  - **Observations:** Shows a balanced mix of lab and procedural counts.

3 **Clusters 5–15:**  
  - **Variations:**is a bit different ication counts) with readmission rates ranging from as low as 0% (Cluster 10) to 50% (Cluster 7).  
  - **Note:** Some clusters are very small (e.g., Cluster 3, Cluster 7) and might rst ou| Cluster | Dominant Race / Gender         | Typical Age Range       | Typical Weight Range   | Hospital Stay (Days) | Readmission Rate | Additional Observations                                          |
|---------|--------------------------------|-------------------------|------------------------|----------------------|------------------|------------------------------------------------------------------|
| 0       | Predominantly Caucasian; mixed genders (with some African American) | Mostly older (∼70–80, ∼80–90) | Mostly [50–75); occasional lower ([25–50]) or higher ([100–125]) | 3–6                | 8.43%           | Large group with moderate stays & lab/procedure counts           |
| 1       | Predominantly Caucasian; many females in younger age groups         | Younger to mid (∼20–30, ∼40–50, some [50–60]) | Mainly [50–75), with some higher ([125–150])         | 1–12               | 12.50%          | Younger patients with relatively higher readmission rate         |
| 2       | Almost entirely Caucasian (majority female)                         | Older (∼70–80 to ∼80–90)              | [50–75) to [100–125]       | Around 6–7         | 27.93%          | High-risk group; highest readmission rate among larger clusters    |
| 3       | Exclusively Caucasian females (small group)                         | Middle-age to older ([40–50] to [80–90]) | Mostly [50–75)           | 3–9                | 33.33%          | Extremely small group with a notably high readmission rate         |
| 4       | Predominantly Caucasian; slightly more males                        | Mostly older ([70–80] to [90–100))     | Mostly [50–75)           | 5–8                | 12.38%          | Consistent older patients with moderate hospital stays            |
| 5       | Predominantly Caucasian; mixed genders                                | Mid-age (∼50–60 to ∼70–80)              | Mostly [75–100); occasional outlier ([150–175]) | Generally short (2–10) | 9.81%           | Lower readmission; overall stable clinical profile                 |
| 6       | Caucasian; both genders                                               | [60–70) to [70–80)                     | Consistently [100–125)     | 2–3                | 10.48%          | Consistent short stays among older patients with higher weight       |
| 7       | Exclusively Caucasian                                                 | Mostly [70–80) (with one [50–60) case)   | Uniformly [75–100)        | Variable (1–11)    | 50.00%          | Very small group (only 2–3 patients) with an unusually high rate      |
| 8       | Predominantly Caucasian with some African American; mix genders         | Younger to mid (∼40–50 to ∼60–70)       | Mainly [75–100); occasional high ([150–175]) | 2–6                | 9.59%           | Mixed characteristics; majority are younger with short stays         |
| 9       | Likely older Caucasian females                                        | Very old ([90–100))          # Diabetes Dataset Analysis Project

## Overview

This project explores dataset of diabetic patient encounters. The goal is to analyze patient demographics, clinical factors, and readmission patterns by applying clustering techniques. This analysis helps potentially guiding targeted interventions and improving patient care.

## Dataset Description

The dataset includes multiple variables grouped into three main categories:

- **Identifiers:**  
  - `encounter_id`: Unique identifier for each encounter.  
  - `patient_nbr`: Unique identifier for each patient.

- **Demographic and Clinical Features:**  
  - **Demographics:** `race`, `gender`, `age` (grouped in intervals), and `weight`.  
  - **Hospitalization Details:** Variables such as `admission_type_id`, `discharge_disposition_id`, `admission_source_id`, and `time_in_hospital`.  
  - **Clinical Procedures and Tests:** `num_lab_procedures`, `num_procedures`, `num_medications`, `number_outpatient`, `number_emergency`, and `number_inpatient`.  
  - **Diagnostic Information:** Primary and secondary diagnoses (`diag_1`, `diag_2`, `diag_3`) and `number_diagnoses`.  
  - **Lab Results and Medications:** Variables like `max_glu_serum`, `A1Cresult`, and several medication-related features that indicate if a drug was prescribed or if there was a change in dosage.

- **Target Variable:**  
  - `readmitted`: Indicates the patient’s readmission status with values such as `<30` (readmitted within 30 days), `>30`, and `No`.

## Complete List of Variables

| Variable Name              | Role    | Type        | Demographic | Description                                                                                                                                                                                                                                                                                           | Units | Missing Values |
|----------------------------|---------|-------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|----------------|
| encounter_id               | ID      |             |             | Unique identifier of an encounter                                                                                                                                                                                                                                                                    |       | no             |
| patient_nbr                | ID      |             |             | Unique identifier of a patient                                                                                                                                                                                                                                                                        |       | no             |
| race                       | Feature | Categorical | Race        | Values: Caucasian, Asian, African American, Hispanic, and other                                                                                                                                                                                                                                       |       | yes            |
| gender                     | Feature | Categorical | Gender      | Values: male, female, and unknown/invalid                                                                                                                                                                                                                                                             |       | no             |
| age                        | Feature | Categorical | Age         | Grouped in 10-year intervals: [0, 10), [10, 20), ..., [90, 100)                                                                                                                                                                                                                                      |       | no             |
| weight                     | Feature | Categorical |             | Weight in pounds.                                                                                                                                                                                                                                                                                     |       | yes            |
| admission_type_id          | Feature | Categorical |             | Integer identifier corresponding to 9 distinct values, for example, emergency, urgent, elective, newborn, and not available                                                                                                                                                                           |       | no             |
| discharge_disposition_id   | Feature | Categorical |             | Integer identifier corresponding to 29 distinct values, for example, discharged to home, expired, and not available                                                                                                                                                                                    |       | no             |
| admission_source_id        | Feature | Categorical |             | Integer identifier corresponding to 21 distinct values, for example, physician referral, emergency room, and transfer from a hospital                                                                                                                                                                  |       | no             |
| time_in_hospital           | Feature | Integer     |             | Integer number of days between admission and discharge                                                                                                                                                                                                                                              |       | no             |
| payer_code                 | Feature | Categorical |             | Integer identifier corresponding to 23 distinct values, for example, Blue Cross/Blue Shield, Medicare, and self-pay                                                                                                                                                                                     |       | yes            |
| medical_specialty          | Feature | Categorical |             | Integer identifier of a specialty of the admitting physician, corresponding to 84 distinct values, for example, cardiology, internal medicine, family/general practice, and surgeon                                                                                                               |       | yes            |
| num_lab_procedures         | Feature | Integer     |             | Number of lab tests performed during the encounter                                                                                                                                                                                                                                                  |       | no             |
| num_procedures             | Feature | Integer     |             | Number of procedures (other than lab tests) performed during the encounter                                                                                                                                                                                                                           |       | no             |
| num_medications            | Feature | Integer     |             | Number of distinct generic names administered during the encounter                                                                                                                                                                                                                                   |       | no             |
| number_outpatient          | Feature | Integer     |             | Number of outpatient visits of the patient in the year preceding the encounter                                                                                                                                                                                                                       |       | no             |
| number_emergency           | Feature | Integer     |             | Number of emergency visits of the patient in the year preceding the encounter                                                                                                                                                                                                                        |       | no             |
| number_inpatient           | Feature | Integer     |             | Number of inpatient visits of the patient in the year preceding the encounter                                                                                                                                                                                                                        |       | no             |
| diag_1                     | Feature | Categorical |             | The primary diagnosis (coded as first three digits of ICD9); 848 distinct values                                                                                                                                                                                                                    |       | yes            |
| diag_2                     | Feature | Categorical |             | Secondary diagnosis (coded as first three digits of ICD9); 923 distinct values                                                                                                                                                                                                                       |       | yes            |
| diag_3                     | Feature | Categorical |             | Additional secondary diagnosis (coded as first three digits of ICD9); 954 distinct values                                                                                                                                                                                                            |       | yes            |
| number_diagnoses           | Feature | Integer     |             | Number of diagnoses entered to the system                                                                                                                                                                                                                                                           |       | no             |
| max_glu_serum              | Feature | Categorical |             | Indicates the range of the result or if the test was not taken. Values: >200, >300, normal, and none if not measured                                                                                                                                                                                  |       | no             |
| A1Cresult                  | Feature | Categorical |             | Indicates the range of the result or if the test was not taken. Values: >8 if the result was greater than 8%, >7 if the result was greater than 7% but less than 8%, normal if the result was less than 7%, and none if not measured.                                                   |       | no             |
| metformin                  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| repaglinide                | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| nateglinide                | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| chlorpropamide             | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| glimepiride                | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| acetohexamide              | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a dosage change. Values: up if increased, down if decreased, steady if unchanged, and no if not prescribed                                                                                                                                  |       | no             |
| glipizide                  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| glyburide                 | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| tolbutamide               | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| pioglitazone              | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| rosiglitazone             | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| acarbose                  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| miglitol                  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| troglitazone              | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| tolazamide                | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| examide                   | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| citoglipton               | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| insulin                   | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| glyburide-metformin       | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| glipizide-metformin       | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| glimepiride-pioglitazone  | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| metformin-rosiglitazone   | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| metformin-pioglitazone    | Feature | Categorical |             | Indicates whether the drug was prescribed or there was a change in the dosage. Values: up if increased during the encounter, down if decreased, steady if unchanged, and no if not prescribed                                                                                                      |       | no             |
| change                    | Feature | Categorical |             | Indicates if there was a change in diabetic medications (either dosage or generic name). Values: change and no change                                                                                                                                                                                  |       | no             |
| diabetesMed               | Feature | Categorical |             | Indicates if there was any diabetic medication prescribed. Values: yes and no                                                                                                                                                                                                                        |       | no             |
| readmitted                | Target  | Categorical |             | Days to inpatient readmission. Values: <30 if the patient was readmitted in less than 30 days, >30 if readmitted in more than 30 days, and No for no record of readmission.                                                                                                                      |       | no             |


## Data Preprocessing

Before analysis, the dataset underwent several preprocessing steps:
- **Handling Missing Values:** Missing entries were addressed based on the variable’s importance and distribution.
- **Encoding Categorical Variables:** Categorical variables were encoded by ordinalEncoder
- **Normalization:** Continuous variables were scaled by StandardScaler

## Clustering Analysis

Two types of unsupervised clustering (K-means Model and DBScan Model) was applied to the dataset and has been compared by the results.

### Summary of Clustering Results

The clustering analysis produced the following clusters:

| Cluster | Size | <30 Day Readmissions | Readmission Rate |
|---------|------|----------------------|------------------|
| 0       | 593  | 50                   | 8.43%            |
| 1       | 440  | 55                   | 12.50%           |
| 2       | 111  | 31                   | 27.93%           |
| 3       | 3    | 1                    | 33.33%           |
| 4       | 210  | 26                   | 12.38%           |
| 5       | 214  | 21                   | 9.81%            |
| 6       | 105  | 11                   | 10.48%           |
| 7       | 2    | 1                    | 50.00%           |
| 8       | 146  | 14                   | 9.59%            |
| 9       | 302  | 11                   | 3.64%            |
| 10      | 1    | 0                    | 0.00%            |
| 11      | 14   | 1                    | 7.14%            |
| 12      | 29   | 2                    | 6.90%            |
| 13      | 390  | 54                   | 13.85%           |


## Patient Cluster Characteristics

Based on the clustering results, here are some high-level observations on the patient characteristics in each cluster:

- **Cluster 0:**  
  - **Demographics:** Mostly Caucasian with a mix of genders.  
  - **Age & Weight:** Patients aged between ~50–80, commonly with weight in the [75–100) range 
  - **Hospital Stay:** Moderate length of stay (3–6 days) with a low readmission rate

- **Cluster 1:**  
  - **Demographics:** Mostly Caucasian with some patients in their 20s 
  - **Hospital Stay:** Around 1–12 days

- **Cluster 2 & 3:**  
  - **Demographics:** Older patients with higher readmission rates (up to 27–33%)  
  - **Clinical Notes:** These clusters may require closer follow-up 

- **Cluster 4:**  
  - **Demographics:** Older population with varied weight ranges and moderate hospital stays.  
  - **Observations:** Shows a balanced mix of lab and procedural counts.

- **Clusters 5–13:**  
  - **Variations:** These clusters is a bit different with readmission rates ranging from as low as 0% (Cluster 10) to 50% (Cluster 7).  
  - **Note:** Some clusters are very small (e.g., Cluster 3, Cluster 7) and might represent outliers.


| Cluster | Dominant Race / Gender         | Typical Age Range       | Typical Weight Range   | Hospital Stay (Days) | Readmission Rate | Additional Observations                                          |
|---------|--------------------------------|-------------------------|------------------------|----------------------|------------------|------------------------------------------------------------------|
| 0       | Predominantly Caucasian; mixed genders (with some African American) | Mostly older (∼70–80, ∼80–90) | Mostly [50–75); occasional lower ([25–50]) or higher ([100–125]) | 3–6                | 8.43%           | Large group with moderate stays & lab/procedure counts           |
| 1       | Predominantly Caucasian; many females in younger age groups         | Younger to mid (∼20–30, ∼40–50, some [50–60]) | Mainly [50–75), with some higher ([125–150])         | 1–12               | 12.50%          | Younger patients with relatively higher readmission rate         |
| 2       | Almost entirely Caucasian (majority female)                         | Older (∼70–80 to ∼80–90)              | [50–75) to [100–125]       | Around 6–7         | 27.93%          | High-risk group; highest readmission rate among larger clusters    |
| 3       | Exclusively Caucasian females (small group)                         | Middle-age to older ([40–50] to [80–90]) | Mostly [50–75)           | 3–9                | 33.33%          | Extremely small group with a notably high readmission rate         |
| 4       | Predominantly Caucasian; slightly more males                        | Mostly older ([70–80] to [90–100))     | Mostly [50–75)           | 5–8                | 12.38%          | Consistent older patients with moderate hospital stays            |
| 5       | Predominantly Caucasian; mixed genders                                | Mid-age (∼50–60 to ∼70–80)              | Mostly [75–100); occasional outlier ([150–175]) | Generally short (2–10) | 9.81%           | Lower readmission; overall stable clinical profile                 |
| 6       | Caucasian; both genders                                               | [60–70) to [70–80)                     | Consistently [100–125)     | 2–3                | 10.48%          | Consistent short stays among older patients with higher weight       |
| 7       | Exclusively Caucasian                                                 | Mostly [70–80) (with one [50–60) case)   | Uniformly [75–100)        | Variable (1–11)    | 50.00%          | Very small group (only 2–3 patients) with an unusually high rate      |
| 8       | Predominantly Caucasian with some African American; mix genders         | Younger to mid (∼40–50 to ∼60–70)       | Mainly [75–100); occasional high ([150–175]) | 2–6                | 9.59%           | Mixed characteristics; majority are younger with short stays         |
| 9       | Likely older Caucasian females                                        | Very old ([90–100))                    | [50–75)                  | ∼3                 | 3.64%           | Represents a group of very elderly patients with low readmission rate  |
| 10      | Single Caucasian female                                               | [80–90)                                | [75–100)                 | 11                 | 0.00%           | Outlier; a single patient with a long stay and no readmission         |
| 11      | Predominantly Caucasian                                               | Wide range ([30–40) up to [70–80] or more) | Varies ([75–100) to [125–150]) | Variable (1–14)    | 7.14%           | Small group with diverse ages and lengths of stay                    |
| 12      | Predominantly Caucasian                                               | Mid-age ([50–60) to [70–80))            | Mostly [75–100)         | Short (2–8)        | 6.90%           | Relatively low readmission; smaller, stable cluster                   |
| 13      | Likely predominantly Caucasian; mix genders                           | Likely older (pattern similar to clusters 0 & 4) | Mixed (commonly [75–100] or higher) | Moderate           | 13.85%          | Large group with moderately high readmission; further analysis needed  |



          | [50–75)                  | ∼3                 | 3.64%           | Represents a group of very elderly patients with low readmission rate  |
| 10      | Single Caucasian female                                               | [80–90)                                | [75–100)                 | 11                 | 0.00%           | Outlier; a single patient with a long stay and no readmission         |
| 11      | Predominantly Caucasian                                               | Wide range ([30–40) up to [70–80] or more) | Varies ([75–100) to [125–150]) | Variable (1–14)    | 7.14%           | Small group with diverse ages and lengths of stay                    |
| 12      | Predominantly Caucasian                                               | Mid-age ([50–60) to [70–80))            | Mostly [75–100)         | Short (2–8)        | 6.90%           | Relatively low readmission; smaller, stable cluster                   |
| 13      | Likely predominantly Caucasian; mix genders                           | Likely older (pattern similar to clusters 0 & 4) | Mixed (commonly [75–100] or higher) | Moderate           | 13.85%          | Large group with moderately high readmission; further analysis needed  |



            |


