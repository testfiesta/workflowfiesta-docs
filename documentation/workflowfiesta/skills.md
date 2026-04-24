---
icon: bolt
---

# Skills

Skills are capabilities you add to agents. They define what an agent can *do* — not just what it knows.

{% hint style="success" %}
**Skills are org-wide.** Once a skill exists in your organization, any agent can use it. You build a capability once and share it everywhere.
{% endhint %}

## What Is a Skill?

Without skills, an agent can reason, write, and answer questions — but it cannot take action in the world. Skills change that.

A skill might let an agent:
- Search the web for current information
- Send an email via Gmail or Outlook
- Create a Jira ticket
- Query Google Analytics
- Run a Python script
- Read a file from your local machine
- Call any external API

## Two Types of Skills

**Prompt Skills** inject additional instructions into an agent's system prompt. They teach the agent a new area of expertise, a set of rules, or a specific way of working. Examples: Marketing Copy, Jira, Code Review, Natural Writing. No external connections needed — they just make the agent smarter at a specific domain.

**Script Skills** let an agent execute real code. When the agent needs to take action — query a database, call an API, process a file — it runs the script. Examples: Analytics Pull (queries Intercom, GA4, Google Ads), Keyword Analyzer (calls Google Ads API), Cohort Retention (queries Intercom user data). Script skills run in a container or on your local machine via the Runner.

## Adding a Skill to an Agent

You add skills through conversation:

> "Add a web search skill to the Research Agent."

> "Give the Marketing Agent the ability to send emails via Gmail."

> "Add the Jira skill to the Project Manager Agent."

If the skill requires credentials, the platform will prompt you to provide them securely before attaching the skill.

## Creating a New Skill

> "Create a skill that teaches agents how to write in our brand voice."

> "Create a skill that lets agents query our internal PostgreSQL database."

For script skills that connect to external tools, the platform will ask for the necessary credentials and walk you through setup.

## Skills vs. Credentials

| | Skills | Credentials |
|---|---|---|
| **What it is** | A capability (what the agent can do) | A secret (how it authenticates) |
| **Example** | Gmail SMTP skill | Gmail username + app password |
| **Stored as** | Instructions or code | Encrypted key-value pairs |

A skill defines *how* to send an email. A credential provides the *authentication* to actually send it. Most integration skills require a matching credential.

See [Credentials](credentials.md) for how to store and manage secrets securely.
