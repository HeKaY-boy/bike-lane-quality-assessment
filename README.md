# Bike-Lane Quality from Smartphone Sensors - 5ARE0, Assignment 1

**Group 6**

| Member | Student number |
|---|---|
| Himanshu Khartade | 2431459 |
| Aniket Zade | 2431491 |
| Yuhan Shao | 2034964 |

Classifies bike-lane segments as **smooth** or **bumpy** using smartphone accelerometer, gyroscope, and gravity data. The notebook compares four supervised models (Logistic Regression, k-NN, Random Forest, and SVC) and four unsupervised models (Agglomerative Clustering, K-Means, Fuzzy C-Means, and Gaussian Mixture), then applies Random Forest to an independent external recording.

## Contents of this submission

| File or folder | Description |
|---|---|
| `Group6.ipynb` | Executed notebook containing the complete analysis pipeline, all code, and saved outputs. |
| `group6_Report.pdf` | Data collection and analysis report following the CRISP-DM framework. |
| `README.md` | Setup instructions and dataset description. |
| `data/Smooth/P1/`, `P2/`, `P3/` | Smooth recordings, one folder per participant. |
| `data/Bumpy/P1/`, `P2/`, `P3/` | Bumpy recordings, one folder per participant. |
| `data/external_data/` | Independent external sensor recording for deployment. |

Package these files in one ZIP archive named `group6_HAR_submission.zip`.

## Requirements and Setup

1. The saved notebook records Python **3.13.5**, NumPy **2.3.5**, pandas **2.2.3**, Matplotlib **3.10.0**, and scikit-learn **1.9.0**. The group confirmed scikit-fuzzy **0.5.0**. The notebook also imports **seaborn**; its version is not printed. Jupyter and ipykernel are needed to open and run the notebook.

   ```bash
   python -m pip install numpy==2.3.5 pandas==2.2.3 matplotlib==3.10.0 scikit-learn scikit-fuzzy==0.5.0 seaborn notebook ipykernel
   ```

   The scikit-learn version is reported as recorded in the notebook. Seaborn and notebook-tool versions were not recorded. The installation command leaves these packages unpinned. All analysis code is contained in the notebook; no project `.py` files are imported.

## How to Run

1. Extract the submission and open `Group6.ipynb` in Jupyter or VS Code. Select the kernel containing the required packages. Set the working directory to the folder containing `data/`.
2. Choose **Kernel → Restart & Run All**, then save the executed notebook with its outputs. The first environment cell prints the main software versions.

**External deployment.** In the deployment section, point `load_and_merge()` to the external `Accelerometer.csv`, `Gravity.csv`, and `Gyroscope.csv`. The notebook creates a prediction timeline and prediction counts. External data are not used for training or testing, and external predictions are not ground-truth labels.

## Dataset description

**Collection.** Three participants, anonymized as **P1-P3**, each contributed a smooth and a bumpy ride. Sensor Logger recorded accelerometer, gyroscope, and gravity at a nominal **100 Hz**, with Standardisation enabled. Phones were fixed vertically on the bicycle basket. Smooth lanes had no obvious defects; bumpy lanes had noticeable but non-dangerous surface imperfections.

The six recordings contain **297,919 samples per sensor**, covering approximately **49.87 minutes**. The table below was checked directly against the repository's raw CSV files. Duration is the last minus the first `seconds_elapsed` value.

| Ride | Duration (s) | Samples per sensor | Route documented in notebook |
|---|---:|---:|---|
| P1 smooth | 332.14 | 33,176 | Geldropsedijk |
| P1 bumpy | 508.06 | 50,749 | Opwettenseweg |
| P2 smooth | 501.65 | 49,779 | Wolvendijk |
| P2 bumpy | 510.10 | 50,613 | Eisenhowerlaan |
| P3 smooth | 561.04 | 55,894 | Wolvendijk |
| P3 bumpy | 579.27 | 57,708 | Eisenhowerlaan |

**Devices and placement.**

| Participant | Phone | Placement |
|---|---|---|
| P1 | iPhone 15 | Fixed vertically on bicycle basket |
| P2 | iPhone 13 | Fixed vertically on bicycle basket |
| P3 | iPhone 17 Pro Max | Fixed vertically on bicycle basket |

**File format.** Each ride folder contains `Accelerometer.csv`, `Gravity.csv`, and `Gyroscope.csv`, which are the three files read by the notebook. Other exported CSVs are present but are not used by the analysis.

| Field | Description |
|---|---|
| `time` | Absolute measurement timestamp used to check sensor alignment. |
| `seconds_elapsed` | Seconds since recording started. |
| `x`, `y`, `z` | Sensor components in the phone's coordinate system. The notebook describes acceleration and gravity in m/s² and angular velocity in rad/s. |

The loader checks identical timestamps and equal row counts across sensors. It renames axis columns with `acc_`, `grav_`, and `gyro_` prefixes. Labels are assigned from recording metadata as the strings `smooth` and `bumpy`.

**Processing.** The notebook computes sensor magnitudes without trimming, filtering, or resampling. Windows contain **200 samples** and advance by **100 samples**: approximately two-second windows with 50% overlap. The six rides yield **2,970 windows**. Five statistics (standard deviation, mean, RMS, minimum, and maximum) are calculated for each sensor magnitude. Gravity features are dropped, leaving ten accelerometer and gyroscope features. Models use standardization and PCA retaining 95% of variance.

**Validation.** Models use a random 75%/25% split of windows, with `random_state=42`. This is not leave-one-participant-out validation. Overlapping windows from the same rides may appear in both subsets, so the scores do not establish performance on unseen riders. Agglomerative Clustering is fitted directly to the test windows; the other clustering methods fit training windows and assign test windows.

**Anonymization and ethics.** Participants are identified as P1-P3 in the analysis. Data are used exclusively for this educational assignment, with participant consent and safe cycling conditions, and should be deleted after course completion and final grading.

## Results in one paragraph

The saved supervised outputs report accuracy of 0.68 for Logistic Regression, 0.81 for k-NN, 0.83 for Random Forest, and 0.81 for SVC. Random Forest is selected for deployment, with bumpy-class F1 of 0.84 and recall of 0.88. The saved unsupervised outputs give ARI between 0.0845 and 0.0880, indicating limited agreement with the smooth/bumpy labels despite silhouette scores around 0.66-0.71. Saved external predictions contain 638 smooth and 380 bumpy windows (62.7% and 37.3%). The external data have no ground-truth labels for calculating accuracy. These window-based results should not be interpreted as evidence of generalization to new riders.
