---
icon: display-code
---

# Development

{% hint style="info" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


Code review agents, PR summarizers, incident responders, and deployment monitors for engineering teams.

{% hint style="success" %}
**All of these are built through conversation.** Copy any prompt below, paste it into WorkflowFiesta, and the platform will guide you through the setup.
{% endhint %}

## Automations

### Code Review Agent

Reviews pull requests for correctness, security vulnerabilities, performance issues, and code style. Posts structured feedback as PR comments.

**Start with this prompt:**

> "Create a code review agent that reviews pull requests. It should check for correctness, security vulnerabilities (OWASP Top 10), performance issues, and maintainability. Post feedback as PR comments with severity levels: critical, warning, suggestion."

**What the platform will ask:**

* Which tools to connect (it will open secure forms for any credentials needed)
* Specific configuration details (which channel, which project, what format)
* Schedule or trigger preferences

**What you'll have when done:** A working code review agent that runs automatically.

### Incident Responder

Manages production incidents with a structured runbook. Declares severity, assigns roles, drafts customer communications, and tracks the timeline.

**Start with this prompt:**

> "Create an incident response agent that follows a structured runbook. It should help declare incident severity, assign IC/comms/tech roles, draft customer status updates, track the timeline, and write the post-mortem."

**What the platform will ask:**

* Which tools to connect (it will open secure forms for any credentials needed)
* Specific configuration details (which channel, which project, what format)
* Schedule or trigger preferences

**What you'll have when done:** A working incident responder that runs automatically.

### PR Summarizer

Reads a pull request and writes a clear summary of what changed, why, and how to test it — ready to paste into the PR description.

**Start with this prompt:**

> "Create an agent that summarizes pull requests. Given a diff or PR link, it should write a clear description of what changed, why it was changed, and how to test it."

**What the platform will ask:**

* Which tools to connect (it will open secure forms for any credentials needed)
* Specific configuration details (which channel, which project, what format)
* Schedule or trigger preferences

**What you'll have when done:** A working pr summarizer that runs automatically.
