# FunctionalConnectivity_eLORETA
Tutorial developed under the framework of the PhD thesis "Novel Contributions to Personalized Brain Stimulation Biomarkers for Better Management of Neurological Disorders" - Doctoral Program in Biomedical Engineering (FEUP), supervised by João P. Cunha (INESC TEC, Porto, Portugal).

The low-resolution electromagnetic tomography (eLORETA) software allows to estimate electroencephalogram (EEG)-based Functional Connectivity (FC) netwroks using several metrics, in both sapce and sensor spaces, and compare them through statistical analysis. Here, we describe the methodology needed for this purpose.

Source: https://www.uzh.ch/keyinst/NewLORETA/InstallAndStartupGuideLoretaKey1.pdf

For visual clarification of the following steps, please see the FunctionalConnectivity_eLORETA.pdf file.

## 1. eLORETA Installation

Installation of the LORETA key software (https://www.uzh.ch/keyinst/NewLORETA/Software/Software.htm), by download the loreta key self-extracting file ("LoretaKey.exe") to your computer.

Prerequisites: Windows 7 or higher.

## 2. Convert the EEG singal into txt format

If EEG signals are in MATLAB files, use the following script:

>> load(filenmae) %mat file containing EEG signals (N samples x N channels)
>> dlmwrite([filename,'.txt'],seg,'delimiter','\t','precision',3)


## 3. Functional Connectivity Estimation
Select "Functional Connectivity Estimation" form the "Utilities" tab of the LORETA menu.

## 4. Identification of the EEG Electrodes Coordinates
In the "Electrode names to coordinates" panel, upload a text file containing the electrode channels.

## 5. Compute the transformation matrix
In the "Electrode cooridnates to transformation matrix" panel, upload the output document of the step 4.

## 6. Regions of the interest
This step is required to estimate FC networks in the source space. 

In the "ROI Marker 1" panel, upload:
* A tex file with the cartesian coordinates of the regions of the interest (ROIs). For this purpose, it can be used a brain average template. Teh first line of this document shold include the total number of ROIs used.
* The output of step 5

Select the method for defining the ROIs from the seed points: All voxels within a radius of 15 mm.

## 7. Estimation of functional networks
In the "Connectivity 1" panel, insert:
* The number of electrodes
* EEG number of samples
* EEG sampling rate
* Frequency bands of interest
* Folder/file mode: Each BIG file to 1 CRS (Each EEG in txt format will be used to estimate functional connectivity)
* Type of FC metric
* Output of the step 6.

Note: if you will estimate functional connectivity of several EEG segments, all segments must have the same number of samples, electrodes and sampling frequency.

By selecting the FC metric "Linear lagged connectivity" metric, this step will generate 3 different text files:
* Global Linear Connectivity
* Linear Lagged Connectivity
* Global Nonlinear Connectiviy


## 8. Statistical Comparison between Networks (optional)
In the "Statics" panel of the LORETA menu, the software allows users to statistially compare FC networks.

For example: Statistical comparison of connectivity between 2 groups using non-parametric randomization techniques with correction for multiple testing (n>6):
* Select "connectivity for time-varying log-spectra
* Select test/analysis: Independent groups A=B
* Upload the txt FC networks in the left and right panels (List A and List B)
* Chose the directory for the results

This step will generate three different outputs:
1 Setup file
2 T-test values
3 Threshold and Extremes Ps 

## 9. Results Visualization (Output)
The Loreta software allows user to visualzie the statistical changes, by selecting Wires > Connectivity Viewer in the main menu.

The user should upload:
* The ROIs file in "OpenCentroids" tab
* T-text file from the step 8 in the "OpenConnectivity" tab
* The corrected threshold value, in the Threshold and Extreme Ps file from the step 8

The software will display the brain with the selected ROIs and connectivity increases (red lines) and/or decreases (blue lines). In the ECG/ERP signals section, each increment will give the results for each frequency band selected.

