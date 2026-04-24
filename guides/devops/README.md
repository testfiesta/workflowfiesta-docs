# 🚀 DevOps

CI/CD automation, infrastructure monitoring, deployment workflows, and incident response for DevOps teams.

{% hint style="success" %}
**All of these are built through conversation.** Copy any prompt below, paste it into WorkflowFiesta, and the platform will guide you through the setup.
{% endhint %}

## Automations

### Deployment Monitor

Watches your CI/CD pipeline, notifies the team on deployment start/success/failure, and triggers rollback procedures if health checks fail.

**Start with this prompt:**

> "Create a deployment monitor workflow that triggers on a webhook from our CI/CD system. It should notify the team on Slack when a deployment starts, report success or failure, and if health checks fail after deploy, alert the on-call engineer and open an incident."

**What the platform will ask:**
- Which tools to connect (it will open secure forms for any credentials needed)
- Specific configuration details (which channel, which project, what format)
- Schedule or trigger preferences

**What you'll have when done:**
A working deployment monitor that runs automatically.

### Infrastructure Alert Responder

Receives alerts from your monitoring system, triages severity, drafts a first response, and pages the right on-call engineer.

**Start with this prompt:**

> "Create an agent that handles infrastructure alerts. When it receives an alert, it should triage severity, check if it's a known issue, draft a status update, and page the on-call engineer if it's SEV-1 or SEV-2."

**What the platform will ask:**
- Which tools to connect (it will open secure forms for any credentials needed)
- Specific configuration details (which channel, which project, what format)
- Schedule or trigger preferences

**What you'll have when done:**
A working infrastructure alert responder that runs automatically.

### Weekly Infrastructure Report

Pulls metrics from your monitoring tools and generates a weekly infrastructure health report — uptime, error rates, cost, and capacity.

**Start with this prompt:**

> "Create a workflow that runs every Monday, pulls last week's infrastructure metrics (uptime, p99 latency, error rate, cost), generates a health report, and emails it to the engineering team."

**What the platform will ask:**
- Which tools to connect (it will open secure forms for any credentials needed)
- Specific configuration details (which channel, which project, what format)
- Schedule or trigger preferences

**What you'll have when done:**
A working weekly infrastructure report that runs automatically.
