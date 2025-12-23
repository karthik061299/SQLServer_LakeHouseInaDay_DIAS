====================================================

Author: AAVA

Date: 

Description: Conceptual Data Model and Data Constraints for UTL Utilization Reporting System

====================================================

# PART 1 CONCEPTUAL DATA MODEL

## 1 Domain Overview

The reporting system covers the Resource Utilization and Billing Management domain This domain encompasses workforce management timesheet tracking project allocation billing operations and utilization analytics for consulting resources across multiple geographical locations India US Canada Mexico LATAM The system tracks resource allocation billable vs non billable hours FTE calculations project assignments and various business classifications to support operational and financial reporting

## 2 List of Entities with Descriptions

### 2 1 Resource
Description Represents individual consultants FTEs and contractors working on various projects This entity captures personal information employment details and resource categorization

### 2 2 Project Assignment
Description Represents the allocation of resources to specific client projects including billing rates project duration and assignment details

### 2 3 Timesheet
Description Captures daily time entries submitted by resources including standard time overtime double time sick time and time off hours

### 2 4 Approved Timesheet
Description Represents timesheet entries that have been approved by managers clients or approvers for billing purposes

### 2 5 Client
Description Represents client organizations for whom resources are allocated and billed

### 2 6 Project
Description Represents specific projects or engagements under which resources work including project type billing type and project classification

### 2 7 Calendar
Description Represents date dimension with working days weekends and business day calculations

### 2 8 Holiday
Description Represents location specific holidays for different geographical regions US India Canada Mexico

### 2 9 Workflow
Description Represents hiring and onboarding workflow processes for resources including process stages and approval levels

### 2 10 Monthly Headcount
Description Represents monthly aggregated headcount data including starts terminations movements and FTE calculations

### 2 11 Organization Hierarchy
Description Represents organizational structure including business units departments circles communities and leadership assignments

## 3 Entity Attributes with Business Names and Descriptions

### 3 1 Resource Entity Source report 392 all SchTask New Monthly HC Report

1 First Name Legal first name of the resource
2 Last Name Legal last name of the resource
3 Employee Code Unique identifier assigned to each resource GCI ID
4 Job Title Official job title or role designation of the resource
5 Employee Type Classification of employment Consultant FTE Contractor
6 Employee Category Categorization based on employment arrangement
7 Start Date Date when the resource started with the organization
8 Termination Date Date when the resources employment ended
9 Final End Date Actual last working day of the resource
10 Employee Status Current status of the resource Active Terminated etc
11 Termination Reason Reason for resource termination or offboarding
12 Visa Type Immigration visa classification for the resource
13 Location Primary work location or office location of the resource
14 Payroll Location Location used for payroll processing purposes
15 Resource Type Onsite or Offshore classification
16 Subtier Company Legal entity or subsidiary employing the resource
17 Standard Job Title Standardized job title for reporting and classification
18 Experience Level Title Experience level classification Junior Mid Senior etc
19 Role Family Broad role category or job family
20 Sub Role Family Specific role subcategory within the role family
21 Grade Name Organizational grade or level assigned to the resource
22 Community Practice or community group the resource belongs to
23 Circle Organizational circle or team assignment
24 Tower Technology or service tower classification
25 Candidate Email Official email address of the resource
26 Candidate City City where the resource resides
27 Candidate State State where the resource resides
28 Gender Gender identification of the resource
29 Veteran Status Veteran classification for compliance reporting
30 EEO Classification Equal Employment Opportunity classification

### 3 2 Project Assignment Entity Source report 392 all Hiring Initiator Project Info

1 Assignment Start Date Date when the resource assignment to the project began
2 Assignment End Date Date when the resource assignment to the project ended
3 PO Start Date Purchase order start date for the assignment
4 PO End Date Purchase order end date for the assignment
5 Bill Rate Standard Time Hourly billing rate for standard time hours
6 Bill Rate Overtime Hourly billing rate for overtime hours
7 Bill Rate Units Unit of measurement for billing rate hourly daily etc
8 Pay Rate Standard Time Hourly pay rate to the resource for standard time
9 Pay Rate Units Unit of measurement for pay rate
10 Salary Fixed salary amount for the resource
11 Salary Units Unit of measurement for salary annual monthly etc
12 Net Bill Rate Net billing rate after deductions or adjustments
13 Loaded Pay Rate Pay rate including all loaded costs and benefits
14 Gross Profit Gross profit amount generated from the assignment
15 Gross Profit Margin Gross profit margin percentage for the assignment
16 Markup Percentage Markup percentage applied to the pay rate
17 Actual Markup Actual markup percentage achieved
18 Maximum Allowed Markup Maximum markup percentage allowed per policy
19 Billing Type Classification as Billable or Non Billable NBL
20 Resource Billing Type Specific billing classification for the resource
21 Project Billing Type Billing type classification at project level
22 Business Type Type of business arrangement Contract SOW etc
23 Assignment Status Current status of the assignment
24 Is Overtime Allowed Indicator whether overtime is permitted for this assignment
25 Is Double Time Allowed Indicator whether double time is permitted
26 Is Overtime Billable Indicator whether overtime hours are billable to client
27 Expected Hours Expected working hours per day for the assignment
28 Weekly Cycle Week cycle definition for timesheet submission
29 Transition Type Type of transition or movement for the assignment
30 Timesheet Manager Manager responsible for timesheet approval

### 3 3 Timesheet Entity Source Timesheet New vw consultant timesheet daywise

1 Period Ending Date End date of the timesheet period
2 Calendar Date Specific date for which hours are recorded
3 Week Date Week ending date for the timesheet entry
4 Standard Time Hours Regular working hours submitted by the resource
5 Overtime Hours Overtime hours submitted by the resource
6 Double Time Hours Double time hours submitted by the resource
7 Time Off Hours Time off or leave hours recorded
8 Holiday Hours Holiday hours recorded
9 Sick Time Hours Sick leave hours recorded
10 Non Billable Standard Time Non billable standard time hours
11 Non Billable Overtime Non billable overtime hours
12 Non Billable Double Time Non billable double time hours
13 Non Billable Sick Time Non billable sick time hours
14 Submitted Hours Total hours submitted by the consultant
15 Year Month Year and month identifier in YYYYMM format

### 3 4 Approved Timesheet Entity Source vw billing timesheet daywise ne

1 Period Ending Date End date of the approved timesheet period
2 Calendar Date Specific date for which approved hours are recorded
3 Week Date Week ending date for the approved timesheet
4 Approved Standard Time Hours Standard time hours approved by manager
5 Approved Overtime Hours Overtime hours approved by manager
6 Approved Double Time Hours Double time hours approved by manager
7 Approved Sick Time Hours Sick time hours approved by manager
8 Approved Non Billable Standard Time Non billable standard time hours approved
9 Approved Non Billable Overtime Non billable overtime hours approved
10 Approved Non Billable Double Time Non billable double time hours approved
11 Approved Non Billable Sick Time Non billable sick time hours approved
12 Billable Indicator Flag indicating if the timesheet entry is billable

### 3 5 Client Entity Source report 392 all Hiring Initiator Project Info

1 Client Code Unique identifier for the client organization
2 Client Name Official name of the client organization
3 Client Type Classification of client type
4 Client Sector Industry sector of the client
5 Client Region Geographical region where client operates
6 Client Entity Legal entity name of the client
7 Parent Account Name Parent or holding company name
8 Super Merged Name Consolidated parent client name for reporting
9 Merged Name Merged or grouped client name
10 Client Group Client grouping for reporting purposes
11 End Client Name Ultimate end client if different from direct client
12 End Client Sector Industry sector of the end client
13 Is SOW Indicator whether client operates under Statement of Work
14 Client Manager Primary manager at client side
15 Invoice Send To Contact person for invoice submission
16 Invoice Address Line 1 First line of invoice mailing address
17 Invoice Address Line 2 Second line of invoice mailing address
18 Invoice City City for invoice mailing address
19 Invoice State State for invoice mailing address
20 Invoice Zip Code Zip code for invoice mailing address
21 Invoicing Terms Terms and conditions for invoicing
22 Payment Terms Payment terms agreed with the client
23 MSP Name Managed Service Provider name if applicable
24 Vertical Name Industry vertical classification

### 3 6 Project Entity Source report 392 all Hiring Initiator Project Info

1 Project Name Official name of the project
2 ITSS Project Name Project name in ITSS system
3 Project Type Classification of project type
4 Project Category Category classification for the project
5 Project City City where project is located
6 Project State State where project is located
7 Project Zip Code Zip code of project location
8 Project Location Country Country where project is located
9 Delivery Model Delivery model for the project Onsite Offshore Hybrid
10 Practice Type Practice or service line type
11 Opportunity Name Sales opportunity name linked to project
12 MS Project Name Microsoft Project system project name

### 3 7 Calendar Entity Source DimDate

1 Date Calendar date
2 Day of Month Day number within the month
3 Day Name Name of the day Monday Tuesday etc
4 Week of Year Week number within the year
5 Month Month number
6 Month Name Name of the month
7 Month of Quarter Month number within the quarter
8 Quarter Quarter number 1 2 3 4
9 Quarter Name Name of the quarter
10 Year Year value
11 Month Year Combined month and year
12 Days in Month Total number of days in the month
13 YYYYMM Year and month in YYYYMM format

### 3 8 Holiday Entity Source holidays holidays India holidays Canada holidays Mexico

1 Holiday Date Date of the holiday
2 Holiday Description Description or name of the holiday
3 Location Geographical location where holiday is observed US India Canada Mexico
4 Source Type Source or type of holiday classification

### 3 9 Workflow Entity Source SchTask

1 Workflow Process Name Name of the workflow process
2 Process Level Current level or stage in the workflow
3 Last Level Final level in the workflow process
4 Workflow Status Current status of the workflow
5 Initiator Person who initiated the workflow
6 Initiator Email Email address of the workflow initiator
7 Date Created Date when workflow was created
8 Date Completed Date when workflow was completed
9 Existing Resource Indicator if resource already exists
10 Legal Entity Legal entity associated with the workflow
11 Comments Comments or notes on the workflow

### 3 10 Monthly Headcount Entity Source New Monthly HC Report

1 Year Month Year and month identifier
2 Begin Headcount Headcount at the beginning of the month
3 Starts New Project New project starts during the month
4 Starts Internal Movements Internal movements or transfers
5 Terminations Terminations during the month
6 Other Project Ends Other project endings
7 Offboard Offboarding count
8 End Headcount Headcount at the end of the month
9 Voluntary Terminations Voluntary termination count
10 Net Addition Net addition to headcount
11 Derived Revenue Derived revenue for the period
12 Derived Gross Profit Derived gross profit for the period
13 Backlog Revenue Backlog revenue
14 Backlog Gross Profit Backlog gross profit
15 Expected Total Hours Expected total hours for the month
16 Business Days Number of business days in the month

### 3 11 Organization Hierarchy Entity Source report 392 all New Monthly HC Report

1 Business Unit Business unit classification
2 Department Department name
3 Sub Department Sub department classification
4 Circle Organizational circle
5 Community Community or practice group
6 Tower Technology or service tower
7 Recruiting Manager Manager responsible for recruiting
8 Resource Manager Manager responsible for resource management
9 Sales Representative Sales representative assigned
10 Inside Sales Inside sales person assigned
11 Recruiter Recruiter assigned to the resource
12 Delivery Leader Delivery leader for the engagement
13 Portfolio Leader Portfolio leader assignment
14 Client Partner Client partner assigned
15 Market Leader Market leader for the region
16 Account Owner Account owner for the client
17 Vertical Name Vertical or industry name
18 Region Group Regional grouping
19 Business Area Business area classification NA LATAM Others India
20 Geo Group Geographical group classification

## 4 Key Performance Indicators KPIs

### 4 1 Total Hours
Description Total available working hours for a resource in a month calculated as number of working days multiplied by location specific hours 9 hours for offshore India 8 hours for onshore US Canada LATAM excluding weekends and location specific holidays
Formula Number of Working Days Location Specific Hours per Day

### 4 2 Submitted Hours
Description Total hours submitted by the resource in timesheets including Standard Time Overtime Double Time and Sick Time
Formula ST OT DT Sick Time

### 4 3 Approved Hours
Description Total hours approved by managers for billing including Approved ST Approved OT Approved DT and Approved Sick Time
Formula Approved ST Approved OT Approved DT Approved Sick Time

### 4 4 Total FTE
Description Full Time Equivalent calculated based on submitted hours divided by total available hours
Formula Submitted Hours Total Hours

### 4 5 Billed FTE
Description Billed Full Time Equivalent calculated based on approved hours divided by total available hours If approved hours are unavailable submitted hours are used
Formula Approved Hours Total Hours or Submitted Hours Total Hours if approved hours unavailable

### 4 6 Available Hours
Description Available hours for a resource calculated as Monthly Total Hours multiplied by Total FTE
Formula Monthly Total Hours Total FTE

### 4 7 Billed Hours
Description Total billable hours approved for billing to the client
Formula Sum of Approved Billable Hours

### 4 8 Project Utilization
Description Utilization percentage at project level calculated as Billed Hours divided by Available Hours
Formula Billed Hours Available Hours 100

### 4 9 Gross Profit
Description Gross profit generated from the assignment calculated as Net Bill Rate minus Loaded Pay Rate multiplied by hours
Formula