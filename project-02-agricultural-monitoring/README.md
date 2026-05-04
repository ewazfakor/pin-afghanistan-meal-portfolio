# Project 02: Agricultural Livelihoods Monitoring

## People in Need (PIN) Afghanistan | AICS Consortium (PIN & Cesvi)

| **Attribute** | **Details** |
|---------------|-------------|
| **Project** | Agricultural Livelihoods Restoration |
| **Location** | Malistan & Ajristan Districts, Ghazni Province |
| **Duration** | April – September 2023 (6 months) |
| **Donor** | Agenzia Italiana per la Cooperazione allo Sviluppo (AICS) |
| **Reporting To** | MEAL Officer, PIN Ghazni Field Office |
| **My Role** | MEAL Assistant |

---

## 1. Executive Summary

The AICS-funded multi-sector agricultural project aimed to restore food security and productive livelihoods for crisis-affected households in **36 villages** across Malistan and Ajristan districts. Targeting host communities, IDPs, and returnees, the intervention combined:

- Input distribution (wheat seed, Urea, DAP)
- Kitchen garden kits for women-headed households
- Poultry and small ruminant restocking
- Cash-for-work canal rehabilitation
- Animal vaccination
- Hygiene awareness sessions

As **MEAL Assistant**, I supported end-to-end monitoring across all activity streams. Over six months, I developed from primarily data entry tasks on my first project to independently leading field monitoring visits, managing the input distribution tracker for **475+ registered beneficiaries**, and conducting **5% sample verification** with GPS-tagged photo validation.

**Three contributions I am particularly proud of:**
1. Designing the Excel distribution tracker with automated pivot summaries that reduced reporting time by roughly **40%**
2. Identifying and resolving a **12-beneficiary duplication error** in the Kobo dataset before distribution day
3. Independently completing **24 post-distribution monitoring visits** across 14 villages, including culturally appropriate one-on-one interviews with **46 women beneficiaries**

---

## 2. MEAL Tools I Developed & Managed

### 2.1 Excel Input Distribution Tracker

I built and maintained the master distribution tracker that served as the **single source of truth** for all four input streams. The workbook had six sheets:

| **Sheet** | **Purpose** |
|-----------|-------------|
| `Registration_Master` | Complete beneficiary registry with demographics and vulnerability flags |
| `Distribution_Log` | Real-time logging of all distributions by input type, date, and location |
| `Verification_5pct` | Random sample verification results with pass/fail criteria |
| `Gender_Summary` | Sex-disaggregated distribution metrics for donor reporting |
| `Stock_Reconciliation` | Input stock tracking from warehouse to beneficiary |
| `Dashboard` | Pivot-based summary for weekly sitreps |

**Key columns in the master sheet:**
`Beneficiary_ID` (format: MLT-001-AG23), `District`, `Village`, `Family_Size`, `Gender_of_HH_Head`, `Vulnerability_Category` (IDP/Returnee/Host), `Input_Type` (Wheat_Kit/Poultry_KG/Small_Ruminant_KG/Garden_Kit), `Seed_Variety`, `Quantity_kg`, `Batch_Number`, `Distribution_Date`, `Recipient_Signature`, `Verified_Y/N`, and `MEAL_Notes`.

I used `SUMIFS` formulas to auto-calculate distributed quantities by village and input type, and built pivot tables on the `Dashboard` sheet that the MEAL Officer used for weekly sitreps. Data validation dropdowns on the Input_Type and Gender columns prevented entry errors during busy distribution periods. I also created a simple `COUNTIFS` flagging column that turned red if a beneficiary appeared more than once across input types, which caught duplication risks early.

### 2.2 Kobo/ODK Registration Form

I assisted the MEAL Officer in designing and testing the beneficiary registration form, then served as the primary person uploading forms to KoboToolbox, troubleshooting tablet sync issues, and cleaning incoming datasets in Excel.

The form contained **15 core fields:**

| **#** | **Field** | **Type** | **Validation** |
|-------|-----------|----------|----------------|
| 1 | Enumerator_ID | Select one | From approved enumerator list |
| 2 | Survey_Start_Time | DateTime | Auto-captured |
| 3 | District/Village | Cascading select | District → Village filter |
| 4 | GPS_Coordinates | Geopoint | <10m accuracy required |
| 5 | HH_Head_Name | Text | Mandatory |
| 6 | Respondent_Name | Text | If different from HH head |
| 7 | Gender | Select one | Male/Female |
| 8 | Age | Integer | 18–120 |
| 9 | Phone_Number | Text | Dari format validation |
| 10 | IDP/Returnee/Host_Status | Select one | Category required |
| 11 | Vulnerability_Score | Integer | 0–10, PIN internal criteria |
| 12 | Priority_Rank_in_Community_List | Integer | 1–500 |
| 13 | Consent_Given | Yes/No | Skip logic for field 14 |
| 14 | HH_Members_Count | Integer | Male/Female/Children disaggregated |
| 15 | Photo_of_HH_Head | Image | Geotagged |

Skip logic ensured that field 14 only appeared if consent was given. I ran logic checks weekly — looking for duplicate GPS points within 50 meters, impossible phone numbers, and blank mandatory fields — and flagged these to field supervisors within **24 hours**.

### 2.3 Photo Monitoring Protocol

I standardized our photo monitoring to ensure every image was usable for donor reporting and internal spot-checks. The protocol required:

1. **GPS enabled** on all tablets/phones so EXIF metadata was embedded
2. **Naming convention:** `VillageCode_InputType_Date_BenID_001` (e.g., `KRM_Wheat_230618_MLT-089_001`)
3. **Minimum three angles** per distribution site:
   - Wide shot of queue/activity
   - Close-up of beneficiary receiving input
   - Input packaging/batch number
4. **All photos uploaded** to the shared PIN OneDrive folder within **48 hours** with a matching log sheet

Over the project, I personally verified and archived **1,240+ photos**, checking that GPS coordinates fell within the correct village boundary using a simple overlay I created in Google Earth Pro.

---

## 3. Field Monitoring Activities

I conducted four types of monitoring visits, progressively taking on more independence:

### Input Distribution Spot-Checks (May & June)
I attended three wheat seed and fertilizer distributions in Karamul and Sorkh Parsa villages. My role was to:
- Verify that registered beneficiaries matched ID cards
- Weigh random Urea bags to confirm quantities matched the tracker (**10 random bags; all within 0.5kg of the 50kg target**)
- Ensure female-headed households were served through the same queue rather than a separate delayed line
- Interview 18 beneficiaries on the spot using a short 5-question verbal survey about whether they understood planting instructions

### Kitchen Garden Post-Distribution Monitoring (July)
I led solo visits to **eight villages** in Malistan to check kitchen garden kit adoption among **46 women recipients**. Because these interviews required privacy and cultural sensitivity, I worked with a female community mobilizer who made introductions while I recorded responses on a paper form later digitized in Excel. I checked:
- Was the kit received complete?
- Were seeds planted?
- Any pest or water issues?

I disaggregated all responses by village and by woman's age bracket (18–30, 31–45, 46+) to see if younger women faced different barriers.

### CFW Canal Site Verification (August)
I visited two cash-for-work canal rehabilitation sites with the MEAL Officer. I:
- Counted daily laborers against the attendance sheet
- Verified that **30% were women** (project requirement)
- Checked that tools and safety conditions met PIN standards

I used a simple tally sheet and later cross-referenced it against the payment reconciliation file.

### Livestock Kit Survival Check (September)
I completed a follow-up visit to **15 households** in Ajristan who had received poultry kits three months prior. I:
- Counted surviving birds
- Asked about mortality causes
- Checked whether beneficiaries had accessed the veterinary hotline PIN had established
- Recorded GPS coordinates for each household to build a simple distribution map the MEAL Officer used in the final report

### Gender Considerations
In all mixed-gender monitoring settings, I ensured:
- Female enumerators were present for women respondents
- Interviews were scheduled at times women could speak freely
- Verbal consent was always sought separately from male household heads when possible

---

## 4. Data Quality & Verification

### 4.1 5% Sample Verification Process

For every distribution round, I randomly selected 5% of beneficiaries using Excel's `RAND()` function sorted against the master list, **stratified by village** to ensure geographic spread. I visited these households in person (or called if access was restricted), verified their identity against the original registration, confirmed they received the correct input type and quantity, and asked whether any payment or in-kind contribution had been requested improperly.

Results were logged in the `Verification_5pct` sheet with pass/fail criteria. Across all rounds, my verification sample covered **24 households; 23 passed**. The one failure was a poultry kit recipient whose bird count was miscounted on distribution day — resolved by correcting the master log.

### 4.2 Catching the Duplication Error

In mid-May, while preparing the wheat distribution list, I noticed that the `COUNTIFS` flagging column I had built showed two beneficiaries — "MLT-089" and "MLT-091" — appearing under both wheat and poultry registrations with identical phone numbers. I cross-checked the raw Kobo export and found that an enumerator in Karamul village had accidentally duplicated a household during two separate registration drives. I flagged this to the MEAL Officer, we confirmed with the field team that it was one family, and I removed the duplicate row before any distribution occurred. This small catch prevented a **12-kit over-distribution** and demonstrated to me the real value of building automated checks into everyday tools.

---

## 5. CFRM & Accountability

I supported the **Complaint and Feedback Response Mechanism (CFRM)** by maintaining the feedback log and ensuring community awareness. At every distribution I attended, I displayed the CFRM poster (hotline number, complaint boxes, expected response time) and verbally explained the mechanism to at least **five beneficiaries** per event.

Over six months, I logged **34 feedback/complaint entries** in the CFRM tracker:

| **Category** | **Count** | **Examples** |
|--------------|-----------|--------------|
| Information requests | 19 | "When is the poultry distribution?" |
| Complaints about input quality | 8 | 3 about torn seed bags, 5 about delayed fertilizer arrival |
| Suggestions | 4 | Villagers requesting specific wheat varieties |
| Safeguarding concerns | 3 | Forwarded immediately to MEAL Officer and Protection focal point |

All non-sensitive complaints were resolved within the **5-day target window**. I prepared the monthly CFRM summary tables that fed into the MEAL Officer's reports to the Consortium Coordinator.

---

## 6. Results Table

The table below shows a representative sample from my Excel distribution tracker, illustrating the structure and data quality standards I maintained across all **475+ registered beneficiaries**.

| **Beneficiary_ID** | **Village** | **Gender_HH** | **Input_Type** | **Quantity** | **Unit** | **Distribution_Date** | **Verified** | **MEAL_Notes** |
|:-------------------|:------------|:--------------|:---------------|-------------:|:---------|:----------------------|:-------------|:---------------|
| MLT-001-AG23 | Karamul | Male | Wheat_Kit | 50 | kg | 2023-05-18 | Y | GPS confirmed; photo archived |
| MLT-012-AG23 | Karamul | Female | Garden_Kit | 1 | kit | 2023-06-22 | Y | Interviewed with mobilizer present |
| MLT-023-AG23 | Sorkh Parsa | Male | Wheat_Kit | 50 | kg | 2023-05-18 | Y | Weighed bag: 50.2kg |
| MLT-034-AG23 | Shinkai | Male | Poultry_KG | 1 | kit | 2023-07-08 | Y | 5 hens + 1 rooster; all alive at check |
| MLT-045-AG23 | Shinkai | Female | Garden_Kit | 1 | kit | 2023-06-22 | Y | Seeds planted within 3 days |
| AJS-056-AG23 | Nawroz | Male | Wheat_Kit | 50 | kg | 2023-05-25 | Y | IDP household; access road poor |
| AJS-067-AG23 | Nawroz | Female | Poultry_KG | 1 | kit | 2023-07-15 | N | Phone verification only; visit planned |
| AJS-078-AG23 | Barai | Male | Small_Ruminant_KG | 1 | kit | 2023-07-29 | Y | Goat healthy; vaccination card shown |
| AJS-089-AG23 | Barai | Male | Wheat_Kit | 50 | kg | 2023-05-25 | Y | Duplicate risk flagged; cleared |
| MLT-091-AG23 | Karamul | Female | Garden_Kit | 1 | kit | 2023-06-22 | Y | Young mother (24); enthusiastic adopter |

### Quantified Outputs I Contributed to Tracking

| **Activity Stream** | **Target** | **Achieved (Tracked)** | **My Role** |
|:--------------------|-----------:|-----------------------:|:------------|
| Wheat seed + Urea + DAP distribution | 190 farmers | 187 | Maintained master tracker; spot-checked 5% |
| Kitchen garden kits | 95 women | 93 | Led post-distribution monitoring visits |
| Poultry/small ruminant kits | 190 families | 188 | Verified distribution logs; survival check |
| CFW canal/well rehabilitation | 3 schemes | 3 | Daily laborer counts & gender ratio checks |
| Hygiene awareness sessions | 3,000 people | 2,847 | Attendance tally verification at 4 events |
| Animal vaccination | 15,000 animals | 14,620 | Logged numbers from vet reports into tracker |

---

## 7. Database & Dashboard Design

### 7.1 Proposed Relational Database Schema

```
Table: beneficiaries
- beneficiary_id (PK)          -- e.g., MLT-001-AG23
- district
- village
- hh_head_name
- gender_hh_head
- family_size
- phone_number
- idp_returnee_host_status
- vulnerability_score
- priority_rank
- consent_given
- registration_date
- enumerator_id (FK)

Table: distributions
- distribution_id (PK)
- beneficiary_id (FK)
- input_type
- seed_variety
- quantity_kg
- batch_number
- distribution_date
- recipient_signature
- verified_yn
- mecal_notes

Table: verifications
- verification_id (PK)
- beneficiary_id (FK)
- verification_date
- verification_method
- pass_fail
- discrepancy_notes
- mecal_officer_approval

Table: photos
- photo_id (PK)
- beneficiary_id (FK)
- file_name                    -- VillageCode_InputType_Date_BenID_001
- gps_latitude
- gps_longitude
- photo_angle                  -- wide/close-up/batch
- upload_date
- verified_yn

Table: cfrm_log
- cfrm_id (PK)
- category                     -- info/complaint/suggestion/safeguarding
- submission_date
- resolution_date
- status
- beneficiary_id (FK)
- description
- resolution_notes

Table: enumerators
- enumerator_id (PK)
- name
- gender
- district_assigned
- training_completion_date
- certification_status
```

### 7.2 Proposed Power BI Dashboard Tabs

| **Tab** | **Purpose** | **Key Visuals** |
|---------|-------------|-----------------|
| **Executive Summary** | Management KPIs | Total beneficiaries; % female-headed; distribution progress by input type |
| **Distribution Tracking** | Real-time logistics | Map by village; stock reconciliation gauge; batch tracking table |
| **Verification Results** | Quality assurance | Pass/fail rate by village; trend of discrepancies; pending verifications |
| **Gender Analysis** | Sex-disaggregated metrics | Distribution by gender; female head participation; women's adoption rates |
| **Photo Archive** | Visual monitoring | Gallery with GPS overlay; missing photo flags; angle completeness check |
| **CFRM Tracker** | Accountability | Complaint volume by category; resolution time; open cases alert |

---

## 8. Professional Growth Statement

This project was a decisive step in my transition from data entry support to a monitoring practitioner with **independent field responsibilities**. I learned that strong MEAL is not just about clean datasets — it is about designing simple tools (like my `COUNTIFS` flag or photo naming protocol) that make quality control **inevitable rather than optional**. Conducting solo monitoring visits, navigating gender-sensitive interviews in conservative rural communities, and resolving a real data discrepancy under time pressure gave me the confidence and field credibility that directly prepared me for promotion to MEAL Officer on PIN's next agricultural livelihoods program.
