# Automated Customer Onboarding Checklist Generator

A Python tool that reads a customer configuration file and generates a tailored HTML onboarding checklist. Sections and tasks are included or excluded automatically based on the customer's subscription plan and enabled integrations.

---

## The Problem It Solves

Onboarding a new enterprise customer used to mean opening a master checklist document, copying it, and manually editing it to remove irrelevant sections. For a Starter plan customer with no integrations, that's 20 minutes of busywork. For an Enterprise customer with Salesforce, Slack, and SSO, it's easy to miss something. This tool generates the right checklist for each customer in seconds.

---

## How It Works

1. You create a simple JSON config for the customer (name, plan, integrations, go-live date)
2. The script reads the config and builds a checklist with the right sections
3. A Jinja2 template renders it as a clean, printable HTML file

Sections included depend on:
- **Plan tier** — Starter, Professional, or Enterprise gates certain sections (API config, SSO, SLA review)
- **Integrations** — Zapier, Salesforce/CRM, and Slack each add their own integration-specific section
- **Go-live** — always appended with a validation and sign-off section

---

## Tech Stack

- **Python 3.8+**
- **Jinja2** — HTML templating
- **json** — config parsing

---

## Installation

```bash
git clone https://github.com/YOUR_USERNAME/onboarding-checklist.git
cd onboarding-checklist
pip install -r requirements.txt
```

---

## Usage

**Create a customer config:**
```json
{
  "name": "Faulu Microfinance Bank",
  "plan": "enterprise",
  "account_owner": "Collins Ngumba",
  "go_live_date": "2024-04-01",
  "integrations": ["salesforce", "slack", "zapier"]
}
```

**Generate the checklist:**
```bash
python generate.py faulu_microfinance.json
```

**Run with sample data:**
```bash
python generate.py
```

Output: `checklist_faulu_microfinance.html` — open in any browser.

---

## Plan vs Sections Matrix

| Section | Starter | Professional | Enterprise |
|---------|---------|--------------|------------|
| Account Setup | ✓ | ✓ | ✓ |
| API Configuration | — | ✓ | ✓ |
| Enterprise Config (SSO, SLA) | — | — | ✓ |
| Integration sections | Based on config | Based on config | Based on config |
| Go-Live Validation | ✓ | ✓ | ✓ |
