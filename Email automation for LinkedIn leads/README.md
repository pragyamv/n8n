# Automated Lead Outreach with Personalized Emails

This project implements an email automation workflow using n8n, Google Sheets, OpenAI, and Gmail. It takes raw lead data from a spreadsheet, generates personalized outreach emails with AI, and updates the source sheet with new information for tracking and follow-up.

---

## Overview

The workflow reads lead data (name, role, company, LinkedIn URL, and snippets) from a Google Sheet. For each lead, an AI model crafts a multi-section personalized email draft. The results are written back into the sheet as new columns, ensuring a structured record of outreach attempts. Finally, Gmail drafts are automatically created, ready for review and sending.

---

## Key Features

- **Personalized Email Generation**
  
  Each lead is enriched with AI-generated content, including:  
  -- &nbsp;Subject line  
  -- &nbsp;Icebreaker (based on LinkedIn content/snippets)  
  -- &nbsp;Main pitch  
  -- &nbsp;Call-to-offer (CTO)  
  -- &nbsp;P.S. reference  

- **Spreadsheet Updates**
  
  The workflow appends new columns (`Subject`, `Icebreaker`, `Pitch`, `CTO`, `PS`) into the same row of the Google Sheet, ensuring every draft is traceable to its original lead.

- **Email Draft Creation**
  
  Draft emails are generated in Gmail, pre-filled with personalized content, so they can be reviewed, edited if needed, and sent.

---

## Typical Applications

-- &nbsp;**Lead Generation** → Automating outreach campaigns with a personal touch at scale.  
-- &nbsp;**Sales Prospecting** → Quickly producing tailored cold emails based on prospect roles and LinkedIn activity.  
-- &nbsp;**Marketing Operations** → Maintaining an organized record of communications, ensuring accountability and iteration.  
-- &nbsp;**Recruiting** → Personalizing candidate outreach with structured, reusable templates.  

---

## Workflow Architecture

1. &nbsp;**Google Sheet with Leads** → (Get row(s) in sheet)  
The workflow starts by pulling rows from the sheet.

2. **AI Model Generates Email Templates** → (Message a model)  
OpenAI takes the row data and generates subject, icebreaker, pitch, CTO, and PS.

3. **Update Sheet with Generated Content** → (Update row in sheet)  
The workflow appends these new fields into the same row of the sheet.

4. **Gmail Create Drafts** → (Create a draft)  
Draft email is created in Gmail using the personalized fields.

5. **Personalized Email Ready for Review**  
Output is a ready-to-send draft per lead.

```mermaid
flowchart TD
    A[Google Sheet with Leads] --> B[Fetch Lead Rows]
    B --> C[AI Model Generates Email Templates]
    C --> D[Update Sheet with Generated Content]
    D --> E[Gmail Create Drafts]
    E --> F[Personalized Email Ready for Review]

