# Diabetes Dataset Analysis Project

## Overview

This project explores dataset of diabetic patient encounters.

https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008 

The goal is to analyze patient demographics, clinical factors, and readmission patterns by applying clustering techniques. This analysis helps potentially guiding targeted interventions and improving patient care.

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

| Variable Name               | Role     | Type         | Demographic | Description                                                                                                                                                            | Units | Missing Values |
|----------------------------|----------|--------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|---------------|
| encounter_id               | ID       |              |            | Unique identifier of an encounter                                                                                                                                      |       | no            |
| patient_nbr                | ID       |              |            | Unique identifier of a patient                                                                                                                                         |       | no            |
| race                       | Feature  | Categorical  | Race       | Values: Caucasian, Asian, African American, Hispanic, and other                                                                                                       |       | yes           |
| gender                     | Feature  | Categorical  | Gender     | Values: male, female, and unknown/invalid                                                                                                                             |       | no            |
| age                        | Feature  | Categorical  |            | Grouped in 10-year intervals: [0, 10), [10, 20), ..., [90, 100)                                                                                                       |       | no            |
| weight                     | Feature  | Categorical  |            | Weight in pounds.                                                                                                                                                     |       | yes           |
| admission_type_id          | Feature  | Categorical  |            | Integer identifier corresponding to 9 distinct values, for example, emergency, urgent, elective, newborn, and not available                                           |       | no            |
| discharge_disposition_id   | Feature  | Categorical  |            | Integer identifier corresponding to 29 distinct values, for example, discharged to home, expired, and not available                                                  |       | no            |
| admission_source_id        | Feature  | Categorical  |            | Integer identifier corresponding to 21 distinct values, for example, physician referral, emergency room, and transfer from a hospital                                 |       | no            |
| time_in_hospital           | Feature  | Integer      |            | Number of days between admission and discharge                                                                                                                        |       | no            |
| payer_code                 | Feature  | Categorical  |            | Integer identifier corresponding to 23 distinct values, for example, Blue Cross/Blue Shield, Medicare, and self-pay                                                  |       | yes           |
| medical_specialty          | Feature  | Categorical  |            | Integer identifier of a specialty of the admitting physician, corresponding to 84 distinct values, e.g., cardiology, internal medicine, family/general practice       |       | yes           |
| num_lab_procedures         | Feature  | Integer      |            | Number of lab tests performed during the encounter                                                                                                                    |       | no            |
| num_procedures            | Feature  | Integer      |            | Number of procedures (other than lab tests) performed during the encounter                                                                                            |       | no            |
| num_medications            | Feature  | Integer      |            | Number of distinct generic names administered during the encounter                                                                                                    |       | no            |
| number_outpatient          | Feature  | Integer      |            | Number of outpatient visits of

## Data Preprocessing

Before analysis, the dataset underwent several preprocessing steps:
- **Handling Missing Values:** most of id features:'encounter_id','patient_nbr', 'admission_type_id','discharge_disposition_id','admission_source_id'.
  irrelavant features to 'readmitted' like: 'payer_code','examide', 'citoglipton', 'glipizide-metformin', 'glimepiride-pioglitazone','metformin-rosiglitazone','metformin-pioglitazone','troglitazone','acetohexamide'
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

3 **Clusters 5–13:**  
  - **Variations:**is a bit different ication counts) with readmission rates ranging from as low as 0% (Cluster 10) to 50% (Cluster 7).  
  - **Note:** Some clusters are very small (e.g., Cluster 3, Cluster 7) and might represent outlier groups.                                      