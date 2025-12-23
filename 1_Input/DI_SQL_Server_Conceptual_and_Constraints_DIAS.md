====================================================

Author: AAVA

Date: 

Description: Conceptual Data Model and Data Constraints for DIAS Reporting System

====================================================

# PART 1: Conceptual Data Model

## 1. Domain Overview
The reporting requirements and data model focus on Workforce Utilization, Project Billing, Timesheet Management, Resource Allocation, and Holiday/Calendar Management for a global IT services organization. The domain covers resource time tracking, project assignments, billing categorization, FTE calculations, and holiday exclusions for accurate reporting and analytics.

## 2. List of Entity Names with Descriptions

1. **New_Monthly_HC_Report**
   - Contains monthly headcount and workforce data, including business area, SOW status, vertical, region, and project information.
2. **SchTask**
   - Represents workflow tasks related to resource management, including candidate names, employee codes, and task types.
3. **Hiring_Initiator_Project_Info**
   - Stores candidate and project information for hiring processes, including job titles, project details, and client information.
4. **Timesheet_New**
   - Captures timesheet entries for resources, including hours worked, type of hours (standard, overtime, sick, etc.), and associated dates.
5. **report_392_all**
   - Aggregates resource, project, and billing information for reporting, including billing type, category, status, and project details.
6. **vw_billing_timesheet_daywise_ne**
   - Provides day-wise approved timesheet hours for resources, categorized by billing type.
7. **vw_consultant_timesheet_daywise**
   - Provides day-wise consultant timesheet hours for resources, categorized by billing type.
8. **DimDate**
   - Calendar dimension table providing date attributes, weekends, and working days.
9. **holidays_Mexico / holidays_Canada / holidays_India / holidays**
   - Store holiday dates and descriptions for respective locations, used to exclude holidays from working day calculations.

## 3. List of Attributes for Each Entity (with Business Names and Descriptions)

### New_Monthly_HC_Report
- Business Area: Geographic business area (NA, LATAM, Others, India)
- SOW: Indicates if client is SOW or not
- Vertical Name: Industry name
- Super Merged Name: Parent client name
- New Business Type: Contract/Direct Hire/Project NBL
- Rec Region: Requirement region name
- ITSS Project Name: Project name
- IS Offshore: Indicates if resource is offshore
- Practice Type: Practice or business unit
- Portfolio Leader: Portfolio lead for reporting
- Status: Resource status (e.g., Billed, Unbilled, SGA)
- Expected Hours: Expected hours per day/month
- Expected Total Hours: Total expected hours for the period
- YYMM: Year and month indicator

### SchTask
- Candidate Name: Name of the consultant or FTE
- GCI_ID: Employee code
- Type: OnSite/Offshore indicator
- Tower: Business unit or logical grouping
- Status: Task or workflow status

### Hiring_Initiator_Project_Info
- Candidate Last Name: Candidate's last name
- Candidate First Name: Candidate's first name
- HR Candidate Job Title: Job title for the candidate
- HR Candidate Job Description: Description of the job role
- HR Candidate Employee Type: Employee type (FTE/Consultant)
- HR Project Referred By: Referrer for the project
- HR Project Start Date: Project start date
- HR Project End Date: Project end date
- HR Client Info Name: Client name
- HR Project Location City: Project location city
- HR Project Location State: Project location state

### Timesheet_New
- GCI_ID: Employee code
- PE Date: Period end date
- C Date: Calendar date
- ST: Standard hours worked
- OT: Overtime hours worked
- TIME_OFF: Time off hours
- HO: Holiday hours
- DT: Double time hours
- NON_ST: Non-standard hours
- NON_OT: Non-overtime hours
- Sick Time: Sick leave hours
- NON_Sick_Time: Non-sick leave hours
- NON_DT: Non-double time hours

### report_392_all
- First Name: Resource first name
- Last Name: Resource last name
- Employee Type: FTE/Consultant
- Client Code: Client code
- Client Name: Client name
- Job Title: Resource job title
- Billing Type: Billable/Non-Billable
- ITSS Project Name: Project name
- Status: Resource status (Billed/Unbilled/SGA)
- Category: Billing category (e.g., India Billing - Client-NBL)
- Market Leader: Market leader for the project
- Portfolio Leader: Portfolio lead
- Vertical Name: Industry vertical
- Region Group: Region grouping

### vw_billing_timesheet_daywise_ne
- GCI_ID: Employee code
- PE Date: Period end date
- Approved Hours (ST): Approved standard hours
- Approved Hours (Non_ST): Approved non-standard hours
- Approved Hours (OT): Approved overtime hours
- Approved Hours (Non_OT): Approved non-overtime hours
- Approved Hours (DT): Approved double time hours
- Approved Hours (Non_DT): Approved non-double time hours
- Approved Hours (Sick_Time): Approved sick leave hours
- Approved Hours (Non_Sick_Time): Approved non-sick leave hours

### vw_consultant_timesheet_daywise
- GCI_ID: Employee code
- PE Date: Period end date
- Consultant Hours (ST): Consultant standard hours
- Consultant Hours (OT): Consultant overtime hours
- Consultant Hours (DT): Consultant double time hours

### DimDate
- Date: Calendar date
- Day Name: Name of the day
- Month Name: Name of the month
- Year: Year
- Week Of Year: Week number
- Is Weekend: Indicates if date is a weekend
- Is Working Day: Indicates if date is a working day

### holidays_Mexico / holidays_Canada / holidays_India / holidays
- Holiday Date: Date of the holiday
- Description: Description of the holiday
- Location: Location code
- Source Type: Source of holiday data

## 4. KPI List
- Total Hours (per resource/location)
- Submitted Hours (timesheet hours submitted by resource)
- Approved Hours (timesheet hours approved by manager)
- Total FTE (Submitted Hours / Total Hours)
- Billed FTE (Approved Hours / Total Hours)
- Project Utilization (Proj UTL)
- Billed Hours
- Available Hours
- Expected Hours
- Status (Billed/Unbilled/SGA)
- Category (Billing/Project/SGA/Bench/AVA)

## 5. Conceptual Data Model Diagram (Tabular Form)

| Entity                        | Connected Entity                | Key Field(s) Used for Relationship           |
|-------------------------------|---------------------------------|----------------------------------------------|
| Timesheet_New                 | SchTask                         | GCI_ID                                      |
| Timesheet_New                 | New_Monthly_HC_Report           | GCI_ID, ITSS Project Name, YYMM              |
| Timesheet_New                 | vw_billing_timesheet_daywise_ne | GCI_ID, PE Date                              |
| Timesheet_New                 | vw_consultant_timesheet_daywise | GCI_ID, PE Date                              |
| Timesheet_New                 | DimDate                         | C Date = Date                                |
| Timesheet_New                 | holidays_*                      | C Date = Holiday Date, Location              |
| report_392_all                | New_Monthly_HC_Report           | GCI_ID, ITSS Project Name                    |
| report_392_all                | SchTask                         | GCI_ID                                       |
| report_392_all                | DimDate                         | Start Date/End Date = Date                   |
| New_Monthly_HC_Report         | DimDate                         | YYMM/Date                                    |
| SchTask                       | Hiring_Initiator_Project_Info   | Candidate Name, GCI_ID                       |
| vw_billing_timesheet_daywise_ne | DimDate                       | PE Date = Date                               |
| vw_consultant_timesheet_daywise | DimDate                       | PE Date = Date                               |
| holidays_*                    | DimDate                         | Holiday Date = Date                          |

## 6. Common Data Elements in Report Requirements
- GCI_ID (Employee Code)
- ITSS Project Name
- Status
- Category
- Billing Type
- Approved Hours
- Submitted Hours
- Available Hours
- Expected Hours
- Portfolio Leader
- Vertical Name
- Region/Location
- Date/YYMM

## 7. API Cost Calculation
- Cost for this Call: $...


# PART 2: Data Constraints

## 1. Data Expectations
1. Data should be complete for all resources, projects, and time periods referenced in the reports.
2. Hours (Submitted, Approved, Billed, Available, Expected) must be accurate and reflect actual timesheet entries and business rules.
3. Dates should be consistent and in standard formats (e.g., YYYY-MM-DD).
4. Status and Category fields should align with defined business logic and mappings.
5. Holidays must be correctly excluded from working day calculations based on location.
6. All KPIs (FTE, Utilization, etc.) must be calculated according to the formulas provided in the requirements.

## 2. Constraints
1. Mandatory Fields: GCI_ID, Project Name, Date, Hours fields (Submitted, Approved, etc.), Status, Category.
2. Uniqueness: Each timesheet entry must be unique per resource, date, and project.
3. Referential Integrity: All GCI_IDs in timesheet and reporting tables must exist in the master resource/entity tables.
4. Location-specific logic: Holiday exclusions and working hours must be based on the resource’s location.
5. No ID attributes are to be exposed in reporting outputs.
6. Status and Category values must be from the defined set in the requirements (e.g., Billed, Unbilled, SGA, Bench, AVA).
7. Hours per day: 9 for offshore (India), 8 for other locations, excluding holidays and weekends.
8. All date fields must be valid calendar dates and match the DimDate table.

## 3. Business Rules
1. Total Hours = Number of Working Days × Hours per Day (by location)
2. Submitted Hours are sourced from timesheet entries (Consultant/Approved hours, ST/OT/DT/Sick, etc.)
3. Approved Hours are sourced from manager approvals; if unavailable, use Submitted Hours.
4. Total FTE = Submitted Hours / Total Hours
5. Billed FTE = Approved Hours / Total Hours (or Submitted Hours if Approved is missing)
6. Allocation across multiple projects: Total Hours are distributed based on the ratio of Submitted Hours for each project; any difference is adjusted proportionally.
7. Status and Category are determined by business logic (see India Billing Matrix, Client Project Matrix, SGA, Bench & AVA Matrix).
8. Holidays and weekends are excluded from working day calculations using DimDate and holidays tables.
9. Portfolio Leader and Vertical Name are included for filtering and reporting in dashboards.
10. All calculations and logic must strictly follow the definitions and mappings provided in the requirements documentation.

## 4. API Cost Calculation
- Cost for this particular Api Call to LLM model: $...
