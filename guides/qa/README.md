---
icon: bug
---

# QA & Testing

{% hint style="success" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


Test case generation, bug triage, coverage reports, and regression monitoring for QA teams.

{% hint style="info" %}
**All of these are built through conversation.** Copy any prompt below, paste it into WorkflowFiesta, and the platform will guide you through the setup.
{% endhint %}

## Automations

### Bug Triage Agent

Reads incoming bug reports, categorizes them by severity and component, assigns them to the right team member, and creates structured Jira tickets.

**Start with this prompt:**

> "Create a bug triage agent that reads bug reports, categorizes them by severity (critical/high/medium/low) and component, and creates Jira tickets with structured descriptions and acceptance criteria."

**What the platform will ask:**

* Which tools to connect (it will open secure forms for any credentials needed)
* Specific configuration details (which channel, which project, what format)
* Schedule or trigger preferences

**What you'll have when done:** A working bug triage agent that runs automatically.

### Test Case Generator

Takes a feature description or user story and generates comprehensive test cases covering happy paths, edge cases, and error conditions.

**Start with this prompt:**

> "Create an agent that generates test cases from feature descriptions. It should cover happy paths, edge cases, boundary conditions, and error states. Output in a format compatible with our test management tool."

**What the platform will ask:**

* Which tools to connect (it will open secure forms for any credentials needed)
* Specific configuration details (which channel, which project, what format)
* Schedule or trigger preferences

**What you'll have when done:** A working test case generator that runs automatically.

### Coverage Report

Pulls test run data from Jira, calculates coverage by feature area, and generates a weekly coverage report.

**Start with this prompt:**

> "Create a workflow that runs every Friday, pulls test execution data from Jira, calculates coverage by epic and component, and sends a coverage report to the QA team."

**What the platform will ask:**

* Which tools to connect (it will open secure forms for any credentials needed)
* Specific configuration details (which channel, which project, what format)
* Schedule or trigger preferences

**What you'll have when done:** A working coverage report that runs automatically.
