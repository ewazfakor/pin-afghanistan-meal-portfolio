# Project 04: Integrated Monitoring & Cross-Sectoral Analytics

## People in Need (PIN) Afghanistan | MEAL Officer — Data Integration, Visualization & Evidence-Based Learning

| **Attribute** | **Details** |
|---------------|-------------|
| **Project** | Cross-Sectoral Integration Portfolio |
| **Location** | Malistan & Ajristan Districts, Ghazni Province |
| **Duration** | Ongoing (2024–2025) |
| **Sectoral Coverage** | Agriculture, WASH, Nutrition, Livelihoods, Protection |
| **My Role** | MEAL Officer |

---

## 1. Project Narrative: Why Integrated Monitoring Matters

In rural Ghazni Province, agriculture, WASH, and nutrition are threads of the same resilience fabric. A farmer cannot adopt improved seeds without reliable irrigation; a woman cannot sustain a kitchen garden without a functional well nearby; food security collapses when waterborne illness drains household income.

This portfolio demonstrates my evolution from **tool-user to tool-builder** — linking five sectoral datasets through village-level keys, shifting reporting from outputs to outcomes.

---

## 2. Dashboard Architecture

### 2.1 Dashboard Structure

I designed a Power BI dashboard with **four core tabs**:

| **Tab** | **Purpose** | **Primary Users** |
|---------|-------------|-------------------|
| **Executive Summary** | KPIs, beneficiary reach, budget execution | Senior Management, Donor |
| **Sectoral Performance** | Monthly trends by sector (agriculture, WASH, nutrition) | Sector Leads, Project Manager |
| **Cross-Sectoral Analytics** | Correlations, combined intervention effects | MEAL Team, Learning Advisor |
| **Adaptive Management** | Red-flag alerts, anomaly detection, recommendations | Program Team, Management |

### 2.2 Data Model

Five datasets linked via `Village_ID`, `Beneficiary_HH_ID`, and `Cluster_ID` using a **star schema with bridge tables**:

```
                    fact_beneficiary_reach
                    ├─ dim_beneficiary (demographics, vulnerability, status)
                    ├─ dim_village (location, elevation, cluster, water access)
                    ├─ dim_date (year, month, quarter, season)
                    ├─ dim_activity (sector, output, modality)
                    └─ dim_partner (PIN, Cesvi, Alliance2015)

                    fact_food_security
                    ├─ dim_beneficiary
                    ├─ dim_village
                    └─ dim_date

                    fact_infrastructure
                    ├─ dim_village
                    └─ dim_date

                    fact_livestock
                    ├─ dim_beneficiary
                    └─ dim_date

                    fact_training_attendance
                    ├─ dim_beneficiary
                    ├─ dim_village
                    └─ dim_date
```

### 2.3 Three Visualizations Driving Decisions

1. **Irrigation-Wheat Yield Scatter** — Rehabilitated canals correlated with **34% higher yields**; prioritized canal rehab in Year 2.
2. **CFW-to-Adoption Funnel** — CFW participants showed **40% higher seed adoption**; justified integrating livelihoods and agriculture.
3. **Water Access-Nutrition Heatmap** — Villages with >80% functional wells had **18% lower malnutrition**; articulated WASH-nutrition linkages.

---

## 3. Cross-Sectoral Analysis Findings

### Finding 1: Water Infrastructure Drives Garden Productivity

Villages with rehabilitated wells showed **23% higher kitchen garden productivity**. Women reallocated **1.2 hours daily** from water collection to garden maintenance. This led to co-locating WASH and garden interventions.

### Finding 2: CFW Income Enables Agricultural Risk-Taking

CFW participants showed **40% higher uptake** of improved seeds and **28% higher fertilizer use** than matched non-participants. Income security created a risk buffer enabling experimentation.

### Finding 3: Combined Training Outperforms Silos

Households where women attended both hygiene and garden training reported **31% higher dietary diversity** than single-sector attendees. This synergy justified restructuring training calendars across teams.

---

## 4. Learning Briefs

### Brief 1: The Water-Garden Nexus — How Water Access Determines Kitchen Garden Success

**Research Question:** Does proximity to a functional water source predict kitchen garden productivity and dietary diversity?

**Methodology:**
- Extracted GPS coordinates and functionality status from the WASH database (n=187 wells)
- Calculated walking distance to each household using geospatial buffers
- Merged with kitchen garden monitoring forms (n=95 women) using a **500m proximity threshold** in Power Query
- Ran Pearson correlation and independent-samples t-tests to examine relationships between walking time to water, vegetable production (kg), and dietary diversity scores (FCS)

**Key Finding:**
- Women within 500m of a rehabilitated well produced **42 kg** of vegetables per season versus **28 kg** for those walking >1 km (p<0.05)
- FCS scores were **18% higher**
- Well *functionality* mattered more than well existence: poorly maintained rehabilitated wells showed no improvement over controls, indicating rehabilitation without sustained maintenance does not shift outcomes
- The time-reallocation effect was significant — women near functional wells reallocated **1.2 hours daily** from water collection to garden maintenance

**Recommendations:**
1. Mandate Village WASH Committees as precondition for kitchen garden enrollment
2. Sequence WASH rehabilitation 3–6 months before garden kit distribution to allow water access stabilization
3. Integrate well maintenance training into agriculture program onboarding
4. Track well functionality quarterly via Kobo forms, not just at installation
5. Automate functionality alerts in the dashboard using red conditional formatting

### Brief 2: Cash-for-Work as Catalyst for Agricultural Adoption

**Research Question:** Do CFW participants adopt improved agricultural inputs at higher rates than demographically similar non-participants?

**Methodology:**
- Used **logistic regression** to estimate propensity scores based on baseline household characteristics
- Paired **100 CFW participants** with **100 non-participant households** using nearest-neighbor matching with a 0.15 caliper
- Controlled for land size, household composition, education level, and pre-program asset ownership
- Verified balance using standardized mean differences
- Compared input adoption rates between matched groups using chi-square tests and odds ratios

**Key Finding:**
- Matched CFW households were **40% more likely** to use improved seeds (73% vs. 52%, OR=2.4)
- **28% more likely** to apply Urea/DAP at recommended rates (61% vs. 43%)
- The effect was strongest among households in the **poorest wealth quintile**
- Follow-up interviews revealed CFW income provided a "safety net" reducing perceived risk of crop failure with unfamiliar inputs

**Recommendations:**
1. Transition from standalone CFW to integrated CFW-Agriculture packages where employment precedes or coincides with input distribution
2. Use CFW wages to partially subsidize input costs for the poorest quintile
3. Add a CFW participation flag to the agriculture monitoring form to enable real-time adoption tracking
4. Monitor adoption rates by CFW participation status as a quarterly leading indicator in program reviews

### Brief 3: Beyond Silos — Synergy of Combined Hygiene and Agriculture Training

**Research Question:** Is there a synergistic effect when women receive both WASH/hygiene and agricultural training compared to single-sector training?

**Methodology:**
- Cross-tabulated training attendance records from Protection (hygiene awareness sessions, n=3,000 beneficiaries) and Agriculture (kitchen garden management training, n=95 women) with endline nutrition survey data (FCS and rCSI scores) by Household ID
- Applied **two-way ANOVA** to test for interaction effects between training exposure types, controlling for household size and baseline food security status
- Post-hoc Tukey HSD tests identified which group differences were significant

**Key Finding:**
- Households receiving both training types achieved mean FCS of **68.4** versus **55.2** for hygiene-only and **58.7** for garden-only (F=14.3, p<0.001)
- The **interaction effect explained 12% of variance** in food security outcomes beyond the additive effects of each training alone
- Qualitative data suggested hygiene training reduced diarrheal disease episodes by approximately **35%**, which decreased nutrient loss and improved absorption of garden produce — creating a biological synergy that neither intervention achieved independently

**Recommendations:**
1. Institutionalize joint training calendars across Protection, Agriculture, and Nutrition teams with quarterly coordination meetings
2. Develop a unified "Resilience Package" training module that integrates hygiene, nutrition, and garden management into a single curriculum delivered by paired sector staff
3. Track combined training coverage as a program-level KPI
4. Include dietary diversity as a standard indicator in all agriculture-WASH program logframes

---

## 5. Capacity Building

I trained **five program staff** across three sessions:

| **Session** | **Duration** | **Content** | **Outcome** |
|:------------|:-------------|:------------|:------------|
| Dashboard Navigation & Filtering | 2 hours | Tab structure, slicers, drill-through, export options | Staff independently navigate dashboard |
| Reading Cross-Sectoral Visuals | 2 hours | Interpreting scatter plots, heatmaps, correlation matrices | Staff identify trends and flag anomalies |
| Adaptive Management Tab | 1 hour | Logging observations, triggering alerts, using red flags | Staff use dashboard in program reviews |

**Bi-weekly 30-minute "data stand-ups"** sustained the practice. By Month 3, staff independently used the dashboard in reviews:
- The Agriculture Officer identified a yield anomaly triggering seed quality investigation
- The WASH Officer used correlation data to prioritize well rehabilitation for garden-expansion villages

---

## 6. Evidence-Based Recommendations

### Adjustment 1: Integrating CFW and Agriculture Programming

| **Indicator** | **Before (Q1)** | **After (Q3)** | **Change** |
|:--------------|:---------------:|:--------------:|:----------:|
| Improved seed adoption (CFW participants) | 52% | 73% | +21 pp |
| Urea/DAP at recommended rate | 43% | 61% | +18 pp |
| CFW households with diversified income | 31% | 58% | +27 pp |

PSM analysis showed CFW income enabled agricultural risk-taking. Previously, teams operated on separate timelines. I recommended integrating CFW registers with input distribution, delivering agricultural training during CFW employment, and prioritizing CFW village selection in agricultural areas.

### Adjustment 2: Pre-Conditioning Kitchen Gardens on Water Access

| **Indicator** | **Before (All Villages)** | **After (Water-Preconditioned)** | **Change** |
|:--------------|:-------------------------:|:-------------------------------:|:----------:|
| Garden productivity (kg/season) | 28 kg | 44 kg | +57% |
| Garden abandonment (mid-season) | 34% | 11% | -23 pp |
| Women's water collection time | 3.2 hrs/day | 1.8 hrs/day | -44% |

Proximity analysis revealed water access as the strongest predictor of garden success. I modified selection criteria to require functional water points within 500m, reducing eligible villages but dramatically improving outcomes and cost-effectiveness.

---

## 7. Technical Skills Showcase

| **Skill Category** | **Tools/Methods** | **Application** |
|:-------------------|:------------------|:----------------|
| **Power Query (M)** | Custom functions, unpivoting Kobo repeats, fuzzy matching | Monthly refresh automation; cleaned 15,000 vaccination records; standardized 47 village name variants |
| **DAX Measures** | `CALCULATE`, `FILTER`, `RELATED`, time intelligence | Dynamic measures for yield/ha, functional water %, dietary diversity reach |
| **Data Cleaning** | Fuzzy matching, IQR outlier detection, validation rules | Flagged 23 anomalous yield records; built automated quality checks |
| **Statistics** | Propensity Score Matching, correlation, two-way ANOVA, chi-square | PSM for CFW impact; correlation for WASH-nutrition; ANOVA for training synergy |
| **Data Architecture** | Star schema, bridge tables, calculated tables | Linked 5 datasets via `Village_ID`, `Beneficiary_HH_ID`, `Cluster_ID` |
| **Visualization** | Conditional formatting, drill-through, bookmarks, tooltips | KPI cards; scatter plots; red-flag adaptive management alerts |

---

## 8. Cross-Sectoral Village Profile (Sample Data)

| **Village** | **Wheat Yield (kg/ha)** | **Well Status** | **Garden Adoption (%)** | **Training Attendance (%)** | **Resilience Score** |
|:------------|:-----------------------:|:---------------:|:-----------------------:|:--------------------------:|:--------------------:|
| Nawabad | 2,850 | Functional | 78% | 82% | 7.8 |
| Qala-e-Mullah | 1,920 | Functional | 65% | 71% | 6.4 |
| Deh-e-Bala | 3,100 | Functional | 89% | 88% | 8.6 |
| Spedar | 1,450 | Non-functional | 34% | 45% | 4.2 |
| Khwaja Omari | 2,680 | Functional | 72% | 76% | 7.3 |
| Sar-e-Karez | 1,780 | Functional | 58% | 63% | 5.9 |
| Shinkai | 980 | Non-functional | 22% | 38% | 3.1 |
| Ibrahim Khail | 2,340 | Functional | 69% | 74% | 6.9 |

*Resilience Score: Composite index (0–10) equally weighted across agricultural productivity, water access, livelihood diversification, and human capital. Source: PIN Ghazni MEAL Database, 2024–2025.*

---

## 9. Power BI Dashboard Screenshots — Layout Specifications

Since actual Power BI files cannot be embedded in GitHub, the following describes each dashboard tab with its visual layout for replication:

### Tab 1: Executive Summary
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

### Tab 2: Sectoral Performance
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

### Tab 3: Cross-Sectoral Analytics
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

### Tab 4: Adaptive Management
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

---

*This portfolio demonstrates advanced MEAL capabilities in data integration, statistical analysis, and evidence-based adaptive management. All data presented is synthetic and anonymized for demonstration purposes. See Ethical Note in the main repository for full compliance statement.*
