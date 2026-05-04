# Project 03: AGRICULTURAL MEAL System Design & Implementation

## People in Need (PIN) Afghanistan | Ghazni Province

| **Attribute** | **Details** |
|---------------|-------------|
| **Project** | AGRICULTURAL (AFG/12682) |
| **Location** | Malistan & Ajristan Districts, Ghazni Province |
| **Duration** | December 2024 – November 2025 |
| **Donor** | Agenzia Italiana per la Cooperazione allo Sviluppo (AICS) via Alliance2015 Consortium |
| **My Role** | MEAL Officer |
| **Team Managed** | 14 MEAL staff (enumerators, assistants, data clerks) |

---

## 1. Project Context & Theory of Change

The AGRICULTURAL project (AFG/12682) operates in Malistan and Ajristan districts of Ghazni Province, where recurrent drought and limited irrigation trap households in cycles of food insecurity. Within PIN's resilience strategy, this intervention targets the **agricultural-water nexus** because input scarcity and water deficits are the binding constraints preventing recovery.

### Theory of Change

**If** smallholder farmers — especially female-headed households — receive quality inputs, rehabilitated water infrastructure, and livestock assets, **and if** communities participate in cash-for-work canal rehabilitation, **then** households will diversify food sources and reduce hunger gaps, **ultimately contributing to** improved food security and reduced negative coping strategies across 36 villages.

---

## 2. MEAL Plan Architecture

### 2.1 Results Framework

| **Level** | **Indicator** | **Target** | **Data Source** | **Collection Method** |
|-----------|---------------|------------|---------------|----------------------|
| **Outcome 1** | % HH with acceptable food consumption score (FCS ≥ 35) | 70% | HH survey | Kobo/ODK, baseline/endline |
| **Outcome 1** | % HH using <3 negative coping strategies (rCSI ≤ 18) | 65% | HH survey | Kobo/ODK, quarterly |
| **Outcome 2** | % villages with functional water management committees | 80% | Key informant interviews | Kobo/ODK + qualitative, endline |
| **Output 1.1** | Farmers receiving wheat seed/fertilizer (disaggregated by sex) | 2,400 (40% female) | Distribution records | Kobo/ODK registration |
| **Output 1.2** | Kitchen gardens maintained ≥2 seasons | 800 | Physical verification | Kobo/ODK + geotagged photos |
| **Output 2.1** | Canal/kareze meters rehabilitated through CFW | 9,500m | Engineering records | Kobo/ODK + blueprints, monthly |
| **Output 2.2** | Water points constructed/rehabilitated | 187 | Infrastructure checklist | Physical verification, quarterly |
| **Output 3.1** | Livestock/poultry kits distributed (≥75% 6-month survival) | 1,200 | Follow-up survey | Kobo/ODK, 3 & 6 months |
| **Output 3.2** | Animals vaccinated through CAHWs | 15,000 | CAHW logbooks | Monthly aggregation |
| **Output 3.3** | Individuals reached with hygiene promotion (disaggregated by sex) | 4,800 (50% female) | Attendance registers | Kobo/ODK, monthly |

### 2.2 Indicator Tracking Table (ITT)

| **Indicator** | **Frequency** | **Responsible** | **Collection Tool** | **Review** |
|---------------|---------------|-----------------|---------------------|------------|
| FCS and rCSI | Baseline, Endline, Quarterly | MEAL Officer + Assistants | Kobo/ODK HH survey | Monthly data review |
| Wheat/fertilizer distribution | Real-time (daily) | MEAL Assistants | Kobo/ODK registration | Weekly during distributions |
| Kitchen garden survival | Monthly | Field Enumerators | Kobo/ODK + photos | Monthly dashboard refresh |
| Canal/kareze rehabilitation | Monthly | MEAL Officer + Engineers | Kobo/ODK measurement + GPS | Monthly |
| Water point functionality | Quarterly | MEAL Assistants | Kobo/ODK infrastructure checklist | Quarterly |
| Livestock retention/survival | 3 & 6-month follow-up | Enumerators | Kobo/ODK follow-up | After each round |
| Animal vaccination | Monthly | MEAL Assistants | Paper → Excel → ITT | Monthly |
| Hygiene promotion reach | Daily tally, monthly sum | Enumerators | Kobo/ODK attendance | Monthly |

### 2.3 Sampling Strategy

I designed a **stratified two-stage cluster sample** with villages stratified by district (Malistan/Ajristan) and elevation band, selected via probability proportional to size. Within villages, households were selected by systematic random sampling from community-compiled lists.

Using the formula:

```
n = Z² · p(1-p) / e²
```

With **Z = 1.96**, **p = 0.50**, and **e = 0.07**, the minimum sample was **196**, inflated by a design effect of **1.5**, yielding **300 households** (150 per district). This achieves **±5.7% precision** on prevalence indicators, within the AICS threshold of **±7%**.

All sampled household GPS coordinates were field-validated to prevent substitution bias.

---

## 3. Tools & Systems I Built

### 3.1 Kobo/ODK XLSForm Structure

I programmed all tools using XLSForm with three integrated sheets:

| **Sheet** | **Content** |
|-----------|-------------|
| **survey** | 127 questions across 6 modules (demographics, food security, water access, agriculture, assets, women's decision-making) with skip logic and bilingual constraint messages |
| **choices** | Cascade select filters (district → village → water source) to prevent entry errors, with English/Dari labels |
| **settings** | `form_id` as `AGR_YYYYMMDD_vX.X`, `instance_name` concatenating `district-village-hh` for traceability, encryption for sensitive modules, Dari as `default_language` |

### 3.2 Data Flow Architecture

```
Field (KoboCollect)
    ↓ Offline caching; sync twice daily at sub-office WiFi hubs
Kobo Server
    ↓ Constraint validation; JSON export
Secured OneDrive Folder
    ↓ Daily cleaning in Excel (logical checks on age consistency, FCS sums)
Excel / SPSS
    ↓ Weighting and cross-tabulations
Power BI
    ↓ Weekly refresh; donor report generation
Pre-formatted Word Templates
    ↓ AICS and Alliance2015 reports
```

### 3.3 Dashboard Design

The Power BI dashboard has four **weekly-refreshed tabs**:

| **Tab** | **Content** |
|---------|-------------|
| **Reach & Disaggregation** | Cumulative beneficiaries by sex/district/activity |
| **Food Security** | FCS/rCSI trends by district |
| **Infrastructure** | GPS map of rehabilitated canals, progress bars, CFW wage-days |
| **Data Quality** | Submission counts by enumerator, missing data rates, GPS validation green/red flags |

---

## 4. Capacity Building: 3-Day Enumerator Training

| **Day** | **Session** | **Hours** | **Content & Exercise** |
|---------|-------------|-----------|------------------------|
| **1** | MEAL, Ethics & Consent | 3h | Theory of Change, do-no-harm, PSEA. Role-play informed consent. |
| | KoboCollect & Form Navigation | 7h | Tablet basics, 6 survey modules, FCS scoring. Practice submissions + shadow scoring. |
| **2** | GPS, Photography & Interview Skills | 6h | Geopoint capture (<10m accuracy), photo consent, rapport-building, women's module. Mock interviews in Dari/Pashto. |
| | Field Simulation | 4h | Full mock surveys in peri-urban community; peer review. |
| **3** | Data Quality & Troubleshooting | 3h | Missing data checks, sync failures, escalation protocols. Debug corrupted forms. |
| | Security & Incident Response | 2h | Check-in protocols, checkpoint navigation. Table-top road-closure scenario. |
| | Certification | 3h | Written test (FCS calculation, consent, GPS) + practical assessment. **90% pass required**; all 12 enumerators certified. |

---

## 5. Data Quality Assurance (DQA) Protocol

| **#** | **Measure** | **Standard** | **Implementation** |
|-------|-------------|------------|--------------------|
| 1 | Missing Data Rate | **<5%** | Kobo constraints + daily Excel check; >5% triggers enumerator coaching |
| 2 | GPS Validation | **100% valid geopoints, <10m accuracy** | Kobo accuracy filter; 10% random field verification |
| 3 | Photo Verification | **100% timestamped, geotagged photos** | Kobo `image` with geotag; 20% manual review |
| 4 | Double-Entry Match | **100% paper-to-digital consistency** | Two assistants independently enter; zero discrepancy tolerance |
| 5 | Spot-Check Coverage | **10% of interviews supervised within 48h** | Random selection; 10-question verification; <10% deviation threshold |

### DQA Process Flow

```
Enumerator Submission (KoboCollect)
    ↓ Auto-validation (constraints, required fields, GPS accuracy)
Kobo Server
    ↓ Daily export to Excel
Data Quality Check
    ├─ Missing data scan
    ├─ Logical consistency checks (age vs. HH composition, FCS sum = 0–112)
    ├─ Duplicate detection (CNIC + phone)
    ├─ GPS outlier flagging (>50m from village centroid)
    └─ Photo completeness verification
    ↓
Issues flagged → Enumerator callback (24h resolution target)
    ↓
Clean dataset → Power BI refresh → ITT update
```

---

## 6. Analysis & Reporting: Baseline Findings

I analyzed **300 weighted baseline surveys** in SPSS. Three findings shaped operations:

### Food Security
Only **34%** reported acceptable FCS — well below the 70% target — with **71%** using 3+ negative coping strategies. Female-headed households were significantly more likely to employ emergency asset sales (χ² = 8.4, p < 0.01). This validated timing input distributions before the lean season.

### Water Access
Mean walking time to water was **42 minutes** (Ajristan highlands: **61 minutes**). **43%** of shallow wells dried July–September. Households without functional karezes were **2.3× more likely** to report water-borne illness, reinforcing kareze rehabilitation priority.

### Gender Roles
Women made independent crop decisions in only **12%** of male-headed households despite performing **67%** of agricultural labor. We redesigned kitchen garden targeting to explicit female-beneficiary registration, added women-only trainings, and added women's decision-making as a standalone indicator.

---

## 7. Adaptive Management Example

Midline data in March 2025 showed **38% poultry mortality** at 3 months, exceeding the 25% ceiling. I triangulated Kobo follow-up data with qualitative interviews and found:
- No follow-up vaccination was scheduled for the Newcastle disease season
- Feed storage guidance was inadequate for mountain winters

I presented evidence to the Project Manager and facilitated a learning session. The team approved:
1. A **month-3 vaccination round**, funded by reallocating 4% of hygiene promotion savings
2. **Revised training on poultry housing insulation**

I updated the Kobo follow-up form, revised the ITT logic, and documented the change in the donor variance report. By 6 months, mortality dropped to **19%**, demonstrating the MEAL system was **operationally consequential**, not merely compliance-driven.

---

## 8. Database Schema & System Architecture

### 8.1 Core Database Tables

```sql
-- Master beneficiary registry
CREATE TABLE beneficiaries (
    beneficiary_id VARCHAR(20) PRIMARY KEY,  -- e.g., AGR-MLT-001-25
    district VARCHAR(50),
    village VARCHAR(50),
    hh_head_name VARCHAR(100),
    gender_hh_head VARCHAR(10),
    age INTEGER,
    family_size INTEGER,
    male_members INTEGER,
    female_members INTEGER,
    children_members INTEGER,
    phone_number VARCHAR(15),
    idp_returnee_host_status VARCHAR(20),
    vulnerability_score INTEGER CHECK (vulnerability_score BETWEEN 0 AND 10),
    priority_rank INTEGER,
    consent_given BOOLEAN,
    registration_date DATE,
    enumerator_id VARCHAR(10),
    baseline_survey_id VARCHAR(20),
    gps_latitude DECIMAL(10,8),
    gps_longitude DECIMAL(11,8),
    gps_accuracy DECIMAL(5,1),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Distribution tracking
CREATE TABLE distributions (
    distribution_id SERIAL PRIMARY KEY,
    beneficiary_id VARCHAR(20) REFERENCES beneficiaries(beneficiary_id),
    activity_type VARCHAR(50),  -- Wheat_Kit, Garden_Kit, Poultry_KG, etc.
    input_subtype VARCHAR(50),  -- seed variety, fertilizer type
    quantity DECIMAL(8,2),
    unit VARCHAR(20),
    batch_number VARCHAR(20),
    distribution_date DATE,
    distribution_location VARCHAR(50),
    recipient_signature BOOLEAN,
    verified_by_meal BOOLEAN,
    verification_date DATE,
    photo_references TEXT[],
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Food security surveys (FCS, rCSI)
CREATE TABLE food_security_surveys (
    survey_id VARCHAR(20) PRIMARY KEY,
    beneficiary_id VARCHAR(20) REFERENCES beneficiaries(beneficiary_id),
    survey_round VARCHAR(20),  -- baseline, midline, endline, quarterly_1, etc.
    survey_date DATE,
    enumerator_id VARCHAR(10),
    fcs_score INTEGER CHECK (fcs_score BETWEEN 0 AND 112),
    rcsi_score INTEGER CHECK (rcsi_score BETWEEN 0 AND 56),
    fcs_acceptable BOOLEAN GENERATED ALWAYS AS (fcs_score >= 35) STORED,
    rcsi_low_coping BOOLEAN GENERATED ALWAYS AS (rcsi_score <= 18) STORED,
    cereal_days INTEGER,
    pulses_days INTEGER,
    vegetables_days INTEGER,
    fruit_days INTEGER,
    meat_days INTEGER,
    milk_days INTEGER,
    sugar_days INTEGER,
    oil_days INTEGER,
    coping_strategy_rations BOOLEAN,
    coping_strategy_borrow BOOLEAN,
    coping_strategy_reduce_meals BOOLEAN,
    coping_strategy_restrict_adult BOOLEAN,
    gps_latitude DECIMAL(10,8),
    gps_longitude DECIMAL(11,8),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Infrastructure tracking
CREATE TABLE infrastructure (
    infra_id VARCHAR(20) PRIMARY KEY,
    village VARCHAR(50),
    infra_type VARCHAR(50),  -- canal, kareze, well, reservoir
    status VARCHAR(20),  -- planned, under_rehab, functional, non_functional
    length_meters DECIMAL(8,2),
    cfw_labor_days INTEGER,
    cfw_women_labor_days INTEGER,
    completion_date DATE,
    gps_latitude DECIMAL(10,8),
    gps_longitude DECIMAL(11,8),
    verification_photo_url TEXT,
    water_committee_established BOOLEAN,
    committee_members_female INTEGER,
    committee_members_total INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Livestock follow-up
CREATE TABLE livestock_followup (
    followup_id SERIAL PRIMARY KEY,
    beneficiary_id VARCHAR(20) REFERENCES beneficiaries(beneficiary_id),
    kit_type VARCHAR(20),  -- poultry, small_ruminant
    followup_round VARCHAR(10),  -- 3_month, 6_month
    followup_date DATE,
    original_count INTEGER,
    surviving_count INTEGER,
    mortality_count INTEGER,
    mortality_cause VARCHAR(100),
    vet_access_used BOOLEAN,
    shelter_adequate BOOLEAN,
    feed_storage_adequate BOOLEAN,
    gps_latitude DECIMAL(10,8),
    gps_longitude DECIMAL(11,8),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Water point functionality
CREATE TABLE water_points (
    water_point_id VARCHAR(20) PRIMARY KEY,
    village VARCHAR(50),
    water_source_type VARCHAR(30),  -- shallow_well, deep_well, kareze, spring
    functionality_status VARCHAR(20),  -- functional, broken, seasonal
    construction_date DATE,
    rehabilitation_date DATE,
    depth_meters DECIMAL(5,1),
    yield_lph DECIMAL(6,2),  -- liters per hour
    walking_time_minutes INTEGER,
    gps_latitude DECIMAL(10,8),
    gps_longitude DECIMAL(11,8),
    last_functionality_check DATE,
    check_photo_url TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- CFRM log
CREATE TABLE cfrm_log (
    cfrm_id VARCHAR(20) PRIMARY KEY,
    category VARCHAR(30),  -- inclusion_error, payment_delay, quality_complaint, protection_concern, suggestion, info_request
    submission_date DATE,
    resolution_date DATE,
    status VARCHAR(20),  -- open, in_progress, resolved, escalated
    beneficiary_id VARCHAR(20) REFERENCES beneficiaries(beneficiary_id),
    description TEXT,
    resolution_notes TEXT,
    escalated_to VARCHAR(50),
    satisfaction_rating INTEGER CHECK (satisfaction_rating BETWEEN 1 AND 5),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Hygiene promotion attendance
CREATE TABLE hygiene_sessions (
    session_id VARCHAR(20) PRIMARY KEY,
    village VARCHAR(50),
    session_date DATE,
    topic VARCHAR(50),
    male_attendees INTEGER,
    female_attendees INTEGER,
    child_attendees INTEGER,
    total_attendees INTEGER GENERATED ALWAYS AS (male_attendees + female_attendees + child_attendees) STORED,
    trainer_id VARCHAR(10),
    photos_verified BOOLEAN,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 8.2 Data Warehouse Star Schema for Analytics

```
                    fact_distributions
                    ├─ dim_beneficiary (beneficiary_id, demographics, vulnerability)
                    ├─ dim_date (date_id, year, month, quarter, season)
                    ├─ dim_location (village_id, district, elevation_band, cluster_id)
                    ├─ dim_activity (activity_id, sector, output, indicator)
                    └─ dim_enumerator (enumerator_id, name, district, certification_date)

                    fact_food_security
                    ├─ dim_beneficiary
                    ├─ dim_date
                    ├─ dim_location
                    └─ dim_survey_round

                    fact_infrastructure
                    ├─ dim_location
                    ├─ dim_date
                    └─ dim_infra_type
```

---

## 9. Professional Impact Statement

This assignment was the bridge from **MEAL Assistant to MEAL Officer**. I owned the **full system lifecycle**:
- Translating donor logframes into XLSForms
- Managing 14 MEAL staff
- Enforcing data quality in low-connectivity environments
- Converting raw data into evidence that reshaped implementation

MEAL leadership in contexts like Ghazni is not about perfect datasets — it is about designing **resilient systems** that tolerate offline gaps and enumerator turnover while producing donor-grade evidence. The AGRICULTURAL project prepared me for senior MEAL roles by proving I can manage multi-output resilience frameworks, navigate Alliance2015 consortium reporting, and translate between field enumerators and AICS compliance officers.

**The system I built did not just track change; it became an instrument for it.**
