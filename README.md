# EEG Motor Imagery Classification: Right Hand vs. Right Foot
This project implements **EEG-based motor imagery classifiers** to distinguish between **right-hand and right-foot** motor imagery tasks using the **BCI Competition III Dataset IVa**. The implementation explores two complementary methodologies:

* **Subject-Specific Modeling:** Independent pipelines using **Common Spatial Patterns (CSP)** and **Linear Discriminant Analysis (LDA)** for five individual participants.
* **Cross-Subject Learning:** A unified approach leveraging **Filter Bank CSP (FBCSP)** to address inter-subject variability and enable generalized classification.

## Neurophysiological Background

Motor imagery elicits **Event-Related Desynchronization (ERD)** in sensorimotor rhythms:
* **Right hand imagery:** Strongest ERD in **contralateral left hemisphere** (C3 electrode)
* **Right foot imagery:** Strongest ERD in **midline central region** (Cz electrode)

These spatial patterns form the physiological basis for CSP-based feature extraction.

## Problem Overview

**Motor imagery (MI)** brain–computer interfaces rely on detecting task-specific modulations in **sensorimotor EEG rhythms**. These modulations typically occur in the **mu (8–13 Hz)** and **beta (13–30 Hz)** bands over motor cortex regions.

This project formulates MI decoding as a **binary classification problem**:

* **Class 1:** Right hand motor imagery
* **Class 2:** Right foot motor imagery

## Dataset

* **Dataset:** BCI Competition III – Dataset IVa
* **Subjects:** 5
* **Paradigm:** Cue-based motor imagery
* **Recording modality:** EEG
* **Channels:** 118 (arranged according to the international 10-20 system)
* **Sampling rate:** 100 Hz
  
Raw EEG data and labels are not included in this repository. Official dataset descriptions and labels are available at:

* **Dataset description:** [https://www.bbci.de/competition/iii/desc_IVa.html](https://www.bbci.de/competition/iii/desc_IVa.html)
* **True labels:** [https://www.bbci.de/competition/iii/results/#labels](https://www.bbci.de/competition/iii/results/#labels)

## Signal Preprocessing

All subjects undergo a consistent **preprocessing pipeline** aligned with motor imagery neuroscience literature:

### Band-Pass Filtering
* A **8–30 Hz band-pass filter** is applied to all EEG channels.
* This range captures **sensorimotor rhythms (mu & beta)** associated with imagined movement.

### Epoching (Cue-Locked Segmentation)
* EEG signals are segmented into time windows following task cues.
* **Epoch timing is subject-specific** to account for inter-subject variability in cortical response latency and rhythm modulation.
* Each subject’s **optimal response window** is determined empirically.

This design ensures **physiologically meaningful feature extraction** for every subject.

## Subject-Specific Classification (5 Subjects)

For each subject, an independent pipeline is trained and evaluated.

### Feature Extraction
* **Common Spatial Patterns (CSP)** are used to maximize variance differences between classes.
* **Per-trial z-score normalization** is applied before spatial filtering.

### Classification
* **Linear Discriminant Analysis (LDA)** is used as a lightweight, interpretable classifier.

### Model Selection & Validation
* Number of **CSP components** is selected via **5-fold stratified cross-validation**.
* **Cross-validation accuracy** guides final model configuration.
* Generalization is evaluated using **held-out test data**.

Each subject has a dedicated notebook reflecting this full pipeline.

## Cross-Subject Classification (Combined Subjects)

To study generalization across participants, EEG data from all five subjects are combined into a single training set.

### Filter Bank CSP (FBCSP)
EEG is decomposed into multiple frequency bands:
* **8–13 Hz**
* **13–20 Hz**
* **20–30 Hz**

**CSP** is applied independently within each band, and extracted features are **concatenated** across bands.

### Classification
* A **single LDA classifier** is trained on the combined feature representation.

### Comparison Study
* Performance of **FBCSP + LDA** is compared against standard **broadband CSP + LDA**.
* Results highlight the benefit of **frequency-specific spatial features** for cross-subject learning.

## Evaluation Strategy

Model performance is assessed using:
* **Training accuracy**
* **Test accuracy**
* **Cross-validation accuracy**
* **Confsuion matrix**
* * **Classification report** (Precision, Recall, and F1-score)
* **Overfitting behavior**
* **Subject-specific vs cross-subject robustness**
* **Feature representation effectiveness**

## Notebooks
* **5 notebooks:** Subject-specific CSP + LDA pipelines.
* **1 notebook:** Cross-subject FBCSP + LDA analysis.

Notebooks are intentionally structured similarly to ensure **methodological consistency**, with differences limited to subject-specific parameters and data.

## Key Takeaways
* **CSP + LDA** provides strong subject-specific MI decoding.
* **Subject-specific epoch timing** is critical for optimal performance.
* **Cross-subject MI classification** benefits from **filter-bank representations**.
* **FBCSP improves robustness** when subject data are pooled.

## License
This project is released under the **MIT License**.

## Author
**Mina Nagy**
