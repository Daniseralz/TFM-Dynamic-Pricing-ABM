# Dynamic Pricing under Capacity Constraints
### An Agent-Based Approach to Competition in the Car Rental Industry
 
**Master's Thesis (TFM)** — Máster en Economics with Data Science, Universidad de Alicante
Author: Daniel Serrano Alzamora · September 2026
 
---
 
## Description
 
This repository contains the Master's Thesis and the simulation code developed for it. The work uses an **Agent-Based Model (ABM)** with synthetic data to evaluate whether a pricing rule based on the relative competitive position against a small subset of price-adjacent rivals (**Top-3 / Positional strategy**) outperforms — in revenue (RevPAR) and occupancy stability — rules based on aggregate market indicators (**Average**) or on own fleet occupancy (**Occupancy**), within a capacity-constrained oligopolistic car rental market. A **Hybrid** strategy combining the Positional and Occupancy signals is also evaluated.
 
The motivation for this thesis stems from an empirical observation made during an internship in the *Pricing and Revenue* department of a car rental company: in daily practice, comparing one's own price against a small group of price-adjacent competitors seemed to provide a more actionable signal than tracking market-wide aggregates. The thesis formalizes this intuition and subjects it to statistical testing in a controlled simulated environment.
 
## Repository contents
 
| File | Description |
|---|---|
| `TFM_Dynamic_Pricing_ABM.pdf` | Full thesis report (theoretical framework, model specification, results, conclusions, and future work). Written in LaTeX. |
| `TFM_Dynamic_Pricing_ABM.ipynb` | Python notebook with the full implementation of the ABM simulator, the experimental design, the statistical tests, and the figures used in the thesis. |
| `TFM_Dynamic_Pricing_ABM_Presentation.pdf` | Slide deck used for the thesis defense, summarizing the motivation, model, results, and conclusions. |
 
## Model overview
 
- **10 synthetic firms** compete on price in a market where each firm operates a **fixed fleet**.
- Aggregate demand is allocated across firms via a **logit choice model** based on price, with **proportional rationing** applied whenever demand exceeds available capacity.
- Each day, firms adjust their price (max. ±3%) according to one of **four pricing rules**:
  - **Average**: reacts to the mean price of all rivals.
  - **Occupancy**: reacts to the firm's own occupancy relative to a target (85%).
  - **Positional**: reacts to the mean price of the 3 rivals closest in price (Top-3).
  - **Hybrid**: an equal-weighted combination (γ=0.5) of Occupancy and Positional.
- The experimental design crosses **2 levels of capacity tension** (low / high season) × **2 fleet-dispersion configurations** (homogeneous / dispersed) × **4 strategies** × **20 random seeds** (320 simulations of 180 days each).
- Main metrics: **RevPAR** (revenue per available car-day) and **occupancy instability**.
## Key results
 
- **Positional ≈ Average**: no statistically significant RevPAR differences between the two strategies in any of the four scenarios (paired test by seed, p ≥ 0.070).
- A controlled sweep of the β parameter (demand price sensitivity) likewise finds no evidence that the Positional strategy's advantage depends on demand elasticity.
- **Hybrid fails to dominate** either of the two best-performing pure strategies (p<0.0001 across all eight relevant comparisons), suggesting that, under the adopted weighting, blending the occupancy signal with the positional one hurts performance.
- No robust hierarchy among strategies emerges for occupancy stability once the Holm correction for multiple comparisons is applied.
- Mean RevPAR consistently doubles across strategies when moving from low to high season.
The full report (`TFM_Dynamic_Pricing_ABM.pdf`) develops the theoretical framework, methodological justification, study limitations, and six proposed lines of future work.
 
## Requirements to run the notebook
 
```bash
pip install numpy pandas matplotlib scipy statsmodels
```
 
The notebook is designed to be run end-to-end (e.g. in Google Colab or Jupyter). It reproduces, in order:
 
1. Baseline parameters and calibration (D₀, β)
2. Market initialization and the rationing mechanism
3. The four pricing rules
4. The simulation engine
5. The full experimental design (320 simulations)
6. Statistical testing (Welch, paired, Holm correction)
7. The β sensitivity sweep
8. Internal simulator verification tests
## How to cite
 
Serrano Alzamora, D. (2026). *Dynamic Pricing under Capacity Constraints: An Agent-Based Approach to Competition in the Car Rental Industry*. Master's Thesis, Máster en Economics with Data Science, Universidad de Alicante.
 
## License
 
This work is shared for academic and educational purposes. If you wish to reuse the code or results, please cite the source.
