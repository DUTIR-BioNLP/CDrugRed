[ **English** | [中文](./README.md) \]


# Discharge Medication Recommendation Task for Metabolic Diseases Based on Chinese Electronic Health Records

<p align="center"> ⭐ <a href="https://tianchi.aliyun.com/competition/entrance/532411">Tianchi Evaluation Website</a>&nbsp&nbsp | &nbsp&nbsp📅 <a href="http://cips-chip.org.cn/2025/">CHIP Conference Evaluation Website</a>&nbsp&nbsp | &nbsp&nbsp🗂️<a href="[./data_file/dataset_inf.md](https://tianchi.aliyun.com/competition/entrance/532411/information)">Evaluation Data</a>&nbsp&nbsp | &nbsp&nbsp📃 <a href="https://arxiv.org/abs/2510.21084">Dataset Paper</a> <br><br> </p>


- [Discharge Medication Recommendation Task for Metabolic Diseases Based on Chinese Electronic Health Records](#discharge-medication-recommendation-task-for-metabolic-diseases-based-on-chinese-electronic-health-records)
  - [Background](#background)
  - [Task Description](#task-description)
  - [Dataset Description](#dataset-description)
    - [1. Data Scale](#1-data-scale)
    - [2. Field Description](#2-field-description)
    - [3. Data Example](#3-data-example)
  - [Evaluation Metrics](#evaluation-metrics)
  - [Baseline System](#baseline-system)
  - [Result Submission](#result-submission)
    - [1. Submission Method](#1-submission-method)
    - [2. Submission Format](#2-submission-format)
  - [Organizers](#organizers)
  - [Dataset Paper and Citation](#dataset-paper-and-citation)


## Background

Metabolic diseases—such as diabetes, hypertension, and fatty liver disease—are major chronic conditions characterized by complex pathophysiological mechanisms and significant individual differences. These diseases pose serious threats to public health and social development. In clinical practice, patients with multiple metabolic disorders require complex treatment plans, and the selection of medications must comprehensively consider prior medical history, concomitant medications, and complications. Exploring innovative drug management models to assist physicians and pharmacists in developing precise and personalized treatment plans is of great importance for improving therapeutic efficacy and reducing adverse drug reactions.

In the “hospital–community/home” closed-loop care system, discharge medication is the key link for connecting inpatient and outpatient treatment. It directly affects disease control and readmission risk. However, the large volume of inpatient data (including medical notes, lab tests, and medication records) is difficult to fully integrate into discharge decision-making in a timely and comprehensive manner. Chinese electronic health records (EHRs) contain complete diagnostic and treatment information, providing crucial data for building personalized medication recommendation systems. With the rapid advancement of artificial intelligence, research on intelligent pharmacy and precision therapy based on EHRs has become an important direction in medical AI.
This evaluation task focuses on “discharge drug recommendation based on inpatient EHRs.” Given a patient’s hospitalization record, the goal is to automatically generate personalized discharge medication recommendations, thereby improving rational drug use and long-term disease outcomes.

## Task Description

This task uses real, de-identified hospital EHR data to evaluate and compare the performance of various models in discharge medication recommendation. The task is defined as: **Given a patient’s inpatient record written in natural language (including chief complaint, medical history, diagnostic and treatment information, etc.), the model must recommend a list of medications the patient should take after discharge**.

- Input: Relevant fields from the patient’s EHR excluding discharge medications, mainly including chief complaint, present illness, past history, admission information, treatment process, and discharge diagnosis.

- Output: The set of medications the patient should be prescribed at discharge (limited to the 651 drugs listed in the provided “Candidate Drug List”).

Participants may use traditional neural networks, pretrained language models, or large models (with no more than 10B parameters). Prompt learning, fine-tuning, and retrieval-augmented generation are all allowed (external knowledge sources must be clearly stated).

## Dataset Description

This task introduces a dedicated dataset for evaluating discharge drug recommendation in metabolic diseases, named CDrugRed. The dataset was constructed from de-identified EHRs provided by the Second Affiliated Hospital of Dalian Medical University. It contains 5,894 medical records from 3,190 patients. The dataset is divided into training, development (Leaderboard A), and test (Leaderboard B) sets. The development and test sets do not contain ground truth labels, and predictions must be submitted online.

**Dataset Access Procedure**

- Download and complete the “Dataset Usage Agreement” at the end of this document, filling in team information and obtaining the team leader’s handwritten signature.

- Email the signed PDF to CDrugRed@163.com
 with the subject line: “Institution-TeamName-CDrugRed Dataset Application.”

- After verification, the organizers will send back the dataset decryption password by email.

- Use the provided password to extract the dataset. The same password applies to both A and B leaderboard datasets.

### 1. Data Scale

|      Dataset     |      Number of Patients     |      Number of Records     |
|-----------------|-------------------|-------------------|
|     Training Set      |     1,910         |     3,602         |
|     Development Set      |     320           |     570           |
|     Test Set     |     960           |     1,722         |


### 2. Field Description

- Patient ID: Unique patient identifier
- Visit ID: Unique identifier for each hospital visit (a patient may have multiple records)
- Gender
- Date of Birth
- Ethnicity
- BMI: Body Mass Index
- Visit Time: Admission date
- Treatment Description: Diagnostic and therapeutic process during hospitalization, including laboratory and imaging examinations
- Admission Information: Patient’s condition and background upon admission (e.g., reason for admission, symptoms, vital signs)
- Present Illness: Onset and progression of current disease, including symptom duration, characteristics, aggravating or relieving factors
- Past History: History of previous illnesses, treatments, surgeries, or transfusions
- Chief Complaint: Main symptoms reported at admission
- Discharge Diagnosis: Final diagnoses at discharge
- Discharge Medications: List of prescribed medications at discharge (empty in the development and test sets)

### 3. Data Example
~~~
{
"Patient ID": 2,
"Visit ID": "2-1",
"Gender": "Female",
"Date of Birth": "1940-12",
"Ethnicity": "Han",
"BMI": 27.3,
"Visit Time": "2015-03",
"Treatment Description": "Urine ketone: +, WBC: 250/μl. After oral rehydration, repeat urinalysis: WBC negative. Meal tolerance test showed HbA1c ...",
"Admission Information": "Chief complaint: 'Thirst, polyuria, and poor glycemic control for 2 months.' On admission: T36.6℃, P76 bpm, BP160/80 mmHg ...",
"Present Illness": "Five years ago, patient developed thirst and polyuria without clear cause, diagnosed with fasting glucose 16.7 mmol/l, treated with metformin, repaglinide, and acarbose ...",
"Past History": "No history of coronary heart disease, hepatitis, tuberculosis, malaria, allergies, trauma, surgery, or transfusion.",
"Chief Complaint": "Thirst, polyuria, and poor glycemic control for 2 months.",
"Discharge Diagnosis": ["Type 2 diabetes mellitus", "Diabetic ketosis", "Urinary tract infection", "Macrovascular complications", ...],
"Discharge Medications": ["Acarbose", "Repaglinide", "Rosuvastatin", "Telmisartan", "Amlodipine", "Calcium Carbonate"]
}
~~~

## Evaluation Metrics
The evaluation uses Jaccard and F1-score as the primary metrics. Detailed formulas are available on the evaluation website.

## Baseline System
The baseline system is based on LoRA fine-tuning of the GLM4-9B-Chat model using the training dataset.

## Result Submission
### 1. Submission Method
The competition includes two phases:

- Leaderboard A (Development Phase): Teams can download training and development data from the Tianchi platform to train and fine-tune models. Results are submitted online for preliminary evaluation. Scores in this phase are for development only and do not count toward final rankings.

- Leaderboard B (Final Phase): Teams download the test set and submit final predictions.
The highest score achieved during the B leaderboard phase determines the final ranking and awards.

**Submission Rules**

- Each team may submit up to 3 results per day.
- Leaderboards are updated hourly and ranked in descending order of evaluation metrics.
- Failed submissions do not count toward the daily limit.

### 2. Submission Format
Both Leaderboard A and B submissions must be in UTF-8 encoded JSON format:
~~~
[
  {"ID": "1-1", "prediction": ["Drug A", "Drug B", ...]},
  {"ID": "1-2", "prediction": ["Drug C", "Drug D", ...]}
]
~~~

Fields:
- ID: Visit ID

- prediction: List of predicted medications (must match the candidate drug list)




## Organizers
- ### Institutions

**Dalian University of Technology**  Ling Luo, Jian Wang, Yuanyuan Sun, Hongfei Lin
**The Second Affiliated Hospital of Dalian Medical University**  Yan Jiang, Fan Wang, Ping Zhang, Huiyi Lv

- ### Contacts

Juntao Li (juntaoli@mail.dlut.edu.cn),
Haobin Yuan (yhhhhb@mail.dlut.edu.cn)

- ### Official Website

Tianchi Platform: https://tianchi.aliyun.com/competition/entrance/532411



## Dataset Paper and Citation

If you use this dataset, please cite as follows:
```
@article{CDrugRed,
  title={CDrugRed: A Chinese Drug Recommendation Dataset for Discharge Medications in Metabolic Diseases},
  author={Juntao Li and Haobin Yuan and Ling Luo and Yan Jiang and Fan Wang and Ping Zhang and Huiyi Lv and Jian Wang and Yuanyuan Sun and Hongfei Lin},
  year={2025},
  archivePrefix={arXiv},
  url={https://arxiv.org/abs/2510.21084}
}
```