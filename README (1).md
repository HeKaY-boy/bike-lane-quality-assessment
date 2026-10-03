# Bicycle Lane Quality Assessment

**Group 6 | 5ARE0 | Assignment 1**

## Project Overview

This project was developed for Assignment 1 of 5ARE0 at Eindhoven University of Technology. We use smartphone accelerometer, gyroscope, and gravity data to classify bicycle-lane sections as **smooth** or **bumpy**. The notebook covers data loading, preprocessing, feature extraction and selection, supervised and unsupervised learning, evaluation, and deployment on an independent external recording.

This README describes the current project setup. The notebook is still being revised; final model results and processing settings will be documented in the completed notebook and report.

## Submission Contents

| File or folder | Description |
|---|---|
| `group6.ipynb` | Analysis notebook containing all analysis code. Rename the current `Main_notebook(2).ipynb` to this filename for submission. |
| `group6_Report.pdf` | Final report describing data collection, methodology, results, and limitations. To be added. |
| `data_raw/` | Raw participant recordings and the independent external recording, using the paths currently specified in the notebook. |
| `README.md` | Project description, environment setup, dataset information, and execution instructions. |

Submit the final files together as `group6_HAR_submission.zip`.

The assignment requires a `data/` folder in the final submission. Before submission, rename `data_raw/` to `data/` and update the participant and external-data paths in the notebook together. The paths below document the current code.

## Requirements and Setup

### Environment

The uploaded notebook records the following environment:

| Software | Recorded version |
|---|---|
| Python | 3.13.5, Anaconda distribution |
| pandas | 2.2.3 |
| NumPy | 2.3.5 |
| Matplotlib | 3.10.0 |
| scikit-learn | 1.9.0, as printed in the saved notebook output; verify in the final environment |
| scikit-fuzzy | 0.5.0 |
| Jupyter Notebook | Version not recorded |

The current code imports scikit-fuzzy for fuzzy clustering. The group confirmed version 0.5.0. Use only packages permitted in the course instruction sessions.

### Setup

Use the group's existing Anaconda environment if available. To create a separate environment, run these commands in Anaconda Prompt or a terminal with conda available:

```bash
conda create -n bike-lane python=3.13.5
conda activate bike-lane
python -m pip install pandas==2.2.3 numpy==2.3.5 matplotlib==3.10.0 scikit-learn scikit-fuzzy==0.5.0 notebook
```

Confirm and pin the scikit-learn and Jupyter versions after the final successful run. The command above installs these two packages without fixed versions.

Start Jupyter from the project directory:

```bash
python -m notebook
```

Select the Python kernel belonging to the environment where the dependencies were installed. The notebook's environment cell prints the Python and main package versions.

## Dataset Description

### Data Collection

Three group members, identified as **P1**, **P2**, and **P3**, each contributed one smooth recording and one bumpy recording to the dataset loaded by the current notebook. Data were collected using Sensor Logger with the accelerometer, gyroscope, and gravity sensor enabled. The notebook documents a nominal sampling rate of **100 Hz** and the Standardisation option enabled.

Phones were placed vertically on the bicycle basket, as documented in the notebook. The exact fastening method should be described in the final report.

- **Smooth:** a typical red cycling lane without noticeable surface imperfections.
- **Bumpy:** a commonly used cycling lane with noticeable imperfections such as cracks, small potholes, or uneven surfaces.

Labels are assigned from the recording metadata and folder organization. They are stored as the strings `smooth` and `bumpy`, rather than read from a label column in each raw sensor CSV.

### Devices

| Participant | Phone | Documented placement |
|---|---|---|
| P1 | iPhone 15 | Vertical on bicycle basket |
| P2 | iPhone 13 | Vertical on bicycle basket |
| P3 | iPhone 17 Pro Max | Vertical on bicycle basket |

### Recording Summary

The following values are taken from the notebook’s saved data-loading output. They have not been independently recalculated from the raw CSVs. The reported time is the maximum `seconds_elapsed` value before trimming. Update this table if the recordings change.

| Recording | Samples per sensor file | Reported time (seconds) | Approximate time (minutes) |
|---|---:|---:|---:|
| P1 smooth | 33,176 | 332.2 | 5.54 |
| P1 bumpy | 50,749 | 508.1 | 8.47 |
| P2 smooth | 49,779 | 501.8 | 8.36 |
| P2 bumpy | 50,613 | 510.2 | 8.50 |
| P3 smooth | 55,894 | 561.1 | 9.35 |
| P3 bumpy | 57,708 | 579.3 | 9.66 |

The current notebook contains three smooth recordings with different lengths. Recording counts describe the files used in the analysis, not all trials originally collected.

### Sensor Files and Fields

Each participant-condition folder is expected to contain:

| File | Measurements |
|---|---|
| `Accelerometer.csv` | Acceleration along the phone's x, y, and z axes |
| `Gyroscope.csv` | Angular velocity around the phone's x, y, and z axes |
| `Gravity.csv` | Gravity components along the phone's x, y, and z axes |

The current loader expects these columns in each CSV:

| Column | Description | Unit or format |
|---|---|---|
| `time` | Measurement timestamp, used to verify alignment across sensors | Confirm timestamp encoding in the raw CSV |
| `seconds_elapsed` | Time elapsed since recording began | Seconds |
| `x`, `y`, `z` in Accelerometer.csv | Acceleration components in phone coordinates | Confirm export units and whether gravity is included |
| `x`, `y`, `z` in Gyroscope.csv | Angular velocity components in phone coordinates | Confirm export units |
| `x`, `y`, `z` in Gravity.csv | Gravity components in phone coordinates | Confirm export units |

After loading, sensor-axis columns are renamed to `acc_x`, `acc_y`, `acc_z`, `gyro_x`, `gyro_y`, `gyro_z`, `grav_x`, `grav_y`, and `grav_z`. The current loader requires equal row counts and exactly matching `time` columns across the three sensor files. Phone axes should not automatically be interpreted as road-relative directions.

### Data Organization

| Current folder | Contents |
|---|---|
| `data_raw/Smooth/P1/` | P1 smooth sensor CSVs |
| `data_raw/Smooth/P2/` | P2 smooth sensor CSVs |
| `data_raw/Smooth/P3/` | P3 smooth sensor CSVs |
| `data_raw/Bumpy/P1/` | P1 bumpy sensor CSVs |
| `data_raw/Bumpy/P2/` | P2 bumpy sensor CSVs |
| `data_raw/Bumpy/P3/` | P3 bumpy sensor CSVs |
| `data_raw/` | External `Accelerometer.csv`, `Gravity.csv`, and `Gyroscope.csv`, as currently expected by the external-data loader |

Raw exports should remain unchanged. Any processed files saved by the final notebook should be stored separately and their location documented here.

### External Dataset

An independent external recording is provided for deployment. It must not be used for training, testing, hyperparameter tuning, or model selection. After model selection is complete, the selected model is applied to windows of this recording to visualize predicted smooth and bumpy sections over time. Predictions should not be described as ground-truth labels.

## How to Run

1. Extract the complete submission archive before opening the notebook.
2. Keep the notebook in the project directory alongside the data folder.
3. Confirm that the participant folders and external sensor files match the paths above. Folder names and capitalization must match the notebook.
4. Activate the Python environment and launch Jupyter from the project directory using `python -m notebook`.
5. Open the notebook and select the appropriate Python kernel.
6. Choose **Restart Kernel and Run All Cells**, or the equivalent option in your notebook interface.
7. Review the environment output and check that all cells complete successfully.
8. Save the executed notebook with its outputs before submission.

The current notebook uses relative paths, so no personal absolute paths should be necessary when the documented folder structure is preserved. If the folder structure is changed, update both the `recordings` dictionary and the external-data loading cell.

**Before submission:** confirm package versions and sensor units, update the data paths and submission filenames, and run the completed notebook from a clean kernel. The current revision has not been independently verified end-to-end.
