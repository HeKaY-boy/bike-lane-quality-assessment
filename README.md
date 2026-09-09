# 5ARE0 Assignment 1 — Assessing Bicycle Lane Quality Using Smartphone Sensor Data

## 1. Project Overview

This group assignment develops a data science pipeline to determine whether a bicycle lane is **smooth** or **bumpy** using smartphone sensor data.

The project uses smartphone motion sensors to collect data while participants cycle on representative smooth and bumpy bicycle lanes. The collected data will be cleaned, transformed into meaningful features, used to train supervised and unsupervised models, and finally evaluated on an independent external dataset.

**Course:** 5ARE0  
**Academic Year:** 2026–2027  
**Assignment:** Assignment 1  
**Deadline:** October 4, 2026, 20:00  
**Group:** Group X

---

## 2. Assignment Goal

The main goal is to create a reproducible data science pipeline that can automatically assess bicycle-lane quality.

### Main task

Classify bicycle-lane sections as:

- **Smooth**
- **Bumpy**

The assignment requires both:

1. **Supervised learning:** train four supervised models.
2. **Unsupervised learning:** train four unsupervised models.

The final goal is to select the best-performing model and use it on an **independent external dataset** supplied by the instructors. The external dataset must not be used for training or testing.

---

## 3. Data Collection

### Participants

Each group consists of 3 students and recruits 2–3 participants.

Participants must:

- Know how to bike.
- Be part of course 5ARE0.
- Belong to the same assignment group.

Participants who cannot safely bike because of a medical condition or who do not know how to bike must not participate.

### Smartphone Sensors

Use the **Sensor Logger** app with:

- Accelerometer
- Gyroscope
- Gravity sensor

All other sensors should be turned off.

### Sensor Configuration

- Sampling rate: **100 Hz**
- Standardisation option: **enabled**
- Phone placement: consistent across all trials

The phone should be secured consistently, for example in a tight pocket, armband, or waistband. The exact placement strategy must be documented because phone orientation affects interpretation of the sensor signals.

### Cycling Conditions

#### Smooth lane

A typical red cycling lane without imperfections should be used.

#### Bumpy lane

Use a commonly used cycling lane with noticeable but safe imperfections such as:

- Small potholes
- Cracks
- Uneven surfaces
- Other typical rough features

Avoid dangerous or extreme road conditions.

### Recording Procedure

1. Configure Sensor Logger.
2. Start recording.
3. Place/secure the phone in the standardized location.
4. Cycle along the selected lane.
5. Stop cycling.
6. Take out the phone.
7. Stop recording.
8. Save and label the recording appropriately.

The group must decide and document:

- Recording duration
- Number of recordings
- Locations
- Experimental design choices

---

## 4. Data Management

The dataset should be organized consistently and reproducibly.

Recommended structure:

```text
data/
├── raw/
│   ├── participant_01/
│   ├── participant_02/
│   └── participant_03/
├── processed/
└── external/
```

Raw and processed data should be kept separate.

Files should have consistent names and timestamps. Participant data should be anonymized.

**Important:** The external dataset must remain completely separate from training and testing. It is only used after finalizing the models for deployment.

---

## 5. Data Science Pipeline

The notebook should implement the complete pipeline:

```text
Data Collection
      ↓
Data Loading
      ↓
Data Understanding / EDA
      ↓
Data Quality Assessment
      ↓
Preprocessing
      ↓
Windowing
      ↓
Feature Engineering / Extraction
      ↓
Feature Selection
      ↓
Train / Validation / Test
      ↓
Supervised Models (4)
      ↓
Unsupervised Models (4)
      ↓
Model Evaluation & Comparison
      ↓
Select Optimal Model
      ↓
External Dataset Deployment
      ↓
Smooth vs Bumpy Road Visualization
```

---

## 6. Data Preprocessing

Use preprocessing techniques taught during the course.

The preprocessing stage should investigate and document issues such as:

- Missing values
- Invalid or corrupted observations
- Sensor inconsistencies
- Outliers
- Signal quality
- Differences between recordings
- Differences caused by phone orientation/placement

Visualization should be used to understand the sensor signals and guide preprocessing decisions.

Every preprocessing decision should have a clear justification.

---

## 7. Feature Engineering and Extraction

Because the sensor data is time-series data, a **windowing strategy** must be considered.

The raw accelerometer, gyroscope, and gravity signals should be transformed into meaningful features.

Potential feature categories should be based on techniques taught in the course.

The project should also include **feature selection** to identify the features that are most discriminative for distinguishing smooth and bumpy lanes.

Document:

- Window size
- Window overlap
- Extracted features
- Feature-selection method
- Selected features
- Reasoning behind the choices

---

## 8. Supervised Learning

Train **four supervised models** using methods covered in the course before the assignment deadline.

For each model, document:

- Model name
- Why it is suitable
- Hyperparameters
- Training procedure
- Validation strategy
- Performance
- Strengths and limitations

The models should ultimately be compared using appropriate evaluation metrics.

---

## 9. Unsupervised Learning

Train **four unsupervised models** using methods covered in the course.

For each model, document:

- Model name
- Why it is suitable
- Hyperparameters
- How clusters/results are interpreted
- Performance/evaluation approach
- Strengths and limitations

The unsupervised approach should be meaningfully compared with the supervised approach.

---

## 10. Model Comparison

The assignment requires comparison of supervised and unsupervised approaches.

Discuss:

### Effectiveness
Which approach performs better and under what conditions?

### Advantages and limitations
Compare the strengths and weaknesses of both approaches.

### Use cases
When would supervised learning be preferred?  
When would unsupervised learning be preferred?

### Optimal model
Select **one final model** as the optimal model.

The choice should be justified using:

- Problem suitability
- Dataset size
- Feature complexity
- Interpretability
- Computational efficiency
- Performance

Also identify the **optimal features** based on the feature-selection techniques used.

---

## 11. Evaluation

The group can choose evaluation metrics as long as they are appropriate for the task.

The analysis should include useful visualizations such as:

- Exploratory data analysis plots
- Raw/processed sensor signals
- Preprocessing visualizations
- Feature-selection plots
- Model performance tables
- Confusion matrices where appropriate
- Other relevant plots

The evaluation should clearly show how the models compare.

Also analyze:

- Classification errors
- Failure cases
- Possible reasons for incorrect predictions
- Limitations of the dataset and methodology

---

## 12. External Dataset Deployment

After all models have been finalized:

1. Select the optimal model.
2. Apply the finalized preprocessing pipeline.
3. Apply the finalized feature-engineering pipeline.
4. Apply the selected features.
5. Run the model on the independent external dataset.
6. Assess the bicycle-lane quality.
7. Create a visualization showing which road sections are:
   - Smooth
   - Bumpy

**The external dataset must not be used for training or model selection.**

---

## 13. CRISP-DM Report Structure

The report should follow the **CRISP-DM framework** and be no longer than **8 pages**.

### 1. Business / Objective Understanding

Explain:

- Problem definition
- Why bicycle-lane quality matters
- Objective of the project

### 2. Data Understanding

Explain:

- Dataset characteristics
- Data-collection methodology
- Exploratory data analysis
- Key observations
- Data-quality issues
- Limitations

### 3. Data Preparation

Explain:

- Preprocessing pipeline
- Reasons for preprocessing choices
- Feature engineering
- Feature extraction
- Feature selection

### 4. Modeling

Explain:

- Four supervised approaches
- Four unsupervised approaches
- Hyperparameter tuning
- Model-selection rationale
- Comparison methodology

### 5. Evaluation

Explain:

- Evaluation metrics
- Validation strategy
- Model comparison
- Classification errors
- Failure modes

### 6. Deployment Considerations & Recommendations

Discuss:

- Practical real-world implementation
- Mobile/real-time feasibility
- Limitations
- Potential improvements
- Future work
- Potential applications

---

## 14. Repository / ZIP Structure

The final submission should be a single ZIP archive:

```text
groupX_submission.zip
│
├── groupX.ipynb
├── groupX_Report.pdf
├── README.md
│
└── data/
    ├── raw/
    ├── processed/
    └── external/
```

The exact filename should follow the submission instructions provided by the course.

---

## 15. Notebook Requirements

The notebook must:

- Execute end-to-end.
- Contain all project code inside the notebook.
- Not import custom `.py` files.
- Use structured Markdown sections.
- Include data loading.
- Include preprocessing.
- Include feature engineering.
- Include feature selection.
- Train models.
- Evaluate models.
- Select the final model.
- Perform deployment on the external dataset.
- Be executed before submission.

At the top of the notebook include:

- Python version
- Required package names
- Package versions

Only use Python packages that were used during the course instruction sessions.

### Code quality

Use:

- Meaningful variable names
- Clear structure
- Comments where useful
- Markdown explanations
- Clearly separated project stages

The notebook should explain the methodology and rationale behind important decisions.

---

## 16. Reproducibility Checklist

Before submission, verify:

- [ ] Notebook runs from beginning to end.
- [ ] All required data is included.
- [ ] No missing custom `.py` files.
- [ ] Required packages are documented.
- [ ] Package versions are documented.
- [ ] Random seeds are fixed where appropriate.
- [ ] Raw and processed data are separated.
- [ ] Data files have consistent names.
- [ ] Participants are anonymized.
- [ ] External dataset is not used for training/testing.
- [ ] Final model can run on the external dataset.
- [ ] All important figures are generated by the notebook.
- [ ] Notebook is saved in executed form.

---

## 17. Report Checklist

- [ ] Maximum 8 pages.
- [ ] CRISP-DM structure followed.
- [ ] Objective clearly explained.
- [ ] Data collection explained.
- [ ] EDA included.
- [ ] Data-quality assessment included.
- [ ] Preprocessing explained and justified.
- [ ] Feature engineering explained.
- [ ] Feature selection explained.
- [ ] 4 supervised models included.
- [ ] 4 unsupervised models included.
- [ ] Hyperparameters documented.
- [ ] Validation strategy explained.
- [ ] Evaluation metrics justified.
- [ ] Model comparison included.
- [ ] Optimal model selected.
- [ ] Optimal features identified.
- [ ] Errors/failure modes discussed.
- [ ] External-data deployment discussed.
- [ ] Limitations and future work included.

---

## 18. Ethical and Privacy Requirements

All participants must provide informed consent.

During data collection:

- Prioritize participant safety.
- Stop a trial if discomfort or injury risk occurs.
- Keep sensor data anonymous.
- Use the data only for the educational assignment.
- Ensure all participants understand the collection and analysis procedure.

Raw data should be deleted after the course has been completed and the final grade has been assigned.

---

## 19. Project Plan

### Phase 1 — Data Collection
- Finalize participants.
- Select smooth and bumpy lanes.
- Standardize phone placement.
- Configure Sensor Logger.
- Collect recordings.
- Label and organize raw data.

### Phase 2 — Data Understanding
- Load all recordings.
- Inspect sensor signals.
- Check sampling rate.
- Visualize recordings.
- Check data quality.
- Understand differences between smooth and bumpy recordings.

### Phase 3 — Preprocessing
- Clean the data.
- Handle missing/invalid values.
- Decide how to handle outliers.
- Standardize/normalize where appropriate.
- Define the windowing strategy.

### Phase 4 — Feature Engineering
- Extract meaningful time-series features.
- Build the feature dataset.
- Visualize feature distributions.
- Apply feature-selection techniques.

### Phase 5 — Modeling
- Train 4 supervised models.
- Train 4 unsupervised models.
- Tune relevant hyperparameters.
- Evaluate all models consistently.

### Phase 6 — Model Selection
- Compare all approaches.
- Select the optimal model.
- Select the optimal features.
- Document the reasoning.

### Phase 7 — Deployment
- Load the external dataset.
- Apply the finalized pipeline.
- Predict smooth/bumpy sections.
- Create the required road-quality visualization.

### Phase 8 — Final Submission
- Complete notebook.
- Write the CRISP-DM report.
- Finalize README.
- Check reproducibility.
- Create the ZIP.
- Submit to Canvas before the deadline.

---

## 20. Important Assignment Constraints

- The project must use smartphone sensor data.
- Sensors: accelerometer, gyroscope, gravity.
- Sampling rate: 100 Hz.
- Standardisation must be enabled.
- Four supervised models are required.
- Four unsupervised models are required.
- External data must not be used for training/testing.
- The final model must be deployed on the external dataset.
- The notebook must run end-to-end.
- Do not use Python packages outside those used during instruction sessions.
- The report must follow CRISP-DM.
- The report maximum is 8 pages.
- Final submission is one ZIP archive.
- Submission deadline: **October 4, 2026, 20:00**.
