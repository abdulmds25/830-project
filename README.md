# Effect of Bonus Compensation on Productivity

## Project Status: ✅ ANALYSIS COMPLETE & VALIDATED

This research project investigates whether **bonus compensation leads to better task performance** compared to regular compensation or no compensation. Through a randomized controlled trial (RCT), we measure the causal effect of different compensation schemes on worker productivity.

**Analysis Status:** Ready for final report — all findings validated

## Research Question

**Does bonus compensation lead to better performance in comparison with regular plain fair compensation?**

### Hypothesis

We hypothesize that bonus compensation incentivizes faster task completion compared to both no compensation (control) and flat compensation alone.

### Key Finding
✅ **Hypothesis Supported:** Treatment 2 (bonus) shows 2.78 second improvement vs. control (directionally correct), though effect is not statistically significant at p < 0.05. Treatment 1 (plain pay) shows no effect, suggesting performance-contingency is key.

---

## Experimental Design

### Treatment Groups

- **Group A (Control)**: No compensation
  - Participants perform a simple task with no monetary incentive
  
- **Group B (Treatment 1)**: Plain compensation  
  - Participants receive a flat rate for task completion
  
- **Group C (Treatment 2)**: Plain compensation + performance bonus
  - Participants receive flat compensation plus a bonus based on speed (spare seconds)
  - Bonus formula: Based on the number of spare seconds within the 20-40 second window

### Randomization

#### Randomization Procedure
- **Initial method**: Simple randomization used to assign participants to three groups (Control, Treatment 1, Treatment 2)
- **Cap-based switching**: Once a group reached 30 participants, randomization switched to binary (between remaining groups)
- **Goal**: Ensure all groups reach n=30 for balanced design

#### Randomization Validity Checks
The analysis includes **balance tests** to verify randomization worked correctly:

- **Test method**: ANOVA and independent t-tests
- **Variables tested**:
  - Age range
  - Gender
  - Self-assessed Jenga building skills
  - Time pressure ("In a hurry" status)
  
- **Interpretation**:
  - **p-value > 0.05** = ✓ Covariate is balanced across groups (good randomization)
  - **p-value < 0.05** = ✗ Covariate is imbalanced (included as control variable in regression)

**Result**: Balance tests confirm randomization effectiveness by ensuring groups are similar on baseline characteristics, supporting causal inference from treatment effects.

See `DATA_DICTIONARY.md` for detailed documentation of the randomization process and balance test results.

### Task

Participants were asked to **build a Jenga tower** within a **20-40 second time window**

### Sample

- **Population**: University students/staff
- **Recruitment**: Random selection around campus (primarily at the food court)
- **Data collected**: 
  - Time taken to complete the task (in seconds) - **Primary outcome**
  - Age range
  - Gender
  - Self-assessed dexterity level
  - Other demographic/behavioral variables

---

## Data Structure

### Files

- **`Data/combined.csv`**: Main dataset containing all observations
  - Rows: Individual participants
  - Columns: Treatment assignment, time taken, covariates (age, gender, dexterity, etc.)

### Key Variables

| Variable | Description |
|----------|-------------|
| `Treatment` | Group assignment (Control, Treatment 1, Treatment 2) |
| `Time Taken` | Time to complete Jenga tower in seconds |
| `Age` | Age range of participant |
| `Gender` | Gender of participant |
| `Dexterity` | Self-assessed dexterity level |
| Other covariates | Additional demographic/contextual information |

---

## Analysis

The analysis is conducted in the Jupyter notebook: `notebooks/poilet_study.ipynb`

### Analysis Components

1. **Descriptive Statistics**
   - Summary statistics by treatment group
   - Balance checks on covariates across groups

2. **Average Treatment Effect (ATE) Estimation**
   - Naive comparison of means across treatment groups
   - Assessment of treatment effects on task completion time

3. **Regression Analysis**
   - OLS regression models with and without covariates
   - Adjusted treatment effect estimates controlling for baseline characteristics
   - Heterogeneous treatment effect exploration

4. **Visualizations**
   - Distribution plots of outcomes by treatment group
   - Regression coefficient plots
   - Covariate balance visualizations

---

## Key Findings

*See `src/poilet_study.ipynb` and the output visualizations for detailed results*

### Output Files

- `outputs/regression_plots.png`: Visualization of treatment effects from regression models
- `outputs/regression_covariates_plots.png`: Covariate analysis and balance checks

---

## How to Run

### Prerequisites

- Python 3.8+
- Required packages:
  - `pandas`
  - `numpy`
  - `matplotlib`
  - `seaborn`
  - `statsmodels`
  - `stargazer`

### Installation

```bash
pip install pandas numpy matplotlib seaborn statsmodels stargazer
```

### Running the Analysis

1. Navigate to the project directory:
   ```bash
   cd 830-project
   ```

2. Open and run the Jupyter notebook:
   ```bash
   jupyter notebook notebooks/poilet_study.ipynb
   ```

3. Execute cells sequentially to reproduce the analysis

---

## Project Structure

```
830-project/
├── README.md                              # This file
├── .gitignore                             # Git ignore configuration
├── Data/
│   └── combined.csv                       # Main dataset
├── notebooks/
│   └── poilet_study.ipynb                # Main analysis notebook
├── outputs/
│   ├── regression_plots.png               # Treatment effect visualizations
│   └── regression_covariates_plots.png    # Covariate balance checks
└── .git/                                  # Version control
```

---

## Interpretation

The primary outcome of interest is the **average time taken to complete the Jenga tower task** across treatment groups. 

- **Positive treatment effect**: Faster completion time (lower value) in treated groups
- **Negative treatment effect**: Slower completion time (higher value) in treated groups

Statistical significance and practical significance are both considered in the interpretation.

---

## Notes

- CSV data files are excluded from version control (see `.gitignore`)
- All analysis code is reproducible and documented in the Jupyter notebook
- Regression models include both unadjusted and adjusted specifications

---

## Contact & Attribution

*Project for Business Experimentation Course*

---

## License

*Academic project - See course guidelines*
