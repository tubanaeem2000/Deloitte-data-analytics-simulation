# Deloitte Australia – Data Analytics Virtual Job Simulation

This repository contains my completed work for the **Deloitte Australia Data Analytics** virtual job simulation on [Forage](https://www.theforage.com/), covering telemetry data analysis with Tableau and a forensic pay-equality audit in Excel.

## 📋 About the Simulation

Daikibo Industrials is a fictional multinational manufacturing company. As a member of Deloitte's Data & Analytics practice, the simulation involved two client-facing tasks:

1. **Data Analysis** – Investigate machine downtime across Daikibo's factories using IoT telemetry data in Tableau.
2. **Forensic Technology** – Support an internal investigation into gender pay equality by classifying an "Equality Score" dataset in Excel.

## 🗂️ Repository Structure

```
├── task-1-data-analysis/
│   ├── daikibo-telemetry-data.json.zip   # Raw IoT telemetry dataset (~160k records)
│   ├── dashboard_reference.png           # Reference screenshot of the final Tableau dashboard
│   └── daikibo-dashboard.twbx            # (optional) Tableau packaged workbook
│
├── task-2-forensic-technology/
│   ├── Equality_Table.xlsx               # Original dataset (Factory, Job Role, Equality Score)
│   └── Equality_Table_solved.xlsx        # Completed dataset with Equality Class column
│
└── README.md
```

## 🔧 Task 1: Data Analysis

**Goal:** Quantify machine downtime per factory and per device type, using telemetry sent every 10 minutes from Daikibo's manufacturing equipment.

**Tools:** Tableau Desktop

**Approach:**
- Imported the raw JSON telemetry data (160,704 records) into Tableau, expanding all schema levels (`location`, `data` fields).
- Created a calculated field `Unhealthy` = `IF [Status]="unhealthy" THEN 10 ELSE 0 END`, representing 10 minutes of potential downtime per unhealthy reading.
- Built two bar charts: **Down Time per Factory** and **Down Time per Device Type**.
- Combined both into a single dashboard, using the factory chart as a filter for the device-type chart.

**Key finding:** `daikibo-factory-seiko` had the highest total downtime (480 minutes), driven entirely by its **LaserWelder** units.

![Dashboard reference](task-1-data-analysis/dashboard_reference.png)

## ⚖️ Task 2: Forensic Technology

**Goal:** Classify each Factory / Job Role's pay "Equality Score" (range −100 to +100, 0 = ideal) into one of three categories to support an internal gender-pay investigation.

**Tools:** Microsoft Excel

**Classification logic:**

| Equality Score | Class |
|---|---|
| −10 to +10 | Fair |
| −20 to −11, or +11 to +20 | Unfair |
| below −20, or above +20 | Highly Discriminative |

Implemented as a live Excel formula (not a hardcoded value), so it recalculates automatically if scores change:

```excel
=IF(AND(C2>=-10,C2<=10),"Fair",IF(OR(C2<-20,C2>20),"Highly Discriminative","Unfair"))
```

**Result summary (37 roles across 4 factories):**
- Fair: 19
- Unfair: 11
- Highly Discriminative: 7

## 🎓 About

Completed by **Tuba** as part of the Deloitte Australia Data Analytics job simulation, as portfolio evidence of Tableau dashboarding and Excel data classification skills.

## 📜 Certificate

Forage issues a completion certificate after both tasks are submitted and approved — see [Forage Dashboard](https://www.theforage.com/dashboard) for the verification link.
