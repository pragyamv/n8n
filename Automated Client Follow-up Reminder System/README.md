# **Automated Client Follow-up Reminder System**

This project implements a calendar-based follow-up automation workflow using n8n, Google Sheets, and Google Calendar. It takes client data with start dates from a spreadsheet, generates multiple follow-up reminders, and automatically creates calendar events to ensure no client follow-up is missed.

## **Overview**

The workflow reads client data from a Google Sheet. For each client, the system generates up to 9 reminders: an optional start date reminder for new clients and 8 follow-up reminders scheduled every 5 days. All reminders are automatically created as Google Calendar events, providing a structured approach to client relationship management.

## **Key Features**

--&nbsp; **Smart Start Date Detection**  
  Clients marked with "(To start)" receive an immediate reminder on their start date with the message "[Client] should start today"

--&nbsp; **Automated Follow-up Schedule**  
  Each client gets 8 follow-up reminders scheduled at 5-day intervals (days 5, 10, 15, 20, 25, 30, 35, 40)

--&nbsp; **Google Sheets Serial Date Processing**  
  Handles Google Sheets epoch format dates (e.g., 45919) and converts them to proper calendar dates

--&nbsp; **Calendar Integration**  
  Creates 15-minute calendar events at 6:00 AM with personalized titles and descriptions for each reminder

## **Typical Applications**

--&nbsp; **Client Onboarding** → Ensuring new clients receive timely check-ins during their initial journey
--&nbsp; **Service Follow-ups** → Maintaining regular contact with ongoing clients at structured intervals  
--&nbsp; **Relationship Management** → Automating touchpoints to prevent clients from falling through the cracks
--&nbsp; **Sales Pipeline** → Following up with prospects at consistent intervals to nurture relationships

## **Workflow Architecture**

1. **Google Sheets with Client Data** → (Trigger: Get spreadsheet data)  
   The workflow starts by pulling client information including names, start dates, and phone numbers.

2. **Date Processing & Reminder Generation** → (Code: Process dates and create reminder schedule)  
   Converts Google Sheets serial dates and generates up to 9 reminders per client with calculated dates.

3. **Split Individual Reminders** → (Split Out: Separate reminder items)  
   Breaks down the reminder array into individual items for processing.

4. **Create Calendar Events** → (Google Calendar: Create events)  
   Each reminder becomes a 15-minute calendar event at 6 AM with personalized details.

5. **Automated Follow-up System** → Output is a complete calendar schedule ensuring no client is forgotten.

---

## 📊 **Workflow Diagram**
```mermaid
flowchart TD
    A[📊 Google Sheets<br/>Client Data] --> B[⚙️ Code Node<br/>Process Dates & Generate Reminders]
    B --> C[🔀 Split Out Node<br/>Individual Reminder Items]
    C --> D[📅 Google Calendar<br/>Create 6 AM Events]
    
    B --> E{Client has<br/>To start marker?}
    E -->|Yes| F[🔔 Start Date Reminder<br/>Should start today]
    E -->|No| G[⏭️ Skip Start Reminder]
    F --> H[📋 8 Follow-up Reminders<br/>Every 5 days]
    G --> H
    H --> C
    
    style A fill:#4285f4,color:#fff
    style B fill:#ea4335,color:#fff
    style C fill:#fbbc04,color:#000
    style D fill:#34a853,color:#fff
    style F fill:#ff6d01,color:#fff


    
