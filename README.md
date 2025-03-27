# Salesforce-Recruitment-Management-App
# 🧑‍💻 Salesforce Recruitment Management App Implementation 🧑‍💻
---
## STEP 1: Project Overview

The **Recruitment Management App** is designed to streamline and automate the hiring process within an organization. It features a suite of Salesforce tools like custom objects, flows, validation rules, reports, dashboards, and automated workflows. The goal is to enhance candidate tracking, job requisition management, interview scheduling, offer management, and overall recruitment process efficiency.


![Salesforce Recruitment Management App ](https://github.com/user-attachments/assets/1e3a1975-55a9-4259-8798-72b023649e38)
---
## STEP 2: Custom Objects and Fields

### 2.1 Job Position  
**Fields**:  
- Position Title (Text)  
- Department (Picklist)  
- Location (Text)  
- Salary Range (Currency)  
- Employment Type (Picklist)  
- Status (Picklist: Open, Closed, On-Hold)  
- Description (Long Text Area)

### 2.2 Candidate  
**Fields**:  
- Full Name (Text)  
- Email (Email)  
- Phone (Phone)  
- Resume (File Upload)  
- Source (Picklist: LinkedIn, Indeed, Referral, Website, Other)  
- Application Date (Date)  
- Status (Picklist: Applied, Screened, Interviewed, Offered, Rejected, Hired)

### 2.3 Application (Junction Object: Job Position <-> Candidate)  
**Fields**:  
- Candidate (Lookup)  
- Job Position (Lookup)  
- Application Status (Picklist)  
- Interview Date (Date/Time)  
- Feedback (Long Text)

### 2.4 Interview  
**Fields**:  
- Candidate (Lookup)  
- Interviewer (User Lookup)  
- Interview Type (Picklist: Technical, HR, Final Round)  
- Scheduled Date (Date/Time)  
- Notes (Text Area)

### 2.5 Recruitment Campaign  
**Fields**:  
- Campaign Name (Text)  
- Platform (Picklist: Social Media, Job Board, Referral)  
- Start Date (Date)  
- End Date (Date)  
- Budget (Currency)  
- Campaign Status (Picklist: Planned, Active, Completed)

### 2.6 Recruiter Assignment  
**Fields**:  
- Recruiter (Lookup - User)  
- Department (Picklist)  
- Job Count (Number)

### 2.7 Offer Letter  
**Fields**:  
- Candidate (Lookup)  
- Job Position (Lookup)  
- Offer Date (Date)  
- Salary Offered (Currency)  
- Status (Picklist: Draft, Sent, Accepted, Rejected)

### 2.8 Background Check  
**Fields**:  
- Candidate (Lookup)  
- Status (Picklist: Initiated, Cleared, Issues Found)  
- Notes (Long Text Area)

### 2.9 Hiring Manager Feedback  
**Fields**:  
- Candidate (Lookup)  
- Manager (Lookup - User)  
- Feedback Date (Date)  
- Rating (Number 1-5)  
- Comments (Long Text)

---

## STEP 3: Page Layouts and Compact Layouts

### Page Layouts  
- **Job Position Layout**: Fields grouped by General Info, Requirements, and Compensation. Related lists: Applications, Interviews.  
- **Candidate Layout**: Candidate profile, Resume, Status tracking, Application history.  
- **Application Layout**: Feedback, Interview Date, Application Status.  
- **Offer Letter Layout**: Salary Offered, Offer Date, Status.

### Compact Layouts  
- **Candidate**: Name, Email, Phone, Status.  
- **Job Position**: Position Title, Department, Status.  
- **Application**: Candidate Name, Status, Job Position.

---

## STEP 4: Validation Rules

- **Job Position**: Ensure salary range is greater than 0: `Salary_Range__c <= 0`.  
- **Candidate**: Application Date cannot be in the future: `Application_Date__c > TODAY()`.  
- **Offer Letter**: Salary Offered must be greater than 10,000: `Salary_Offered__c < 10000`.

---
## STEP 5: Automation with Flows

### Screen Flows
- **Candidate Quick Application Form**: Create candidate record and application in one screen.
- **Hiring Manager Feedback Submission**: Let managers rate and submit feedback.

### Record-Triggered Flows
- **Auto-Assign Recruiter Based on Department** (Job Position trigger).
- **Update Candidate Status when Offer Sent**.
- **Create Background Check Record Automatically on Offer Acceptance**.

### Scheduled Flows
- **Weekly Interview Summary Emails to Recruiters**.
- **Follow-up Emails to Inactive Candidates**.

### Auto-Launched Flows
- **Generate Offer Letter Record**.
- **Send Notifications for Background Check Completion**.
---
## STEP 6: Security Enhancements

### User Management (Org with 75 Users)  
**Profiles**:  
- System Administrator  
- Recruiter  
- Hiring Manager  
- HR Analyst  
- Read-Only Executive

### Permission Sets  
- Interview Access  
- Offer Management  
- Background Check Access  
- Campaign Management

### Roles  
- CEO → VP HR → HR Manager → Recruiters  
- Department Heads → Hiring Managers

### User Assignment  
- 35 Recruiters  
- 20 Hiring Managers  
- 10 HR Admins  
- 10 Executives & Analysts

### Object Security Level Settings (CRUD Permissions)  

| Object                     | Recruiter | Hiring Manager | HR Analyst | Executive |
|----------------------------|-----------|----------------|------------|-----------|
| Job Position               | CRED      | Read           | Read       | Read      |
| Candidate                  | CRED      | Read           | Read       | Read      |
| Application                | CRED      | Read           | Read       | Read      |
| Offer Letter               | Read      | Read           | CRED       | Read      |
| Background Check           | Read      | Read           | CRED       | No Access |
| Hiring Manager Feedback    | No Access | CRED           | Read       | Read      |
| Recruitment Campaign       | Read      | Read           | CRED       | Read      |

---

## STEP 7: Reports and Dashboards

### Reports  
- Active Applications by Job Title  
- Candidate Source Analysis  
- Recruiter Performance (Applications Processed)  
- Time to Hire by Department  
- Budget Utilization by Campaign  

### Dashboards  
- **Recruitment Overview Dashboard**:  
  - Open Positions by Department (Bar Chart)  
  - Application Funnel (Funnel Chart)  
  - Hires by Month (Line Chart)  
  - Campaign ROI (Donut Chart)  
  - Interview Schedule (List Component)

---

## STEP 8: Conclusion

This final version of the **Salesforce Recruitment Management App** includes all essential custom objects and fields while ensuring a well-structured security model, reporting system, and automation. The app was deployed successfully, offering a streamlined recruitment process for Nexus Cloud Technology ( enterprise-level organizations).
