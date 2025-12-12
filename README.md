# Congestion Price Effects in NYC (2025)

## Overview
This project examines how private vehicle travel patterns changed after the implementation of New York City (NYC)’s 2025 Congestion Pricing Program (CPP). As fuel tax revenues decline nationwide due to the increasing adoption of electric, hybrid, and fuel-efficient vehicles, policymakers have sought alternative strategies to maintain transportation funding. The policy represents the first large-scale congestion pricing system in the U.S., creating an important empirical case to evaluate early behavioral responses to cordon-based tolling. Using Replica mobility datasets and regression models (Difference-in-Differences (DID) and Two-Way Fixed Effects model (TWFE)), we estimate changes in private vehicle demand in the Congestion Relief Zone (CRZ) before and after tolling began.

---
## Data
### **Replica Mobility Dataset**
- Synthetic population-based mobility data
- Includes multiple modes (walk, transit, bike, private vehicles)
- Provides origin–destination (OD) pairs, timestamps, and trip purpose

### **Filtering Criteria**
- Study area: Manhattan
- Only **private vehicle trips** included  
- Commercial, taxi, and freight trips excluded  
- Datasets in 2024 (Pre-CPP) and 2025 (Post-CPP)
---

## Methodology
### **1. Difference-in-Differences (DID)**
- **Treatment group:** Trips entering the CRZ  
- **Control group:** Trips entering Upper Manhattan (UM)
- DID compares pre/post differences across treated and control groups.  
- Estimated model:  
  `ln(Y_it) = β0 + β1 Zone_i + β2 Time_t + δ (Zone_i × Time_t) + ε_it`    
  

### **2. Two-Way Fixed Effects (TWFE)**
To account for unobserved heterogeneity:
- **OD-pair fixed effects** (ui)  
- **Time fixed effects** (vt)  

Final model:  
`ln(Y_it) = δ D_it + β2 Time_t + u_i + ε_it`

### **3. Spatial Analysis Levels**
#### **Macro-Level: CRZ vs UM**
Provides a stable comparison by reducing fragmentation across OD pairs.

#### **Micro-Level: Census Tracts**
Allows inclusion of **trip duration** as a control variable.  
Model:  
`ln(Y_it) = δ D_it + β2 Time_t + γ ln(Duration_it) + u_i + ε_it`   

---
## Results 
Results are estimated **hourly**, reflecting variation in travel demand.  

### Macro-level analysis: CRZ Vs. UM
**Weekday Effects**
- Small increases occur during the late-night hours (23:00–04:00).
- The largest decreases in CRZ-bound private vehicle trips appear between 05:00–11:00, with reductions of approximately 11–22%. 

**Weekend Effects**
- Most hours fluctuate within -10% to 10%, with confidence intervals often crossing zero (the baseline).
-  8% to 10% reductions appear around 8:00-10:00, with a small cluster of reductions during the 16:00 - 18:00.

### Micro-level estimates: Census Tracts
**Weekday Effects**
- A similar pattern emerges: the largest decreases occur between 05:00–11:00, with reductions of 6–17%.
- Confidence intervals are tighter than in the macro-level estimates, indicating more precise estimates.

**Weekend Effects**
- Overall impacts remain weak; the strongest effect appears as a 5% increase at 13:00.
- Morning reductions remain visible but occur over a shorter window (mainly at 08:00).

Note: In the micro-level analysis, trip duration is already embedded in the OD-pair structure of the Replica data. As a result, census-tract–level estimates with explicit duration controls yield results identical to OD-pair–based estimates, due to multicollinearity between trip duration and OD-pair fixed effects.

---

## Contribution
This study provides:
- A **systemwide analysis** of private vehicle travel behavior using Replica, filling the gap left by transit- and ride-hailing-focused research
- Insights to support future congestion management strategies (e.g., CPP, Vehicle Miles Traveled Pricing) in other U.S. cities
- Early empirical evidence from the first large-scale congestion pricing implementation in the U.S.

---

## Running the Code
Before running the code for our experiments, you need to download the Replica data sample from our Google Drive folder. Like the Replica dataset itself, this folder is accessible to anyone with a UC Berkeley affiliation. Click [here](https://drive.google.com/drive/folders/1Z-p5sSczNkTPDP8hMitVTWYBZNSOq73M?usp=drive_link) or copy the link from `data/readme.txt` to access the folder. Next, copy every CSV file from the Drive folder into the `data` folder. 

The next step is to create the conda environment from `environment.yml`. To do this, open the project root folder in your terminal and run

```
conda env create -f environment.yml
```
This creates an environment called `nyc_toll`, which you can use to run the notebooks that contain our experiments.

### `macro.ipynb`

This notebook runs our macro-level analysis. Make sure to set your kernel to use the `nyc_toll` environment. If you run all cells, `results/macro` will be populated by a table with our parameter estimates and `figures/macro` will contain a plot of our parameter estimate of the congestion toll effect varying with time.

### `micro.ipynb`

This notebook runs our macro-level analysis. If you run all cells, `results/micro` will be populated by a table with our parameter estimates and `figures/micro` will contain a plot of our parameter estimate of the congestion toll effect varying with time.

## Authors
- Donghui Lee (UC Berkeley)
- Giuseppe Perona (UC Berkeley)
- Jaden Lee (UC Berkeley)

---
