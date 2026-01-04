# Dataset: BCI Competition III – Dataset IVa

This project uses **BCI Competition III Dataset IVa**, a well-known benchmark dataset for motor imagery EEG classification.

No raw EEG data or labels are included in this repository.


## Dataset Description

- **Task:** Motor imagery classification  
- **Classes:**  
  - Right hand imagery  
  - Right foot imagery  
- **Subjects:** 5 subjects (aa, al, av, aw, ay)
- **Signal type:** EEG
- **Recording setup:** Multiple EEG channels recorded during motor imagery tasks

The official dataset description, recording protocol, and experimental details are provided by the competition organizers:

**Dataset description:**  
https://www.bbci.de/competition/iii/desc_IVa.html


## Labels

Ground-truth labels for evaluation are provided separately by the competition:

**True labels:**  
https://www.bbci.de/competition/iii/results/#labels


## Usage in This Project

- Each subject is first modeled **independently** using **CSP + LDA**
- A **cross-subject classification** experiment is conducted by combining data from all five subjects and applying **FBCSP + LDA**
- Official train/test splits defined by the competition are preserved
- No modifications to the original labeling scheme are performed


## Data Access

The dataset must be downloaded manually from the official BCI Competition website.

After downloading, data files should be placed locally and loaded directly within the notebooks.

This repository intentionally excludes raw EEG data to comply with dataset redistribution rules.
