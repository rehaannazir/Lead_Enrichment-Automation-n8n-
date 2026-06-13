# 🚀 Lead Enrichment & Automation

<p align="center">
  <b>An end-to-end n8n automation workflow for lead validation, enrichment, scoring, PDF generation, CRM handling, and sales follow-up.</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-n8n-orange" />
  <img src="https://img.shields.io/badge/Category-Sales%20Automation-blue" />
  <img src="https://img.shields.io/badge/Project-Capstone-success" />
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen" />
</p>

---

## 📌 Project Overview

**Lead Enrichment & Automation** is a complete business automation workflow built with **n8n**.

This workflow takes a new lead submission, validates the email, enriches company/person data, checks CRM status, assigns a lead score, categorizes the lead, creates a professional PDF, uploads it to Google Drive, updates Google Sheets, notifies the sales team, schedules an event, and sends follow-up emails.

The project represents a real-world workflow used by:

- Sales Operations Teams
- Business Analysts
- Content Coordinators
- Sales Managers
- B2B Agencies
- AI Automation Agencies

---

## 🎯 Business Problem

Sales teams often receive raw leads with incomplete or unverified information.

Manual lead processing usually involves:

- Checking whether the email is valid
- Searching company details manually
- Checking if the lead already exists in CRM
- Categorizing lead quality
- Creating lead documents
- Sending internal notifications
- Scheduling follow-ups
- Sending welcome and follow-up emails

This process wastes time and creates operational delays.

This workflow solves the problem by automating the complete lead management pipeline.

---

## ✅ What This Workflow Does

```text
New Lead Submission
        ↓
Basic Email Validation
        ↓
Hunter Email Verification
        ↓
Lead Enrichment
        ↓
Company Validation
        ↓
CRM Search
        ↓
Lead Score Assignment
        ↓
Lead Categorization
        ↓
PDF Generation
        ↓
Google Drive Upload
        ↓
Google Sheets Update
        ↓
Sales Notification
        ↓
Calendar Scheduling
        ↓
Welcome Email
        ↓
Follow-up Email
```

---

## 🧠 Workflow Architecture

The workflow is divided into different business departments to simulate a real company process.

| Department | Responsibility |
|---|---|
| **User-End** | Receives lead submission |
| **Sales OP / Intern** | Validates incoming lead email |
| **Business Analyst** | Enriches and validates company data |
| **Sales OP / Intern** | Searches CRM and scores the lead |
| **Content Coordinator** | Creates PDF and uploads it to Drive |
| **Sales Manager** | Contacts, schedules, and follows up with lead |


---

## 1️⃣ User-End

The workflow starts when a new lead submits a form.

### Responsibilities

- Captures lead entry
- Starts the automation
- Sends lead data to validation stage

### Main Node

- **On Lead Entry**

---

## 2️⃣ Sales OP / Intern — Email Validation

This section checks whether the lead email is valid or not.

### Responsibilities

- Monitor incoming submissions
- Perform basic email validation
- Verify email through Hunter
- Separate valid and invalid leads
- Add invalid leads to nurture sheet

### Main Nodes

- **Basic Email Validation**
- **Hunter**
- **Hunter Email Validation**
- **Appending Nurture Lead**

### Logic

```text
If email format is invalid:
    Add lead to nurture list

If email format is valid:
    Send email to Hunter API

If Hunter verifies email:
    Continue to enrichment

If Hunter rejects email:
    Add lead to nurture list
```

---

## 3️⃣ Business Analyst — Lead Enrichment

This stage enriches the lead and validates company information.

### Responsibilities

- Enrich lead data
- Extract company details
- Check company validity
- Purify and clean data
- Store incomplete company records separately
- Pass valid company leads to next stage

### Main Nodes

- **Enrich Lead**
- **Company Validation**
- **Adding Nurture Lead**
- **Nurturing Lead**
- **Merge**

### Logic

```text
If company data exists:
    Send lead forward for CRM search and scoring

If company data is missing:
    Add lead to nurturing sheet
```

---

## 4️⃣ Sales OP / Intern — CRM Search & Lead Scoring

This section checks whether the lead is new or already exists in CRM, then assigns a lead score.

### Responsibilities

- Search lead in CRM
- Check whether lead is new or existing
- Merge lead data
- Assign lead score
- Categorize lead into High, Medium, or Low
- Route lead based on quality

### Main Nodes

- **Search CRM**
- **Merge1**
- **Assigning Lead Score**
- **Based on Categories**
- **Approving Lead**
- **Inappropriate Lead**

---

## 📊 Lead Scoring System

The workflow assigns a score based on lead quality and completeness.

| Condition | Score |
|---|---:|
| Valid email | +20 |
| Verified company | +25 |
| Service requirement available | +20 |
| Country available | +10 |
| New lead in CRM | +15 |
| Complete profile | +10 |

### Lead Categories

| Score Range | Category | Action |
|---|---|---|
| 70–100 | High | Send to content and sales team |
| 40–69 | Medium | Send for approval |
| 0–39 | Low | Add to inappropriate/nurture list |

### Routing Logic

```text
If lead score is High:
    Send to Content Coordinator
    Send to Sales Manager

If lead score is Medium:
    Send approval email to Sales Manager

If lead score is Low:
    Store as inappropriate lead
```

---

## 5️⃣ Content Coordinator — PDF Generation

This section creates a professional lead PDF and stores it in Google Drive.

### Responsibilities

- Copy Google Docs template
- Replace placeholders with lead data
- Generate PDF file
- Upload PDF to Google Drive
- Save finalized lead entry in Google Sheets

### Main Nodes

- **Copying Template**
- **Updating Template**
- **Downloading PDF**
- **Uploading PDF to Drive**
- **Finalised Lead Entry**

### PDF Automation Flow

```text
Copy Google Docs Template
        ↓
Update Template With Lead Data
        ↓
Download Document as PDF
        ↓
Upload PDF to Google Drive
        ↓
Save Final Lead Entry
```

---

## 6️⃣ Sales Manager — Communication & Follow-up

This section manages lead contact, scheduling, welcome message, and follow-up.

### Responsibilities

- Notify account sales executive
- Schedule Google Calendar event
- Send welcome email
- Wait for follow-up time
- Send follow-up email

### Main Nodes

- **Contacting**
- **Scheduling Event**
- **Welcoming Lead**
- **Wait**
- **Follow Up**

### Follow-up Flow

```text
Qualified Lead
        ↓
Notify Sales Executive
        ↓
Schedule Calendar Event
        ↓
Send Welcome Email
        ↓
Wait
        ↓
Send Follow-up Email
```

---

## 🛠️ Tools & Integrations Used

| Tool / Service | Purpose |
|---|---|
| **n8n** | Main workflow automation platform |
| **Hunter API** | Email verification |
| **HTTP Request Node** | Lead enrichment API integration |
| **Google Sheets** | Lead storage and tracking |
| **Google Docs** | Lead PDF template |
| **Google Drive** | PDF file storage |
| **Gmail** | Welcome and follow-up emails |
| **Google Calendar** | Lead meeting scheduling |
| **Airtable / CRM** | CRM search and lead status |
| **Slack** | Internal sales notification |

---

## 📂 Repository Structure

```text
lead-enrichment-automation/
│
├── README.md
├── .gitignore
├── .env.example
│
├── workflows/
│   └── lead-enrichment-workflow.json
│
├── docs/
│   ├── Lead_Eneichment.png
│   ├── Lead_Enrichment_01.png
│   ├── Lead_Enrichment_02.png
│   └── Lead_Enrichment_03.png
│
├── data/
│   └── sample_leads.csv
│
└── notes/
    └── setup-steps.md
```

---

## 🔐 Environment Variables

Create a `.env` file locally.

```env
HUNTER_API_KEY=your_hunter_api_key_here
ENRICHMENT_API_KEY=your_enrichment_api_key_here
GOOGLE_SHEET_ID=your_google_sheet_id_here
GOOGLE_DRIVE_FOLDER_ID=your_google_drive_folder_id_here
GOOGLE_DOC_TEMPLATE_ID=your_google_doc_template_id_here
CRM_API_KEY=your_crm_api_key_here
SLACK_WEBHOOK_URL=your_slack_webhook_url_here
```

> Never upload your real `.env` file to GitHub.

---

## 🚀 How to Use

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/lead-enrichment-automation.git
cd lead-enrichment-automation
```

### 2. Import Workflow into n8n

1. Open n8n
2. Go to **Workflows**
3. Click **Import from File**
4. Select this file:

```text
workflows/lead-enrichment-workflow.json
```

### 3. Connect Credentials

Connect credentials for:

- Hunter API
- Google Sheets
- Google Docs
- Google Drive
- Gmail
- Google Calendar
- Slack
- CRM / Airtable

### 4. Update Node Settings

Update these values inside your n8n nodes:

- Google Sheet ID
- Google Docs Template ID
- Google Drive Folder ID
- API endpoints
- API keys
- Gmail account
- Slack webhook
- Calendar settings

### 5. Run the Workflow

You can run the workflow using:

- Manual Trigger
- n8n Form Trigger
- Webhook Trigger
- CRM Lead Entry Trigger

---

## 🧩 Key Features

- Lead form submission trigger
- Basic email validation
- Hunter email verification
- Lead enrichment
- Company validation
- CRM duplicate checking
- Lead score assignment
- High, Medium, and Low categorization
- Conditional routing
- Google Docs template automation
- PDF generation
- Google Drive upload
- Google Sheets final entry
- Slack sales notification
- Gmail welcome email
- Google Calendar scheduling
- Automated follow-up email

---

## 💼 Business Value

This workflow reduces manual sales operations work by automating the full lead-processing pipeline.

### Before Automation

```text
Manual lead checking
Manual email verification
Manual company research
Manual CRM search
Manual lead scoring
Manual document creation
Manual team notification
Manual follow-up
```

### After Automation

```text
Lead submitted once
System validates email
System enriches company data
System checks CRM
System assigns lead score
System routes lead automatically
System creates PDF
System uploads file to Drive
System updates Sheets
System schedules follow-up
System contacts lead
```

---

## 🏢 Real-World Use Cases

This automation can be used by:

- AI automation agencies
- B2B sales teams
- SaaS companies
- Lead generation agencies
- CRM teams
- Marketing departments
- Business development teams
- Freelancers offering automation services

---

## 🧠 Skills Demonstrated

- n8n workflow automation
- API integration
- Sales automation
- CRM automation
- Lead enrichment
- Email verification
- Conditional routing
- Data cleaning
- Google Workspace automation
- PDF generation
- Workflow architecture
- Business process automation
- No-code/low-code automation engineering

---

## 📌 Project Status

```text
Status: Completed
Type: Capstone Project
Category: Lead Enrichment / Sales Automation
Platform: n8n
```

---

## 🏆 Capstone Achievement

This capstone project demonstrates the ability to design and automate a complete business workflow.

It combines:

- Lead validation
- Lead enrichment
- CRM search
- Lead scoring
- Department routing
- PDF generation
- Drive storage
- Sales notification
- Calendar scheduling
- Email follow-up

into one professional end-to-end automation system.

---

## 👨‍💻 Author

**Rehan Nazir**  
AI Automation Learner | Data Science Student | n8n Workflow Builder

---

## ⭐ Final Note

This project is built to demonstrate real-world automation thinking, business workflow design, and the ability to create systems that save time, reduce manual work, and improve sales operations.
