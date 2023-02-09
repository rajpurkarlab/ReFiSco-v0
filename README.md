# ReFiSco-v0
Report Fix and Score (ReFiSco) Dataset for Radiology Reports -- Preliminary Version (v0)

ReFiSco-v0 is a derivative dataset created from a very small subset of MIMIC-CXR, we have obtained permission from PhysioNet to host it. Please do not reshare without permission. 

## Expert Evaluation Study
We analyze the quality of X-REM compared to a machine learning baseline and a human benchmark through a human expert evaluation study. The human evaluation supplements evaluation through traditional quantitative metrics with additional clinical context. 

We conduct the human evaluation on a subset of 60 studies from MIMIC-CXR and recruit four radiologists to provide evaluations. For each study image, we compile three reports: one generated from our method ([X-REM](https://github.com/rajpurkarlab/X-REM)), one generated from a machine learning baseline (CXR-RePaiR) trained on the same MIMIC-CXR training set without the 60 samples, and one taken from a human benchmark (MIMIC-CXR). To each radiologist, we present one image and one report for each of the 60 studies. Each report is randomly and independently chosen from one of the three sources. The radiologist is blinded to the source. We ask each radiologist to assess the error severity of their assigned reports.

## Data Collection Details
Participants: We recruited 4 practicing radiologists to annotate these reports. After informed consent, these radiologists were given instructions and a 30 minute orientation to describe the task. 

Data: For this study, we randomly selected a subset of 60 studies from the MIMIC-CXR dataset with (i) a single frontal view and (ii) no references to prior examinations. For each study, we collected 3 reports: one generated from our method (X-REM), one generated from a baseline model (CXR-Repair), and one written by a human radiologist (taken from MIMIC-CXR). 

Study: For each radiologist, we presented one frontal chest x-ray and one report for each of the 60 studies. Each report was randomly and independently chosen from the CXR-Refuse, CXR-Repair, or MIMIC-CXR source. The radiologist was blind to the source of the report.

Task: The radiologist was asked to review the report for each image. They are asked to mark each line of the report with one of 5 error categories based on ACR’s RADPEER program for peer review and the ACR’s Actionable Reporting Work Group document.  In increasing order of severity, the categories are 'No error', 'Not actionable', 'Actionable nonurgent error', 'Urgent error', or 'Emergent error'. Moreover, the radiologist is asked to correct each error using either deletion, substitution, or insertion of a line. (Note: comparison to prior was a non-actionable error.) Their instructions are [here](https://docs.google.com/document/d/1Xkg7MblXJLvIx0-vf9llyMjE7GNP5-IuzEL-wBzvax8/edit?usp=sharing).

## Dataset
The dataset is released in [refisco-v0.ipynb](refisco-v0.csv). Each row represents one line of a report, and the lines for the same id, annotator, and source make up one annotation. The impression_original column contains the original text from the source report. If impression_original is blank for a row, then the row represents an insertion. In the impression_edited column, [no edit] represents no change, [delete] represents deleting the line, and text represents subsitution or insertion. 

## Analysis
We convert the error categories to scores 0-4, with 4 being the most severe. Then, we aggregate the error across lines of the report using maximum error severity (MES) and average error severity (AES). We found that the mean MES for X-REM, CXR-Repair, and MIMIC-CXR were 2.11, 2.26, and 1.58. The mean AES were 1.76, 2.42, and 1.47. The analysis is done in [Data_Analysis.ipynb](Data_Analysis.ipynb).