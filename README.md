# Estimate Follow-up & Booking Automation

An AI-powered estimate follow-up system built with n8n, Google Sheets, and Gmail for US residential cleaning companies. It captures new estimates from a frontend form, sends automated follow-up emails on a daily schedule, stops all reminders the moment a customer books or opts out, and tracks every estimate in real time — fully automated, zero manual intervention.

---

## 🚀 Demo

📽️ [Watch Demo Video](https://drive.google.com/file/d/1YPjvAEDfrVEd3TqOML5AErGjY39rlgaf/view?usp=drive_link)
🌐 [Live Website](https://sparkle-to-scheduled.lovable.app/)

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| n8n | Workflow automation engine |
| Google Sheets | CRM — estimate tracking & status updates |
| Gmail | Automated follow-up email delivery |
| JavaScript | Logic, date calculations, ID generation |
| Webhook | Receives data from frontend website |
| Lovable | Frontend form for estimate entry & booking |

---

## 📋 Project Overview

Residential cleaning companies lose booked jobs every week because nobody follows up on pending estimates. Staff get busy, forget, or accidentally email customers who already booked.

This system solves all of that:

❌ Estimates sent but never followed up on
❌ No way to track which customers are still pending
❌ Staff manually checking and sending reminders
❌ Follow-up emails sent to customers who already booked
❌ No record of estimate status or communication history

✅ Every estimate automatically saved and tracked in Google Sheets
✅ Follow-up emails sent on schedule every morning at 9 AM
✅ System checks status before every email — never double-sends
✅ All future emails stop the moment a customer books or opts out
✅ Full audit trail of every estimate, email sent and status change

---

## ⚡ How It Works

Owner submits estimate via CleanFlow website ↓ Webhook triggers n8n ↓ Estimate ID generated + data saved to Google Sheets ↓ Daily 9 AM schedule fires ↓ Filter: Is estimate Pending + Follow-up date due + Not opted out? Yes ——→ Is Follow-up Count less than 3? Yes ——→ Send follow-up email via Gmail → Update count and next follow-up date in Sheets ↓ No ——→ Mark as Follow-up Complete ↓ Customer books ——→ Owner updates status on CleanFlow website → Webhook fires → Status updated to Booked → All future emails cancelled automatically

---

## 🖥️ Workflow Screenshot

<img width="1919" height="804" alt="image" src="https://github.com/user-attachments/assets/b1cce06f-0d2e-4b68-b90d-f8f46a53c003" />
<img width="1919" height="808" alt="image" src="https://github.com/user-attachments/assets/20b394c7-2b4a-4026-9e4b-885c8aaebb0d" />
<img width="1919" height="808" alt="image" src="https://github.com/user-attachments/assets/4dd83615-11f0-47d2-b8e4-bf3d75309010" />

---

## 🔧 Workflow Nodes

### 2.1 New Estimate Entry (3 Nodes)

| Node | Name | Description |
|------|------|-------------|
| 1 | Receive Estimate from Website | Webhook receives form data from CleanFlow |
| 2 | Generate Estimate ID & Dates | Creates unique EST-ID, sets follow-up schedule |
| 3 | Save Estimate to Google Sheets | Appends new row with all estimate details |

---

### 2.2 Daily Follow-up Checker (8 Nodes)

| Node | Name | Description |
|------|------|-------------|
| 1 | Run Every Day at 9 AM | Schedule trigger — fires daily at 9 AM |
| 2 | Get All Estimates | Reads all rows from Google Sheets Estimates tab |
| 3 | Filter Pending & Due Estimates | Keeps only Pending rows where follow-up date has arrived |
| 4 | Is Follow-up Count Less Than 3? | Routes True (send email) or False (mark complete) |
| 5 | Send Follow-up Email via Gmail | Sends personalized reminder to customer |
| 6 | Calculate Next Follow-up Date | Computes next send date based on attempt number |
| 7 | Update Follow-up Count & Dates | Updates Google Sheets with new count and dates |
| 8 | Mark as Follow-up Complete | Sets Status to Follow-up Complete after 3 attempts |

---

### 2.3 Mark as Booked (2 Nodes)

| Node | Name | Description |
|------|------|-------------|
| 1 | Receive Booking Update from Website | Webhook receives Estimate ID and new status |
| 2 | Update Status in Google Sheets | Updates Status to Booked or Opted Out instantly |

---

## 📊 Google Sheets Structure

**Estimates Tab**

- Estimate ID
- Customer Name
- Email
- Service Type
- Bedrooms
- Bathrooms
- ZIP Code
- Estimate Amount
- Estimate Date
- Status
- Follow-up Count
- Last Follow-up Date
- Next Follow-up Date
- Opt-Out
- Notes

---

## 💡 What I Learned

- Building a multi-workflow automation system where each workflow handles one clear responsibility
- Using JavaScript inside n8n to generate unique IDs, calculate date gaps and handle data formatting
- Referencing data from earlier nodes in a chain using `$('Node Name').item.json` syntax
- Implementing idempotency logic to prevent duplicate emails and duplicate records
- Connecting a Lovable frontend form directly to n8n webhooks using production URLs
- Structuring Google Sheets as a live CRM with real-time status tracking
- Designing follow-up logic that respects opt-outs and stops automatically after a set number of attempts
- Testing automation workflows step by step using manual triggers and test data

---

## 🔗 Links

- 📽️ [Demo Video](https://drive.google.com/file/d/1YPjvAEDfrVEd3TqOML5AErGjY39rlgaf/view?usp=drive_link)
- 📁 [Workflow JSON](https://drive.google.com/drive/folders/1nyOoK6LBJ-VPLHIfden0skJOGRZ883ng?usp=drive_link)
- 🌐 [Live Website](https://sparkle-to-scheduled.lovable.app/)

---

## 👤 About Me

**Omi Mojumdar — AI Automation & Agent Developer**

- 🔗 [LinkedIn](https://www.linkedin.com/in/omimojumdar)
- 📧 omimojumdar83@gmail.com
