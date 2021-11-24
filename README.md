# Estimating the Probability of Confirmed COVID-19 Cases Taking into the Intensive Care Unit (ICU)

This repository includes the slides and coding parts for this project.

This project is carried out by *Eda AYDIN, Zilan EROL* under the supervision of *Engin Deniz ALPMAN* in the **[Data Science for the Public Good program](https://www.kodluyoruz.org/bootcamp/data-science-for-the-public-good-istanbul-ankara/)**

The dataset of this project is obtained from the [Kaggle - COVID-19 - Clinical Data to assess diagnosis](https://www.kaggle.com/Sírio-Libanes/covid19)

Note:  The data sets to be used in the project comply with the health-ethical rules and are suitable for use as a license.

## A. BUSINESS UNDERSTANDING

> **Business Goal Declaration**

The COVID-19 pandemic has caused us to rethink the organization of the health system, as it affects the whole world about the inadequacy of the health system.

Some of the sentences we hear every day due to the increasing cases are

* **“The occupancy of the intensive care unit is increasing”**,
* **“The intensive care units are full.”**

pioneered this project.

Based on these sentences, in this project, it will be determined whether the COVID-19 patient needs to be treated in the intensive care unit to preserve the health services system capacity.

We have two purposes here.

1. Our first purpose is to give the most accurate answer to tertiary hospitals based on the available data, based on the patient's need for intensive care support. In this way, intensive care resources can be organized or patient transfer can be planned.
2. Our other purpose is to provide an accurate answer to local and temporary hospitals based on subsampling of widely available data and not needing intensive care support. Thus, physicians fighting on the front line can safely discharge patients and monitor them remotely.

The data sets to be used in the project comply with the health-ethical rules and are suitable for use as a license.

> **Our Business Problem**

According to our declaraton of businness goal: our aim to predict admission to the ICU of confirmed COVID-19 cases.

## B. DATA UNDERSTANDING

* This dataset consists of:
  * Patient demographic information
  * Patient previous grouped diseases
  * Blood results
  * Vital signs
    * Disalostic Blood Pressure
    * Systolic Blood Pressure
    * Heart Rate
    * Respiratory Rate
    * Temprature
    * Oxygen Saturation

---

* This dataset includes:
  * Number of rows: 1925
  * Number of inpatients : 385
  * Number of features 230 + 1(target)
  * Each paient's medical record in different window intervals are located on 5 different rows.

 ![dataset small part](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/dataset_small_part.png)

 0 stands for negative and 1 stands for positive.

* Patient with ID 1 experienced ICU admission in the first 2 hours from Hospital admission (0-2).
* Patient with ID 2 experienced ICU admission after 12 hours from Hospital admission (ABOVE_12).
* Patient with ID 11 experienced ICU admission between 6 and 12 hours from hospital admission (6 - 12)
* Patients with ID 12 did not experienced ICU admission.
* Patients with ID 14 experienced ICU admission between 4 and 6 hours from hospital admission (4 - 6)

### PATIENT - ICU - WINDOW RELATIONSHIP (CUMULATIVE)

![patient icu window relationship cumulative ](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/icu_admission_according_to_hours_window.png)

* Number of patients admitted to the ICU between:
  * 0-2 hours: 32
  * 2-4 hours: 27
  * 4-6 hours: 40
  * 6-12 hours: 31
  * above 12 hours: 65
* Number of patients who experience ICU : 195
* Number of patients who don't experience ICU: 190
* Number of patients who back to the normal stage after the admission to ICU: 0

### ICU distribution by number of patients

![]()