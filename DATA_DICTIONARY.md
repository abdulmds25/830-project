# Data Dictionary: Effect of Bonus Compensation on Productivity

## Overview
This document describes all variables in the `Data/combined.csv` dataset collected for the experiment on bonus compensation effects on task productivity.

---

## Variable Definitions

### **Primary Outcome Variable**

| Variable | Type | Description | Unit | Range | Notes |
|----------|------|-------------|------|-------|-------|
| `Time Taken` | Numeric (Continuous) | Duration to complete Jenga tower task | Seconds | 5-65 | Primary outcome of interest. Should fall within 20-40s task window for valid attempts. |

---

### **Treatment Assignment**

| Variable | Type | Description | Coding | Notes |
|----------|------|-------------|--------|-------|
| `Block` | Categorical | Treatment group assignment | "Control", "Treatment 1", "Treatment 2" | Assigned via randomization. Once a group reached 30, randomization switched to binary. |
| `treatment_numeric` (Derived) | Numeric | Numeric treatment identifier | 0 = Control, 1 = Treatment 1, 2 = Treatment 2 | Created during data processing for regression analysis. |
| `treated` (Derived) | Binary | Any treatment vs Control | 0 = Control, 1 = Any treatment | Created during data processing for aggregated analysis. |

#### **Treatment Details**:
- **Control (0)**: No compensation. Participant completes Jenga tower with no monetary incentive.
- **Treatment 1 (1)**: Plain compensation. Participant receives flat fixed amount ($X) for task completion.
- **Treatment 2 (2)**: Plain compensation + performance bonus. Participant receives fixed amount ($X) plus bonus based on spare seconds within the 20-40s window.
  - Bonus formula: $Y per spare second (calculated as max(40 - Time Taken, 0))
  - Example: If task completed in 35s, bonus = 5 spare seconds × $Y

---

### **Demographic Covariates**

| Variable | Type | Description | Coding | Range | Notes |
|----------|------|-------------|--------|-------|-------|
| `What is your age range?` | Numeric (Ordinal) | Age range bracket | Self-reported | 18-65+ | Typically: 18-25, 26-35, 36-45, 46-55, 56-65, 65+ |
| `What is your gender?` | Categorical | Gender identity | "M", "F", or other | - | Coded as `gender_M` (1=Male, 0=Female/Other) in analysis. |
| `How would you rate your Jenga building skills?` | Numeric (Ordinal) | Self-assessed Jenga dexterity | Likert scale (1-5) | 1-5 | 1 = Very poor, 5 = Very skilled. Measures baseline dexterity covariate. |
| `Are you in a hurry right now?` | Categorical (Binary) | Time pressure indicator | "Yes", "No" | - | Coded as `in_hurry` (1=Yes, 0=No). Controls for time urgency as a behavioral covariate. |

---

### **Administrative Variables**

| Variable | Type | Description | Notes |
|----------|------|-------------|-------|
| `Timestamp` | DateTime | Date and time of observation | Format: M/D/YYYY HH:MM:SS. Useful for chronological ordering and identifying data collection sessions. |
| `Score` | Numeric | Task performance score | Currently empty/unused. Was intended to track task success metrics or bonus calculation verification. |
| `Notes` | Text | Experimenter or participant notes | Free text field capturing qualitative observations, e.g., "rejected the reward", "volunteered", issues encountered. |

---

## Data Collection Protocol

### **Sample**
- **Population**: University students and staff
- **Recruitment**: Random selection around campus (primarily food court)
- **Randomization**: Simple randomization initially; switched to binary randomization once a group reached n=30

### **Task**
- **Task**: Build a Jenga tower
- **Time constraint**: 20-40 second window for valid completion
- **Measurement**: Time taken recorded in seconds (precision to 0.01s)

### **Data Quality Standards**
- Valid observations: Time Taken between 5-65 seconds (extreme values investigated)
- Missing data: Should be minimal; any gaps flagged during analysis
- Bonus rejections: Tracked in Notes field (indicates intent-to-treat vs as-treated considerations)

---

## Analysis Variables (Derived)

| Variable | Derivation | Usage |
|----------|-----------|-------|
| `treatment_numeric` | Map: Control→0, T1→1, T2→2 | Regression models with treatment dummies |
| `treated` | Binary: treatment_numeric ∈ {1,2} → 1, else 0 | Collapsed treatment analysis (any treatment vs control) |
| `is_T1` | treatment_numeric == 1 → 1, else 0 | Individual treatment 1 effect estimation |
| `is_T2` | treatment_numeric == 2 → 1, else 0 | Individual treatment 2 effect estimation |
| `gender_M` | gender ∈ {"M", "m"} → 1, else 0 | Gender covariate in regressions |
| `in_hurry` | "Yes" → 1, "No" → 0 | Time pressure covariate |
| `bonus_rejected` | Notes contains "reject*", "decline", "no bonus" → 1, else 0 | Identifying non-compliance for intent-to-treat analysis |

---

## Summary Statistics Target

| Group | Target N | Current N | Status |
|-------|----------|-----------|--------|
| Control | 30 | TBD | Data collection ongoing |
| Treatment 1 | 30 | TBD | Data collection ongoing |
| Treatment 2 | 30 | TBD | Data collection ongoing |
| **Total** | **90** | TBD | **Balanced design target** |

---

## Data Entry & Quality Checklist

- [ ] Timestamp recorded for all observations
- [ ] Treatment assignment verified (no missing values)
- [ ] Time Taken measured precisely (to 0.01s if possible)
- [ ] Age range collected
- [ ] Gender recorded
- [ ] Jenga skills rating obtained (1-5)
- [ ] Hurry question answered
- [ ] Any special notes or incidents documented
- [ ] No duplicate Timestamp entries
- [ ] Time Taken within valid range (5-65s, ideally 20-40s window)

---

## Known Data Issues & Notes

1. **Duplicate age column**: Original data has "What is your age range?" appearing twice. First occurrence is kept; duplicate dropped.
2. **Empty Score column**: Was intended for performance tracking; currently unpopulated. Consider removing or populating with bonus calculations.
3. **Treatment imbalance**: Early data shows skew toward treatments. Continue recruiting for Control group.
4. **Bonus rejections**: Some participants declined rewards (documented in Notes). Important for intent-to-treat vs as-treated analysis.
5. **Missing "in_hurry" mapping**: Data collected as "Yes"/"No"; mapped to 1/0 for analysis.

---

## Contact & Updates
- **Data collected**: Starting 2/20/2026
- **Last updated**: 2/26/2026
- **Collection status**: Ongoing—target ~90 total observations (30 per group)

For questions about variable definitions or data collection procedures, see the experiment protocol or contact the research team.
