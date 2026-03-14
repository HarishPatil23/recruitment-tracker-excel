

#  Recruitment Tracker — Excel Data Analytics Project

> An end-to-end recruitment performance tracker built in Microsoft Excel, designed to simulate real-world agency recruiting operations and demonstrate hands-on data analysis skills alongside 4 years of recruitment experience.

---

##  Project Overview

This project replicates how a staffing agency or internal recruitment team might track requisitions, candidates, and recruiter activity — then transforms that raw operational data into meaningful performance insights through a structured data model, pivot analysis, and an interactive dashboard.

Built entirely from scratch in Excel, this tracker covers the full recruitment lifecycle: from opening a job requisition to sourcing, screening, interviewing, and hiring.

---

##  Objectives

- Demonstrate data analysis skills applied to a recruitment domain
- Build a structured, analysis-ready data model from raw activity logs
- Track KPIs that matter in recruiting: time-to-hire, source effectiveness, funnel conversion
- Showcase Excel proficiency (data modeling, COUNTIFS, IF, IFERROR, MINIFS, TEXT, AND, OR, pivot tables, dashboards)

---

##  File Structure

```
recruitment-tracker-excel.xlsx
│
├── Raw_Data_Reqs           → Job requisitions (Req ID, Title, Client, Dates, Priority)
├── Raw_Data_Candidates     → Candidate pipeline (200 records across 10 reqs)
├── Raw_Data_Activities     → Recruiter activity log (478 activity events)
├── Lookup_Tables           → Reference data (Recruiters, Stages, Sources)
│
├── Data_Model              → Cleaned, joined, flag-enriched analytical dataset
├── Pivot_Backend           → COUNTIFS-based pivot calculations (no pivot table dependency)
├── Pivot_Charts            → Chart-ready aggregations
└── Dashboard               → KPI summary view with visual indicators
```

---

##  Data Description

### Raw Data — Requisitions (`Raw_Data_Reqs`)
| Column | Description |
|---|---|
| `Req_ID` | Unique requisition identifier (R001–R010) |
| `Job_Title` | Role being hired (Business Analyst, Data Analyst, Data Engineer) |
| `Client` | Hiring company (Amazon, Microsoft, Google) |
| `Open_Date` | Date requisition was opened |
| `Close_Date` | Date requisition was closed/filled |
| `Priority` | Business priority (High / Medium / Low) |

### Raw Data — Candidates (`Raw_Data_Candidates`)
| Column | Description |
|---|---|
| `Candidate_ID` | Unique candidate identifier (C0001–C0200) |
| `Req_ID` | Linked requisition |
| `Recruiter` | Assigned recruiter (Harish, Anita, Sneha, Rahul) |
| `Source` | Sourcing channel (LinkedIn, Indeed, Monster, CareerBuilder, ZipRecruiter) |
| `Resume_Date` | Date resume was received |
| `Current_Stage` | Last known pipeline stage (Sourced → Screened → Interview → Offer → Hired / Rejected) |
| `Years_Exp` | Candidate's years of experience |
| `Location` | Candidate location |

### Raw Data — Activities (`Raw_Data_Activities`)
| Column | Description |
|---|---|
| `Activity_ID` | Unique activity identifier |
| `Candidate_ID` | Linked candidate |
| `Recruiter` | Recruiter who performed the activity |
| `Activity_Type` | Type of activity (Resume Submitted, Screen Completed, Hired, etc.) |
| `Activity_Date` | Date activity occurred |

---

##  Data Model

The `Data_Model` sheet is the analytical core of this project. It joins candidate data with activity logs to derive:

| Derived Column | Logic |
|---|---|
| `Submission_Date` | MINIFS on activity log to find earliest "Resume Submitted" date per candidate |
| `Interview_Date` | MINIFS on activity log to find earliest "Interview Scheduled" date per candidate|
| `Hire_Date` | MINIFS on activity log to find earliest "Hired" date per candidate |
| `Submission_Flag` | 1 if Submission_Date is not blank, else 0 |
| `Interview_Flag` | 1 if Interview_Date is not blank, else 0 |
| `Hire_Flag` | 1 if Hire_Date is not blank, else 0|
| `Days_To_Submit` | Resume_Date → Submission_Date (skipped if dates missing or illogical) |
| `Time_to_Interview` | Submission_Date → Interview_Date (skipped if dates missing or illogical) |
| `Time_to_Hire` | Submission_Date → Hire_Date (skipped if dates missing or illogical) |
| `Invalid_Hire_Flag` | AND logic — flags records where Hire_Date is before Submission_Date |

---

##  Key Metrics & Insights

| Metric | Value |
|---|---|
| Total Candidates Tracked | 200 |
| Total Hires | 93 |
| Overall Hire Rate | ~46.5% |
| Avg. Days to Submit | ~12 days |
| Avg. Time to Hire | ~4 days (post-submission) |

### Hiring Funnel
```
Sourced → Screened → Interview → Offer → Hired
  200       ~171       ~105       ~28      93
```

### Recruiter Performance
| Recruiter | Candidates |
|---|---|
| Harish | 59 |
| Anita | 52 |
| Sneha | 48 |
| Rahul | 41 |

### Top Sourcing Channels
| Source | Candidates |
|---|---|
| Indeed | 46 |
| ZipRecruiter | 43 |
| CareerBuilder | 37 |
| Monster | 37 |
| LinkedIn | 37 |

---

##  Dashboard

The `Dashboard` sheet provides a high-level summary of recruitment performance including:

- Total Candidates and Total Hires (KPI cards)
- Hiring funnel visualization
- Source effectiveness breakdown
- Recruiter-level performance comparison
- Requisition status by client and priority

---

##  Excel Skills Demonstrated

- **Data Modeling** — joining multiple raw tables into a single analytical layer
- **MINIFS** — extracting earliest activity dates from a log by matching Candidate ID and Activity Type
- **COUNTIFS** — building pivot-style aggregations without pivot table limitations
- **Flag Engineering** — creating binary indicators for funnel analysis
- **Date Arithmetic** — calculating time-to-hire, days-to-submit, and processing speed
- **Data Validation** — dropdown controls using lookup tables
- **Pivot Tables & Charts** — visual summaries of recruiter and source performance
- **Dashboard Design** — clean KPI layout with structured layout and named ranges
- **Data Quality Checks** — `Invalid_Hire_Flag` to catch logical inconsistencies in data

---

##  Why This Project

With 4 years of hands-on recruitment experience, I understand the data that gets generated in a hiring workflow — but it often goes unanalyzed. This project bridges that gap by applying data analysis thinking to a domain I know deeply.

The goal was to go beyond just tracking candidates in a spreadsheet, and instead build something that answers real questions a recruiting team or hiring manager would ask:

- Which sourcing channel is most effective?
- How long does it take to move a candidate through the funnel?
- Which recruiter closes the most hires?
- Are there data quality issues in how activities are being logged?

---

##  How to Use

1. Download `Recruitment_Tracker_From_Scratch.xlsx`
2. Enable editing and macros if prompted
3. Start with the `Raw_Data_*` sheets to understand the source data
4. Review `Data_Model` to see how the data is joined and enriched
5. Explore `Pivot_Backend` and `Pivot_Charts` for the aggregation logic
6. Open `Dashboard` for the final summary view

The `Recruitment_Tracker_From_Scratch_-_Raw_Untouched.xlsx` file contains only the raw input sheets with no transformations applied — useful for understanding the starting point of the project.

---

##  Tools Used

- Microsoft Excel (primary tool)
- Formulas: MINIFS, COUNTIFS, IF, IFERROR, AND, OR, TEXT
- Pivot Tables, Slicers
- Named Ranges, Data Validation

---

##  About

Built by a recruiter with 4 years of experience in staffing and talent acquisition, expanding into data analytics to bring deeper insight into hiring operations.


---

*This is a personal portfolio project. All candidate and company data is entirely synthetic and generated for demonstration purposes.*
