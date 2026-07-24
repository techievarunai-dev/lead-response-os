# Lead Response OS

AI-powered lead intake and CRM intelligence system that qualifies inbound leads, researches the prospect's company, enriches the CRM with AI-generated business insights, alerts the sales team in real time, and logs every lead to a centralized revenue ops database — with no manual intervention.

**[Watch the 3-min walkthrough →](LOOM_LINK_HERE)**

---

## The Problem

Manual lead qualification is slow and inconsistent. A form submission sits in an inbox or a raw CRM record until someone manually researches the company, judges fit, and decides what to do next — by which point a hot lead has often gone cold.

## What This System Does

Turns a basic contact form submission into a fully qualified, enriched, CRM-ready lead — automatically, in seconds.

## Architecture

```
Lead Intake (Jotform)
        │
        ▼
  Normalize Lead Data
        │
        ▼
┌───────────────────────────────┐
│      AI Lead Intelligence      │
│                                 │
│  Lead Qualification Agent  ──┐  │
│  Company Intelligence Agent ─┤  │
└───────────────────────────────┘
        │
        ▼
   Merge AI Insights
        │
        ▼
   Build CRM Payload
        │
        ▼
┌─────────────────────┐
│   CRM Enrichment      │
│  Create/Update         │
│  HubSpot Contact       │
└─────────────────────┘
        │
        ├──────────────┐
        ▼              ▼
  Notify Sales      Save Lead to
  Team (Slack)      Revenue Ops
                     (Airtable)
```

## Workflow Breakdown

**1. Lead Intake**
Captures inbound leads from a website form (Jotform) and normalizes the raw submission into a consistent structure.

**2. Lead Qualification Agent**
AI evaluates the lead and outputs:
- Lead score
- Qualification: Hot / Warm / Cold
- Intent
- Urgency
- Recommended pipeline
- Lead summary
- Next best action

**3. Company Intelligence Agent**
Pulls live website content via Jina Reader, then generates:
- Company profile, industry, business model, stage
- Products & services, technologies in use
- Pain points and automation opportunities
- Suggested sales angle and GTM strategy
- Confidence score on the analysis

**4. Merge AI Insights → Build CRM Payload**
Combines the qualification output and company intelligence into a single structured payload, formatted for CRM properties.

**5. CRM Enrichment (HubSpot)**
Creates or updates the HubSpot contact, writing the AI-generated insights into custom CRM fields.

**6. Internal Notifications**
- **Slack** — instant alert to the sales team with lead details, qualification, and AI recommendations
- **Airtable** — every lead logged to a centralized revenue ops table for reporting, tracking, and analytics

## Tech Stack

| Component | Tool |
|---|---|
| Orchestration | n8n |
| AI / LLM | OpenAI GPT |
| Web content extraction | Jina AI Reader |
| CRM | HubSpot API |
| Team alerts | Slack API |
| Revenue ops database | Airtable API |
| Data transformation | JavaScript |

## Sample Input → Output

**Input (Jotform submission):**
```json
{
  "name": "Jordan Lee",
  "email": "jordan@acme-saas.com",
  "company_url": "https://acme-saas.com",
  "message": "Looking for a way to automate our lead routing, we're growing fast and it's becoming a bottleneck."
}
```

**Output (written to HubSpot + Airtable):**
```json
{
  "lead_score": 87,
  "qualification": "Hot",
  "intent": "Automation / operational efficiency",
  "urgency": "High",
  "recommended_pipeline": "Mid-Market SaaS",
  "company_profile": {
    "industry": "B2B SaaS",
    "company_stage": "Growth",
    "pain_points": ["Manual lead routing", "Scaling ops without adding headcount"],
    "automation_opportunity": "High",
    "sales_angle": "Position around time-to-value and reduced manual ops load",
    "confidence_score": 0.91
  },
  "next_best_action": "Reach out within 1 hour with a personalized demo offer referencing their lead-routing pain point"
}
```

## How to Use

1. Import `workflow-export.json` into your n8n instance
2. Connect credentials for: Jotform (or your form provider), OpenAI, Jina AI, HubSpot, Slack, Airtable
3. Configure the webhook trigger to point at your form's submission endpoint
4. Activate the workflow

> Note: This is a demonstration project built with placeholder/test data. Credentials and endpoint URLs in the exported JSON have been scrubbed — you'll need to connect your own.

## Business Value

Instead of a form submission sitting untouched until someone manually reviews it, Lead Response OS qualifies, researches, and routes every lead within seconds of submission — giving sales teams a prioritized, pre-enriched pipeline instead of a raw contact list, and a centralized Airtable log for reporting on lead quality and source performance over time.

---

Built by [Varun Murugan P](https://automatewithvarun.vercel.app) — GTM Engineer
