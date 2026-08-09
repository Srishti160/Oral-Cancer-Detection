PROBLEM IDENTIFICATION AND IMPLEMENTATION: - 
This chapter defines the core problem this project aims to solve and outlines the 
implementation strategy, including dataset description and the methodology for data 
handling. 
3.1 Problem Identification: 
The data set used in this project consists of 3556 Raman Spectra samples, each represented 
as a vector of 1037 spectral intensity values (columns Var1-Var1037). The first row 
corresponds to Raman shift positions (in cm⁻¹) and each subsequent rose face sponge to 
individual spectral measurement. 
The primary challenge in oral cancer management is early and accurate detection. While 
biopsies provide definitive results, their invasive nature and dependence on expert 
pathologists make them impractical for large-scale screening. Traditional imaging 
modalities and cytological tests also suffer from limitations in sensitivity and specificity. 
Therefore, the problem addressed in this project is: “To develop a machine learning-based 
diagnostic pipeline using Raman spectroscopy data for accurate, non-invasive detection of 
oral cancer.” 
This involves preprocessing spectral data, extracting meaningful features, and training 
classification models to distinguish between healthy and non-healthy tissues. 
3.2 Implementation: 
Dataset Description 
The dataset used in this project consists of 3556 Raman Spectra samples, each represented 
as a vector of 1037 spectral intensity values. The first row corresponds to Raman shift 
positions (in cm−1) and each subsequent row corresponds to an individual spectral 
measurement. 
The spectra were initially divided into 5 classes: 
• Class 0: Healthy tissue 
• Class 1: Premaligant (early dysplasia) 
• Class 2: Oral Cancer (malignant tissue) 
• Class 3: Other Oral Conditions (e.g., inflammation, ulceration) 
• Class 4: Miscellaneous / Noise or Ambiguous 

For this project, the classification problem was simplified into a binary task: 
• Healthy (Class 0) 
• Non-Healthy (Classes 1-4 combined) 
This approach aligns with the clinical objective of identifying potential malignant tissues 
that require further diagnostic confirmation. Since the most diagnostically relevant Raman 
signals lie in the biological fingerprint region (500−2000 cm-1), only this region of the 
spectra was selected for analysis. This ensures the exclusion of irrelevant high-wave 
number regions and focuses on molecular vibrations associated with proteins, lipids, and 
nucleic acids.


4.1 METHODOLOGY: - 
Raw Raman spectra often contain noise, fluorescence background, and baseline shifts. 
To enhance data quality, the following preprocessing pipeline was applied: 
• Spectral Cropping: Restricted to the 500−2000textcm−1 region, which is the 
biologically relevant fingerprint region. 
• Cosmic Ray Removal: Using the Whitaker algorithm to eliminate spurious spikes 
caused by cosmic rays. 
• Denoising: The Savitzky-Golay filter was applied with a window length of 
9 and polynomial order of 3 to smooth the spectral data and reduce noise. 
• Baseline Correction: The Adaptive Smoothness Penalized Least Squares (asPLS) 
method was used to remove the fluorescence background, which can obscure the 
Raman signals. 
• Normalization: Min-Max normalization was applied to scale the intensities between 
zero and one, ensuring that all spectra are on a comparable scale. 
To better understand the effect of preprocessing, Figure 2 and Figure 3 helps us to compare 
a raw spectrum with its processed version. 
Fig 4.1: The figure shows a raw Raman spectrum before baseline correction, highlighting the 
presence of a strong background signal. 
7 
Fig 4.2: This figure illustrates the same Raman spectrum after baseline correction, showing a 
flattened baseline and enhanced spectral peaks. 
4.2 Feature Extraction: 
The fingerprint region-specific Raman peaks correspond to molecular vibrations of biomolecules such 
as nucleic acids, proteins, and lipids. These peaks serve as biomarkers for distinguishing healthy and 
malignant tissues. The following features were extracted from the spectra: 
• ~785 cm-1: Symmetric phosphate stretching (associated with DNA/RNA) 
• ~1003 cm-1: Phenylalanine ring breathing (associated with proteins) 
• ~1095 cm-1: C-C stretching (lipids) 
• ~1245 - 1250 cm-1 : Amide III band (proteins) 
• ~1300 cm-1: CH2 twisting (lipids, proteins) 
• ~1445 cm-1: CH2 deformation (lipids, proteins) 
• ~1575 - 1585 cm-1 : Associated with DNA/RNA 
• ~1655 - 1665 cm-1 : Amide I band (associated with proteins)

<img width="326" height="257" alt="image" src="https://github.com/user-attachments/assets/c2c3fa26-41b5-4af7-b100-4bfa6f0d252a" />

Result
The project's XGBoost model achieved a higher  accuracy and sensitivity than most of the other methods. The exceptional sensitivity of 99.4% is particularly significant in a clinical context, as it means the model is highly 
effective at correctly identifying cancerous cases, which is the top priority for a diagnostic 
tool. While the specificity (82.1%) is slightly lower than some other models, the high 
sensitivity is often a more critical metric in early screening applications to ensure no 
potential cancer cases are missed.
