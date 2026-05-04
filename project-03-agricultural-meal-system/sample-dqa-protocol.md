# Data Quality Assurance (DQA) Protocol — AGRICULTURAL Project AFG/12682

## 1. Purpose & Scope

This protocol establishes the minimum data quality standards, verification procedures, and escalation pathways for all primary data collected under the AGRICULTURAL project (AFG/12682). It applies to:

- Household surveys (baseline, midline, endline, quarterly)
- Beneficiary registration and distribution records
- Infrastructure monitoring and verification
- Livestock follow-up surveys
- Hygiene promotion attendance registers
- Community Feedback and Response Mechanism (CFRM) logs

---

## 2. Data Quality Standards

| **Dimension** | **Standard** | **Measurement Method** | **Tolerance** | **Escalation Threshold** |
|:--------------|:-------------|:------------------------|:--------------|:-------------------------|
| **Accuracy** | Record matches source document | Random spot-check comparison | ≥95% match | <95% triggers enumerator retraining |
| **Completeness** | All required fields populated | Missing data rate calculation | <5% missing | ≥5% triggers daily enumerator coaching |
| **Consistency** | Logical relationships hold | Automated logical checks | <3% logical errors | ≥3% triggers form review |
| **Timeliness** | Data submitted within 24h of collection | Submission timestamp vs. collection date | 100% within 24h | Any delay >48h escalates to MEAL Officer |
| **Precision** | GPS accuracy within specification | GPS metadata extraction | ≥95% within 10m | <95% triggers device recalibration |
| **Validity** | Data represents intended construct | Indicator definition alignment | 100% aligned | Any misalignment triggers protocol revision |

---

## 3. Verification Procedures

### 3.1 Automated Verification (Kobo/ODK)

| **Check** | **Implementation** | **Action on Failure** |
|:----------|:--------------------|:------------------------|
| Required fields | `required = yes` in XLSForm | Form cannot be finalized |
| Constraint validation | `constraint` column with formulas | Error message displayed; enumerator must correct |
| GPS accuracy | `accuracy-threshold = 10` | Warns enumerator; submission allowed but flagged |
| Skip logic integrity | `relevant` column formulas | Questions hidden appropriately; no orphaned data |
| Date validation | `constraint = . >= 2024-12-01` | Prevents backdated or future-dated entries |
| Duplicate prevention | `unique` on beneficiary ID server-side | Rejects duplicate submissions; logs attempt |

### 3.2 Daily Data Quality Checks (Excel)

**Performed by:** Data Quality Clerk
**Timeline:** Within 4 hours of daily data export
**Tools:** Excel with standardized DQA macro

| **Check #** | **Check Name** | **Procedure** | **Flag Condition** |
|:------------|:---------------|:--------------|:-------------------|
| DQA-1 | Missing Data Scan | Count blank cells in required fields | Any required field blank |
| DQA-2 | Duplicate Detection | `COUNTIFS` on beneficiary_id + survey_date | Count > 1 for same beneficiary on same day |
| DQA-3 | GPS Outlier Flag | Compare GPS to village centroid lookup | Distance > 50m from village boundary |
| DQA-4 | Age Consistency | Verify age against household composition | Age < 18 for HH head; child age > adult age |
| DQA-5 | FCS Range Check | Sum food group days × weights | FCS < 0 or FCS > 112 |
| DQA-6 | rCSI Range Check | Sum coping strategy scores | rCSI < 0 or rCSI > 56 |
| DQA-7 | Phone Format Validation | Regex match on phone_number | Does not match `^07[0-9]{8}$` |
| DQA-8 | Enumerator Performance | Calculate submission rate per enumerator | < 80% of expected daily submissions |
| DQA-9 | Photo Completeness | Cross-reference photo log against submissions | Missing mandatory photo angles |
| DQA-10 | Temporal Consistency | Survey date vs. distribution date | Survey before registration or distribution |

### 3.3 Weekly Field Verification

**Performed by:** MEAL Officer or Senior MEAL Assistant
**Sample:** 10% of all submissions, randomly selected
**Method:** In-person spot-check or phone verification

| **Verification Step** | **Standard** | **Pass Criteria** |
|:----------------------|:-------------|:------------------|
| Beneficiary identity confirmed | Match CNIC + name + phone | All three match registration |
| Consent confirmed | Verbal re-confirmation | Beneficiary recalls consent and purpose |
| GPS location verified | Physical visit or GPS photo match | Within 10m of submission coordinates |
| Key responses verified | Re-ask 5 core questions | ≥4 match original submission |
| Photo documentation reviewed | Original photos on device/tablet | All angles present, timestamp within survey date |

### 3.4 Monthly Data Review Meeting

**Participants:** MEAL Officer, MEAL Assistants, Data Clerks, Project Manager
**Agenda:**
1. Review monthly missing data rates by enumerator
2. Review GPS accuracy trends
3. Review spot-check pass/fail rates
4. Identify recurring errors and root causes
5. Update training or form design as needed
6. Approve clean dataset for ITT update

---

## 4. Data Quality Incident Log

| **Incident ID** | **Date** | **Type** | **Description** | **Records Affected** | **Root Cause** | **Corrective Action** | **Resolved By** | **Status** |
|:----------------|:---------|:---------|:------------------|:---------------------|:---------------|:-----------------------|:----------------|:-----------|
| DQI-2025-001 | 2025-01-10 | Missing GPS | 14 submissions from Jaghatu with no GPS coordinates | 14 | Enumerator disabled GPS to save battery | Device settings locked; enumerator retrained on GPS importance | MEAL Officer | Resolved |
| DQI-2025-002 | 2025-01-14 | Duplicate Entry | 3 households registered twice in Karamul | 3 | Enumerator revisited same household without checking existing records | Added unique constraint on CNIC; pre-load existing beneficiary list on tablet | MEAL Assistant | Resolved |
| DQI-2025-003 | 2025-01-18 | FCS Error | 7 surveys with FCS > 112 | 7 | Enumerator misread "milk days" as "meat days" | Refresher training on FCS scoring; added visual aid card to enumerator kit | MEAL Officer | Resolved |

---

## 5. Roles & Responsibilities

| **Role** | **DQA Responsibilities** |
|:---------|:-------------------------|
| **MEAL Officer** | Overall DQA protocol ownership; monthly review chair; incident escalation point; donor reporting sign-off |
| **MEAL Assistants** | Daily data export and cleaning; enumerator performance tracking; spot-check execution; weekly report preparation |
| **Data Quality Clerk** | Daily automated checks (DQA-1 through DQA-10); incident logging; enumerator callback coordination |
| **Field Enumerators** | Accurate data collection per protocol; timely submission; GPS and photo compliance; immediate error reporting |
| **Project Manager** | Resource allocation for DQA; approval of corrective actions; liaison with donor on data issues |

---

## 6. Tools & Templates

| **Tool** | **Purpose** | **Format** | **Updated** |
|:---------|:------------|:-----------|:------------|
| Daily DQA Checklist | Systematic daily scanning of new submissions | Excel macro-enabled workbook | Per data export |
| Spot-Check Form | Standardized in-person verification | Kobo/ODK form + paper backup | As needed |
| Enumerator Performance Tracker | Individual submission rates, error rates, retraining needs | Excel dashboard | Weekly |
| Incident Log Template | Standardized recording of data quality issues | Excel + shared drive | Real-time |
| Data Cleaning Log | Record of all changes made to raw data | Excel with change tracking | Per cleaning session |

---

## 7. Document Control

| **Version** | **Date** | **Author** | **Changes** | **Approved By** |
|:------------|:---------|:-----------|:------------|:----------------|
| 1.0 | 2024-12-01 | MEAL Officer | Initial draft | Project Manager |
| 1.1 | 2025-01-05 | MEAL Officer | Added GPS outlier threshold (50m); added photo completeness check | MEAL Manager |
| 1.2 | 2025-01-15 | MEAL Officer | Added enumerator performance tracker; updated incident log format | Project Manager |

---

*This DQA Protocol is a living document. All team members are encouraged to suggest improvements based on field experience. Changes require MEAL Officer review and Project Manager approval.*
