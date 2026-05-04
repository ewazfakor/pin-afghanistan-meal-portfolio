# Power BI Dashboard Layout Guide

## Dashboard 1: Executive Summary

### Visual Layout
```
┌─────────────────┬─────────────────┬─────────────────┬─────────────────┐
│  Total HH       │  % Female-Headed│  Avg FCS        │  CFRM Resolution│
│  Reached        │  HH Reached     │  Score          │  Rate           │
│  [KPI Card]     │  [KPI Card]     │  [KPI Card]     │  [KPI Card]     │
├─────────────────┴─────────────────┴─────────────────┴─────────────────┤
│  Beneficiary Reach by Sector & Sex (Stacked Bar Chart)              │
├─────────────────────────────────────────────────────────────────────┤
│  Cumulative Reach Trend — Monthly (Line Chart with target line)     │
├─────────────────────────────────────────────────────────────────────┤
│  Budget Execution by Sector (Gauge Charts × 4)                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Key DAX Measures
```dax
Total_HH_Reached = DISTINCTCOUNT(fact_beneficiary_reach[Beneficiary_HH_ID])

Pct_Female_Headed = 
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT(fact_beneficiary_reach[Beneficiary_HH_ID]),
        dim_beneficiary[Gender_HH_Head] = "Female"
    ),
    [Total_HH_Reached],
    0
)

Avg_FCS = AVERAGE(fact_food_security[FCS_Score])

CFRM_Resolution_Rate = 
DIVIDE(
    CALCULATE(
        COUNTROWS(fact_cfrm),
        fact_cfrm[Status] = "Resolved",
        DATEDIFF(fact_cfrm[Submission_Date], fact_cfrm[Resolution_Date], DAY) <= 5
    ),
    COUNTROWS(fact_cfrm),
    0
)
```

---

## Dashboard 2: Sectoral Performance

### Visual Layout
```
┌───────────────────────────┬───────────────────────────┐
│  Agriculture Outputs      │  WASH Outputs              │
│  (Bar: target vs actual) │  (Bar: target vs actual)  │
├───────────────────────────┼───────────────────────────┤
│  Nutrition Indicators     │  Livelihoods Indicators   │
│  (Line: FCS/rCSI trend)  │  (Bar: CFW wage days)     │
├───────────────────────────┴───────────────────────────┤
│  Sector Contribution to Resilience Score (Radar Chart)│
└───────────────────────────────────────────────────────┘
```

### Key DAX Measures
```dax
Agriculture_Target_Achievement = 
DIVIDE(
    SUM(fact_distributions[Quantity]),
    SUM(dim_activity[Target_Quantity]),
    0
)

WASH_Functionality_Rate = 
DIVIDE(
    CALCULATE(
        COUNTROWS(fact_infrastructure),
        fact_infrastructure[Status] = "Functional"
    ),
    COUNTROWS(fact_infrastructure),
    0
)

CFW_Wage_Days = SUM(fact_infrastructure[CFW_Labor_Days])
```

---

## Dashboard 3: Cross-Sectoral Analytics

### Visual Layout
```
┌───────────────────────────┬───────────────────────────┐
│  Irrigation vs. Yield     │  CFW Participation vs.    │
│  (Scatter: water access    │  Seed Adoption            │
│   x-axis, yield y-axis)   │  (Funnel: CFW → adoption) │
├───────────────────────────┼───────────────────────────┤
│  Water Access vs. Nutrition│  Training Synergy        │
│  (Heatmap: village ×      │  (Grouped Bar: single vs. │
│   water status × FCS)     │   combined training)      │
├───────────────────────────┴───────────────────────────┤
│  Correlation Matrix (5 sectors, color-coded r values) │
└───────────────────────────────────────────────────────┘
```

### Key DAX Measures
```dax
Yield_Per_Hectare = 
DIVIDE(
    SUM(fact_agriculture[Wheat_Yield_kg]),
    SUM(fact_agriculture[Land_Size_Hectares]),
    0
)

CFW_Adoption_Rate = 
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT(fact_beneficiary_reach[Beneficiary_HH_ID]),
        dim_beneficiary[CFW_Participant] = "Yes",
        dim_activity[Adopted_Improved_Seed] = "Yes"
    ),
    CALCULATE(
        DISTINCTCOUNT(fact_beneficiary_reach[Beneficiary_HH_ID]),
        dim_beneficiary[CFW_Participant] = "Yes"
    ),
    0
)

Training_Synergy_Score = 
CALCULATE(
    AVERAGE(fact_food_security[FCS_Score]),
    dim_beneficiary[Hygiene_Training] = "Yes",
    dim_beneficiary[Garden_Training] = "Yes"
)
```

---

## Dashboard 4: Adaptive Management

### Visual Layout
```
┌─────────────────────────────────────────────────────────────┐
│  [RED ALERT] 3 villages with >30% garden abandonment        │
│  [YELLOW ALERT] 2 enumerators with >5% missing data rate   │
│  [GREEN] 95% of Q1 targets achieved on time                │
├─────────────────────────────────────────────────────────────┤
│  Anomaly Detection Table (village, indicator, expected,    │
│  actual, deviation, recommended action)                     │
├─────────────────────────────────────────────────────────────┤
│  Recommendation Tracker (open/closed, owner, due date,     │
│  implementation status)                                     │
└─────────────────────────────────────────────────────────────┘
```

### Alert Logic (DAX)
```dax
Red_Flag_Garden_Abandonment = 
IF(
    [Garden_Abandonment_Rate] > 0.30,
    "CRITICAL: Garden abandonment >30%",
    BLANK()
)

Yellow_Flag_Missing_Data = 
IF(
    [Enumerator_Missing_Data_Rate] > 0.05,
    "WARNING: Missing data rate >5%",
    BLANK()
)

Green_Flag_Target_On_Track = 
IF(
    [Quarterly_Target_Achievement] >= 0.95,
    "ON TRACK: ≥95% Q target achieved",
    BLANK()
)
```

---

## Data Refresh Schedule

| **Dataset** | **Refresh Frequency** | **Method** | **Owner** |
|:------------|:----------------------|:-----------|:----------|
| Kobo/ODK exports | Daily (06:00) | Power Query API pull | Data Clerk |
| Excel trackers | Weekly (Monday 08:00) | SharePoint folder refresh | MEAL Assistant |
| SPSS analysis outputs | Per survey round | Manual import | MEAL Officer |
| External market data | Monthly | Manual CSV import | MEAL Assistant |

---

*Note: These are layout specifications and DAX measure templates for replication. Actual .pbix files are excluded from this public repository per PIN data sharing policies. See Ethical Note for synthetic data usage.*
