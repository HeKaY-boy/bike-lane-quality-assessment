# Bike-Lane Quality from Smartphone Sensors — 5ARE0, Assignment 1

**Group X** — members: *fill in names and student numbers*

Classifies bike-lane segments as **smooth** or **bumpy** from smartphone accelerometer, gyroscope and gravity data
(4 unsupervised + 4 supervised models, leave-one-participant-out validation, deployment on new recordings).

## Contents of this submission

```
groupX_submission.zip
├── groupX.ipynb          Executed notebook: the complete pipeline (loading → preprocessing → features → models → deployment)
├── groupX_Report.pdf     Data collection and analysis report (CRISP-DM, 6 pages)
├── README.md             This file
├── data/
│   ├── raw/              Untouched sensor exports, anonymized: raw/<smooth|bumpy>/<P1|P2|P3>/<P#_class_run1>/{Accelerometer,Gravity,Gyroscope}.csv
│   ├── raw_excluded/     Two first-round smooth rides that were rejected and re-recorded (kept for transparency; never used for modeling)
│   └── processed/        Written by the notebook: trimmed_recordings and window_features.csv (kept separate from raw data)
└── models/               Written by the notebook: bike_lane_model.pkl (final Logistic Regression pipeline)
```

## How to run

1. Python 3.10+ recommended (tested with **3.12.3**; other recent versions of the packages should also work) and these packages (tested versions in brackets):
   `numpy` (2.4.4), `pandas` (3.0.2), `matplotlib` (3.10.8), `scikit-learn` (1.8.0), plus `jupyter`/`ipykernel` to open the notebook.
   ```
   pip install numpy pandas matplotlib scikit-learn jupyter
   ```
   No other third-party packages are used, and the notebook imports no `.py` files.
2. Unzip, open `groupX.ipynb` in Jupyter or VS Code, and make sure the **working directory is the folder that contains `data/`**
   (all paths are relative).
3. *Kernel → Restart & Run All*. Runtime is about 1-2 minutes on a laptop; all random seeds are fixed, so results reproduce.
   The notebook prints the exact Python and package versions in its first cell.

**Applying the model to the external dataset:** in Section 17 of the notebook set `EXTERNAL_FOLDER` to the folder holding the external
`Accelerometer.csv`, `Gravity.csv`, `Gyroscope.csv` (and optionally `Location.csv` for a route map) and run the remaining cells.
The external data is never used for training or testing.

## Dataset description

**Collection.** Sensor Logger app; accelerometer, gyroscope and gravity sensor only; 100 Hz; *Standardisation* on; phone carried in a pocket
while riding a continuous stretch of bike lane. *Smooth* = typical red cycling lane without imperfections; *bumpy* = commonly used lane with
noticeable, non-dangerous imperfections. 3 participants (anonymized as P1, P2, P3) × 2 conditions = **6 rides, 11.8 min, 70 204 samples per sensor**.

| Ride | Duration (s) | Samples per sensor | Recorded (UTC date) |
|---|---|---|---|
| P1 smooth | 77.3 | 7 719 | 2026-09-28 |
| P1 bumpy | 180.3 | 18 010 | 2026-09-13 |
| P2 smooth | 126.7 | 12 576 | 2026-09-28 |
| P2 bumpy | 197.1 | 19 553 | 2026-09-12 |
| P3 smooth | 47.8 | 4 763 | 2026-09-10 |
| P3 bumpy | 76.1 | 7 583 | 2026-09-12 |

**Phone / placement / bike / route:** *fill in for each participant (the notebook has a cell for this in Section 1 — keep both in sync).*

**File format.** One CSV per sensor and ride, columns `time` (Unix time, ns), `seconds_elapsed` (s since recording start), `x`, `y`, `z`.
Accelerometer in m/s², gyroscope in rad/s, gravity in m/s². The three files of a ride share identical timestamps row for row (verified by
assertions in the notebook).

**Anonymization.** Participants are P1-P3 in all files, folder names, plots and text. The app's `Metadata.csv` (contains a device ID) is not included.

**Excluded recordings.** The first smooth rides of P1 and P2 contained lane imperfections (much higher spread and peaks than genuinely smooth rides, see notebook
Section 3.2) and were re-recorded; the rejected files are in `data/raw_excluded/`.

**Ethics.** Consenting adult group members, safe lanes only, data used exclusively for this assignment and deleted after the course.

## Results in one paragraph

Leave-one-participant-out macro-F1 (train on two riders, test on the third): Logistic Regression 0.955, SVM 0.957, Random Forest 0.947, Decision Tree 0.924.
Logistic Regression is selected (statistically tied with the best, simplest and most interpretable). Best unsupervised model: Ward-linkage Agglomerative
clustering (ARI 0.86, purity 0.96, in-sample). Almost all errors occur in the first/last 10 s of rides (slow start-up / stopping, partly label noise). See the report for details.

## Before submitting (checklist for the group)

- [ ] Fill in names and student numbers (notebook title cell, report title page, this file).
- [ ] Fill in phone models, placement, bike and route information (notebook Section 1, report Section 2.1, this file), then re-run the notebook.
- [ ] Apply the model to the external dataset (notebook Section 17) and add the result and figure to the report (Section 6.1).
- [ ] Confirm with the teaching staff whether the archive must be named `groupX_submission.zip` or `groupX_HAR_submission.zip` (the assignment text uses both).
- [ ] Confirm that PCA, SelectKBest and mutual information were covered in the instruction sessions (the assignment allows only packages used there; all code uses numpy/pandas/matplotlib/scikit-learn).
- [ ] Rename `groupX` to your real group number in all file names.
