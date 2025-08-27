# Multi-Scale Anti-Correlated Neural States Analysis Pipeline

## Overview

This Google Colab notebook identifies and analyzes anti-correlated neural states during naturalistic fMRI measurements across global (whole-brain) and local (ROI-specific) scales. The method detects periods when brain regions show temporally opposing activity patterns and examines how these states relate to one another across scales, and to narrative events.

**Core Concept**: During movie viewing, brain activity exhibits periods where regions are temporally anti-correlated. We identify these periods using bimodality testing on time-by-time correlation matrices, create spatial templates capturing the dominant patterns, and analyze their relationship to stimulus boundaries.

**Paper**: ToDo

**Authors:** Dora Gozukara, Nasir Ahmad | **Lab:** [DyNaC-Lab](https://www.dynac-lab.com) | **Year:** 2025

## Running the Analysis

### Open in Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drgzkr/Multi-Scale_Anti-Correlated/main/Multi_Scale_AntiCorrelated_Neural_States_Dominate_Naturalistic_WholeBrain_Activity)

Click the "Open in Colab" button or copy the notebook URL to run in your browser. All required packages are installed automatically at the beginning of the notebook.

### Select Dataset
Use the dropdown menu to choose from pre-configured dataset (only possibly by contacting the authors to access the data unless you are using your own data):
- **StudyForrest**: 8 movie runs with narrative events, shots, audio features
- **CamCAN**: Single run with subjective events and camera transitions  
- **Custom**: Your own dataset (see below)

## Using Your Own Data

To analyze your own dataset:

1. **Upload data to Google Drive** in an accessible folder

2. **Set the dataset flag**:
```python
use_yourData = True
```

3. **Configure paths and parameters**:
```python
# Path to your 4D fMRI data
reference_nifti_path = '/content/drive/MyDrive/your_folder/your_data.nii.gz'

# TR duration in seconds  
TR_duration = 2.0

# Load your 4D data (shape: x, y, z, time)
yourdata_nifti_path = '/content/drive/MyDrive/your_folder/your_data.nii.gz'
concat_all_whole_brain_data = image.load_img(yourdata_nifti_path).get_fdata()
```

4. **Define stimulus boundaries**:
```python
# Create binary arrays (1s at boundary timepoints, 0s elsewhere)
stimuli_boundaries = [your_event_array1, your_event_array2]
stimuli_names = ['events', 'scenes']

# Example: Random boundaries for testing
random_boundaries = np.zeros(n_timepoints)
boundary_indices = np.random.choice(n_timepoints, size=20, replace=False)
random_boundaries[boundary_indices] = 1
stimuli_boundaries = [random_boundaries]
stimuli_names = ['random_events']
```

## Notebook Structure

The analysis runs in three main sections:

**Global Scale Analysis**
- Creates global template from ROI-averaged data
- Identifies task-positive vs default-mode-like states
- Analyses state transitions and durations
- Analyses state transitions and stimuli onsets

**Local Scale Analysis**  
- Examines anti-correlation within individual ROIs
- Creates local templates and timeseries
- Quantifies explained variance and state properties
- Analyses state transitions and stimuli onsets

**Cross-Scale Analysis**
- Correlates global and local templates
- Examines boundary overlap between scales
- Network-level analyses using Yeo parcellation

## Data Requirements

- **4D fMRI data**: Preprocessed volumetric timeseries (NIfTI format)
- **Stimulus annotations**: Event boundaries as binary arrays matching fMRI timepoints
- **TR specification**: Repetition time in seconds


## Output

The notebook generates:

- **Neural State Templates**: Global and local spatial patterns projected to cortical surfaces
- **Statistical Results**: Boundary overlap metrics and permutation test results
- **Visualizations**: Timeseries plots, brain maps, transition matrices
- **Saved Files**: NIfTI brain maps and figure outputs to Google Drive


## Citation

```
Gozukara, D., Oetringer, D., Ahmad, N., & Geerligs, L. (2025). 
Multi-Scale Anti-Correlated Neural States Dominate Naturalistic Whole-Brain Activity.
```

## Support

For questions or issues, contact the authors or visit [DyNaC-Lab](https://www.dynac-lab.com).
