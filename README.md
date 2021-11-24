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

![bar distribution](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/histogram_icu_class.png)

### Window Intervals, ICU = 1 Distribution by patient number

![window icu bar chart](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/window_icu_histogram.png)

## C. DATA ANALYSIS

### Preparatory Data Analysis

* **Data Dropping**
  * **Column Uniqueness:** Remove the duplicate columns
  * **Row Uniquness :** Change the all columns by patient number, Drop patient rows when ICU = 1 at Windows 0-2. (We cannot use in the modelling part.)
  * **Drop - Illogical rows:** There is no illogical columns
  * **Drop Null-Target rows:** Drop the 199 patient ID information
* **Data Splitting (Train / Test) :**
* **Outlier Handling :** The data set scaled before. So we don't have to do anything.
* **Missing Data Handling :** Fill all NaN variales bu using ffill and bfill method.
* **Feature Engineering**  

### Exploratory Data Analysis

* **Visualizations After Preparatory Data Analysis**
  * Age Percentile by patients
    * ![age Percentile by patients](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/age_percentil_before.png)
  * ICU Distribution by Window Intervals
    * ![icu distribution by window intervals](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/patient_event_widnow_icu.png)
  * Does Age, Disease Groping influence taking the patient to an ICU bed?
    * ![age disease groping icu](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/ages_disease_grouping_icu_2.png)

* **Visualizations for Specific Features After Preparatory Data Analysis**
  * Time-Variant Features (Max)
    * ![max](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/time_variant_groups_max_after.png)
  * Time-Variant Features (Min)
    * ![max](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/time_variant_groups_min_after.png)

## D. DATA MODELLING

### WINDOW 1 (0-2 Hours)

#### Data Modelling Process for Window 1

* Preprocessing Data → Retrieve all data of the patient according to the 0-2 hour interval
* Correlations → Identifying importances features that affect ICU value in the 0-2 hour range
  * Respiratory Rate is the most important feature.
* Feature Encoding → Handling categorical features
* Data Modelling
  * KNN → Accuracy: %74
* Random Forest Classifier →  Accuracy : %78

![window 1 auc score](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/windows%20-1%20auc%20score.png)

### WINDOW 2-3 (2-6 HOURS)

#### Data Modelling Process for Window 2-3

* Preprocessing Data → Retrieve all data of the patient according to the 2-6 hour interval | Removing the patients where ICU = 1 in Window 1 to prevent the bias
* Correlations → Identifying importances features that affect ICU value in the 2-6 hour range
  * Respiratory Rate is the most important feature.
* Feature Encoding → Handling categorical features
* Data Modelling
  * KNN → Accuracy: %72
* Random Forest Classifier →  Accuracy : %84

![window 1 auc score](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/window%202-3%20acu%20score.png)

### WINDOW 4-5 (ABOVE 6 HOURS)

#### Data Modelling Process for Window 4-5

* Preprocessing Data →  Retrieve all data of the patient above 6 hours | Removing the patient where ICU = 1 between 0 - 6 Hours to prevent the bias
* Correlations → Identifying importances features that affect ICU value above 6 hours
  * Respiratory Rate is the most important feature.
* Feature Encoding → Handling categorical features
* Data Modelling
  * KNN → Accuracy: %96
* Random Forest Classifier →  Accuracy : %98

![window 1 auc score](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/window%204-5%20auc%20score.png)

## E. MODEL EVALUATION

* Random Forest gave better results than KNN.
* Random Forest Classifier models also gave equal results with RFC tuned models.
* As the number of patients admitted to the intensive care unit increased as time progressed, the accuracy result increased accordingly.
* The most important factor in the possibility of being admitted to the intensive care unit is the respiratory rate of the person.

![auc scores by model and window intervals](https://github.com/edaaydinea/Estimating-the-Probability-of-Confirmed-COVID-19-Cases-Taking-into-the-Intensive-Care-Unit-ICU-/blob/main/auc%20score%20by%20model%20and%20widnow%20intervals.png)

## F. RESOURCES

### **Notebook Resources**

* Dataset: [COVID-19 - ICU Dataset](https://www.kaggle.com/Sírio-Libanes/covid19)
* [https://www.kaggle.com/andrewmvd/enriched-lightgbm-pr-86-auc-92-68](https://www.kaggle.com/andrewmvd/enriched-lightgbm-pr-86-auc-92-68)
* [https://www.kaggle.com/souhardyaganguly/covid-icu-admission-predict-xgboost-90](https://www.kaggle.com/souhardyaganguly/covid-icu-admission-predict-xgboost-90)
* [https://www.kaggle.com/felipeoliveiraml/stacking-gradient-boosting-pr-80](https://www.kaggle.com/felipeoliveiraml/stacking-gradient-boosting-pr-80)
* [https://www.kaggle.com/harriwashere/task-1-eda-3-model-ensemble](https://www.kaggle.com/harriwashere/task-1-eda-3-model-ensemble)
* [https://www.kaggle.com/felipeveiga/starter-covid-19-sirio-libanes-icu-admission](https://www.kaggle.com/felipeveiga/starter-covid-19-sirio-libanes-icu-admission)
* [https://www.kaggle.com/mpwolke/covid19-diagnosis-learning-curves](https://www.kaggle.com/mpwolke/covid19-diagnosis-learning-curves)
* [https://www.kaggle.com/epdrumond/icu-admission-data-classification-model#1.-Import-Libraries](https://www.kaggle.com/epdrumond/icu-admission-data-classification-model#1.-Import-Libraries)
* [https://www.kaggle.com/epdrumond/icu-admission-data-cleaning-and-exploration/notebook](https://www.kaggle.com/epdrumond/icu-admission-data-cleaning-and-exploration/notebook)

### **Website Resources**

* ***Stackoverflow***
  * [https://stackoverflow.com/questions/55567706/plot-all-pandas-dataframe-columns-separately](https://stackoverflow.com/questions/55567706/plot-all-pandas-dataframe-columns-separately)
  * [https://stackoverflow.com/questions/50185926/valueerror-shape-of-passed-values-is-1-6-indices-imply-6-6](https://stackoverflow.com/questions/50185926/valueerror-shape-of-passed-values-is-1-6-indices-imply-6-6)
  * [https://stackoverflow.com/questions/62476253/how-to-show-seaborn-countplot-and-print-dataframe-side-by-side-in-python](https://stackoverflow.com/questions/62476253/how-to-show-seaborn-countplot-and-print-dataframe-side-by-side-in-python)
  * [https://stackoverflow.com/questions/22086116/how-do-you-filter-pandas-dataframes-by-multiple-columns](https://stackoverflow.com/questions/22086116/how-do-you-filter-pandas-dataframes-by-multiple-columns)
  * [https://stackoverflow.com/questions/21720022/find-all-columns-of-dataframe-in-pandas-whose-type-is-float-or-a-particular-typ](https://stackoverflow.com/questions/21720022/find-all-columns-of-dataframe-in-pandas-whose-type-is-float-or-a-particular-typ)
  * [https://stackoverflow.com/questions/47815140/check-if-multiple-columns-exist-in-a-df](https://stackoverflow.com/questions/47815140/check-if-multiple-columns-exist-in-a-df)

* ***Pandas Seaborn Documentations***
  * [https://pandas.pydata.org/pandas-docs/stable/reference/](https://pandas.pydata.org/pandas-docs/stable/reference/)
  * [https://pandas.pydata.org/pandas-docs/stable/user_guide/index.html](https://pandas.pydata.org/pandas-docs/stable/user_guide/index.html)
  * [https://seaborn.pydata.org/tutorial.html](https://seaborn.pydata.org/tutorial.html)
  * [https://seaborn.pydata.org/api.html](https://seaborn.pydata.org/api.html)

* ***GeeksforGeeks***
  * [https://www.geeksforgeeks.org/append-extend-python/](https://www.geeksforgeeks.org/append-extend-python/)
  * [https://www.geeksforgeeks.org/how-to-plot-multiple-data-columns-in-a-dataframe/](https://www.geeksforgeeks.org/how-to-plot-multiple-data-columns-in-a-dataframe/)
  * [https://www.geeksforgeeks.org/different-ways-to-create-pandas-dataframe/](https://www.geeksforgeeks.org/different-ways-to-create-pandas-dataframe/)

* ***Others***
  * [https://yigitsener.medium.com/veri-analizinde-değişkenlerin-gruba-bağlı-özelliklerini-ayrıntılı-veren-fonksiyonunun-pythonda-3e11b0fa1cc7](https://yigitsener.medium.com/veri-analizinde-değişkenlerin-gruba-bağlı-özelliklerini-ayrıntılı-veren-fonksiyonunun-pythonda-3e11b0fa1cc7)
  * [https://yigitsener.medium.com/veri-biliminde-eksik-kay%C4%B1p-verilere-yakla%C5%9F%C4%B1m-stratejileri-ve-python-pandas-uygulamas%C4%B1-501fbf643795](https://yigitsener.medium.com/veri-biliminde-eksik-kay%C4%B1p-verilere-yakla%C5%9F%C4%B1m-stratejileri-ve-python-pandas-uygulamas%C4%B1-501fbf643795)
  * [https://www.delftstack.com/howto/seaborn/size-of-seaborn-heatmap/](https://www.delftstack.com/howto/seaborn/size-of-seaborn-heatmap/)
  * [https://datacarpentry.org/sql-ecology-lesson/02-sql-aggregation/index.html](https://datacarpentry.org/sql-ecology-lesson/02-sql-aggregation/index.html)
  * [https://datatofish.com/select-rows-pandas-dataframe/](https://datatofish.com/select-rows-pandas-dataframe/)
  * [https://www.tutorialspoint.com/how-to-add-percentages-on-top-of-bars-in-seaborn-using-matplotlib](https://www.tutorialspoint.com/how-to-add-percentages-on-top-of-bars-in-seaborn-using-matplotlib)
  * [https://pbpython.com/groupby-agg.html](https://pbpython.com/groupby-agg.html)
  * [https://machinelearningmastery.com/roc-curves-and-precision-recall-curves-for-classification-in-python/](https://machinelearningmastery.com/roc-curves-and-precision-recall-curves-for-classification-in-python/)

* **Book Resouces**
  * Hands-on Machine Learning with Scikit-Learn, keras & Tensorflow
  * Introduction to Machine learning
  * Data Science from Scratch
  * Python for Data Science Handbook
  * Practical Statistics for Data Scientists
  * Python for Data Analysis
  * Fundamentals of Data Visualization
