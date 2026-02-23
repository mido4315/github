# Geomasking and Spatial Autocorrelation (Seminar Project)

This repository contains my seminar project on **anonymization of georeferenced microdata** and **analytical validity**.  
I evaluate how two geomasking methods—**Donut Masking** and **AGDM**—affect **spatial autocorrelation** in a binary health outcome (`sleep_diso`) using synthetic point microdata for Cologne (n = 10,900).

## Research Question
**How do geomasking methods (Donut vs AGDM) affect spatial autocorrelation in the binary health outcome `sleep_diso`, and which method preserves spatial autocorrelation patterns more closely to the original data?**

## Data (high level)
- Synthetic point microdata for Cologne (10,900 points).
- Each record represents an individual with attributes such as:
  - `id`, `district`, `gender`, `age`
  - `sleep_diso` (0/1, rare outcome)
  - geometry (point coordinate)
- Three geometry versions are compared:
  - Original coordinates
  - Donut-masked coordinates
  - AGDM-masked coordinates

## Methods (what I did)
### Spatial weights
- Point data: **k-nearest neighbors (kNN)** spatial weights
- Main analysis: **k = 8**, row-standardized
- Sensitivity check: **k ∈ {6, 8, 10, 12}**

### Global spatial autocorrelation
- **Global Moran’s I** with permutation test (**999 permutations**)
- **Geary’s C** with permutation test (**999 permutations**)

### Local spatial autocorrelation (LISA)
- **Local Moran’s I (LISA)** with permutation test (**999 permutations**)
- Cluster types:
  - High–High (HH), Low–Low (LL), High–Low (HL), Low–High (LH), Not significant
- Visual comparison across original vs masked datasets

### Quantitative comparison (local results)
To compare original vs each masked dataset:
- **Spearman correlation** between Local Moran’s I values
- **Jaccard overlap** of significance patterns (significant vs not significant)
- **Cluster agreement rate** for points where at least one dataset is significant

## Key interpretation note
Because `sleep_diso` is **binary and rare**, spatial clustering is expected to be **weak** (small Moran’s I values).  
The main focus is on **relative changes** between original and masked datasets (validity preservation), not on large effect sizes.

## Repository contents
- `Anonymization_of_Georeferenced_Microdata_Seminar.ipynb`  
  Colab notebook used to run the analysis and generate outputs.
- `outputs/`  
  Generated figures and tables (exported from the notebook).
- `presentation.pdf`  
  Seminar slide deck (Beamer).
- `report.pdf`  
  Written seminar report.

## How to reproduce (high level)
1. Open `Anonymization_of_Georeferenced_Microdata_Seminar.ipynb` (Google Colab recommended).
2. Install required packages (the notebook includes installation cells).
3. Run all cells to regenerate the outputs in `outputs/`.

> Note: File paths in the notebook may reference Google Drive locations (typical Colab workflow). You may need to adjust paths depending on your environment.

## Results summary (one sentence)
Both masking methods attenuate spatial autocorrelation relative to the original data, and **AGDM preserves local spatial autocorrelation patterns slightly better** than Donut according to similarity metrics.

## Author
Mohamed Hassan  
ID: 272455
