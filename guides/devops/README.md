---
description: Automate deployment reports, incident runbooks, monitoring alerts, and infrastructure documentation so your engineers focus on building.
---

# ⚙️ DevOps

Automate deployment reports, incident runbooks, monitoring alerts, and infrastructure documentation so your engineers focus on building.

---

## What DevOps teams automate

### Deployment summaries
Generate clear deployment reports from commit logs, PR descriptions, and release notes.

> *"Summarize what went out in today's deployment. Pull from the last 10 merged PRs and write a plain-language summary for the team."*

### Incident runbooks
Create and maintain incident response runbooks that stay current with your infrastructure.

> *"Create an incident runbook for a database outage. Include detection steps, escalation path, rollback procedure, and post-mortem template."*

### Monitoring alerts
Set up intelligent alerting workflows that summarize what's wrong and suggest next steps.

> *"Create a workflow that receives PagerDuty alerts, summarizes the incident in plain language, and posts it to our #incidents Slack channel with suggested first steps."*

### Infrastructure documentation
Keep your infra docs current by generating them from your actual configuration.

> *"Document our Kubernetes cluster setup. Pull from our config files and write a clear architecture overview for new engineers."*

### Post-mortem drafts
Generate structured post-mortems from incident timelines and Slack threads.

> *"Draft a post-mortem for last night's outage. Here's the incident timeline and the Slack thread. Write it in our standard format."*

---

## Getting started

{% stepper %}
{% step %}
### Tell WorkflowFiesta what you want to automate
Start with your most time-consuming recurring task. Describe it in plain language.
{% endstep %}

{% step %}
### Answer a few questions
WorkflowFiesta will ask about frequency, inputs, outputs, and who should receive the results.
{% endstep %}

{% step %}
### Review and activate
WorkflowFiesta shows you exactly what it's going to build. Approve it and it starts running.
{% endstep %}
{% endstepper %}

---

## Popular devops automations

| Automation | What it does |
|------------|-------------|
| **Deployment report** | Merged PRs → plain-language release summary |
| **Incident runbook generator** | Incident type → structured response runbook |
| **Alert summarizer** | PagerDuty/monitoring alert → plain-language summary + Slack post |
| **Infra doc generator** | Config files → architecture documentation |
| **Post-mortem drafter** | Incident timeline → structured post-mortem |
| **On-call handoff** | Shift end → status summary for incoming on-call engineer |

---

{% hint style="info" %}
**DevOps tip:** Install the WorkflowFiesta Runner on your infrastructure machines so agents can read config files, run scripts, and access internal systems directly.
{% endhint %}

---

{% content-ref url="../README.md" %}
[Back to Guides](../README.md)
{% endcontent-ref %}
