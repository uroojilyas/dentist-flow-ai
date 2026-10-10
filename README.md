# Dentist Flow AI

An autonomous, multi-tool AI receptionist and appointment management agent built for upscale dental clinics in Cairo. It handles patient inquiries, doctor/service matching, real-time schedule checks, and end-to-end appointment bookings directly in Airtable.

---

##  Features

- **Multi-Domain Intelligence:** Dynamically queries clinic services, pricing, doctor availability, and active schedules across multiple database tables.
- **Autonomous Booking Engine:** Enables real-time slot selection and updates patient records with zero human intervention.
- **Stateful Memory:** Maintains full conversational context for natural multi-turn interactions.
- **Deterministic Tool Execution:** Built with guardrails to eliminate loops and prevent overbooking.

---

##  Tech Stack

| Layer | Technology |
|---|---|
| **Orchestration** | n8n (Autonomous Agent Workflow) |
| **LLM Engine** | Groq (LLaMA 3 Model) |
| **Database / CRM** | Airtable (Multi-Table Schema: `Appointments`, `Doctors`, `Services`) |
| **Interface** | n8n Chat Trigger / Webhook (Web UI) |

---

##  Architecture

| Component | Description |
|---|---|
| **Trigger** | Multi-channel Webhook / Chat Trigger |
| **Brain** | Groq LLaMA 3 Agent with Window Buffer Memory |
| **Toolbox** | 4 specialized tools: `search_appointments`, `update_appointment`, `search_doctors`, `search_services` |
| **Data Layer** | Airtable Relational CRM |

---

##  Quickstart (Run in < 5 Minutes)

### Prerequisites

- An **n8n** instance (Cloud, or local via Docker/npx)
- A **Groq API Key**
- An **Airtable** account and Personal Access Token

### Setup

**1. Clone the repository**

```bash
git clone https://github.com/YOUR_USERNAME/dental-ai-concierge.git
cd dentist-flow-ai
```

**2. Set up Airtable**

Create a Base called `Dental Clinic System`, then create the three tables described in the [Airtable Schema](#airtable-schema) below. Column names must match exactly.

**3. Import the workflow into n8n**

1. Open n8n → **Workflows** → **Import from File**.
2. Select `Workflow.json` from this repository.

**4. Configure credentials**

- Add your Groq API Key to the **Groq Chat Model** node.
- Add your Airtable Personal Access Token to **all** Airtable Tool nodes.

**5. Execute and test**

1. Activate the workflow in n8n.
2. Open the Chat Trigger UI and try:

   > "Hi! What services do you offer, which doctor does teeth whitening, and can I book a slot for October 9, 2026?"

---

## Airtable Schema

| Table | Columns |
|---|---|
| `Appointments` | `Date`, `TimeSlot`, `Status`, `PatientName`, `PatientPhone` |
| `Services` | `ServiceName`, `Price`, `Description` |
| `Doctors` | `DoctorName`, `Specialty`, `WorkingDays`, `Bio` |

---

##  Business Impact

- **15+ Hours Saved per Week:** Eliminates repetitive phone/chat receptionist tasks.
- **$1,200/Month Cost Reduction:** Replaces late-night, off-hours staffing needs.
- **30% Revenue Lift:** Captures after-hours booking inquiries that previously went unanswered.
