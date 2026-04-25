---
icon: bolt
---

# Skills

{% hint style="success" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


Skills are reusable building blocks that extend agent behavior across your organization. Once a skill exists, any agent can use it.

{% hint style="info" %}
**Skills are org-wide.** Build a capability once and every agent in your organization can use it — no need to repeat yourself across agents.
{% endhint %}

## What Is a Skill?

An agent's ability to take action — run code, call APIs, send emails, create tickets — comes from its **platform access level and available tools**, not from skills. A fully configured agent can already do a great deal without any skills attached.

Skills serve a different purpose: they make agent behavior **consistent, efficient, and reusable** across your organization.

There are two types:

{% tabs %}
{% tab title="Prompt Skills" %}
#### Prompt Skills

A prompt skill injects additional instructions into an agent's system prompt. It encodes domain expertise, style rules, API patterns, or institutional knowledge — so the agent behaves consistently and correctly every time, without you re-prompting each conversation.

**Examples:**

* **Marketing Copy** — teaches the agent your brand voice, tone rules, and what phrases to avoid
* **Code Review** — encodes a specific review checklist (security, performance, maintainability)
* **Natural Writing** — injects rules to avoid AI-sounding patterns and write like a human
* **Jira** — teaches the agent your project's issue types, field formats, and RACI ownership

The agent could often reason through these domains on its own. A prompt skill locks in the _specific behavior you want every time_ — no drift, no inconsistency.
{% endtab %}

{% tab title="Script Skills" %}
#### Script Skills

A script skill packages a specific script (Python, bash, etc.) that an agent can execute. They're used for repeatable tasks that require real execution — querying an API, processing data, reading local files.

The script lives in the skill so agents don't need to regenerate it each time. It runs in a container or on your local machine via the Runner.

**Examples:**

* **Analytics Pull** — queries Intercom, Google Analytics, and Google Ads and returns a formatted report
* **Keyword Analyzer** — calls the Google Ads Keyword Planner API and categorizes results by tier
* **Cohort Retention** — queries Intercom user data and outputs a retention matrix

{% hint style="info" %}
Script skills require credentials for any external services they connect to. WorkflowFiesta will walk you through connecting them securely when you add the skill.
{% endhint %}
{% endtab %}
{% endtabs %}

## What Skills Are Not

{% hint style="info" %}
**Skills do not unlock capabilities an agent doesn't otherwise have.**

An agent's ability to take action — run code, call APIs, send emails, create Jira tickets — comes from its platform access level and available tools. Skills make behavior consistent, efficient, and org-wide. They don't gate what an agent can do.
{% endhint %}

## Creating a Skill

Start a conversation with WorkflowFiesta:

> "Create a skill that teaches agents how to write in our brand voice. The tone should be direct and confident, avoid corporate jargon, and never use phrases like 'leverage' or 'synergy'."

> "Create a script skill that queries our internal PostgreSQL database and returns a summary of open support tickets."

WorkflowFiesta will ask clarifying questions — what the skill should do, what constraints it should follow, and whether it needs credentials to connect to any external service.

## Adding a Skill to an Agent

> "Add the Marketing Copy skill to the Content Agent."

> "Give the Support Agent the Jira skill so it can create tickets from conversations."

Skills are org-wide — once created, they're available to every agent. Adding a skill to a specific agent simply activates it for that agent's context.

## Browsing Available Skills

All skills in your organization are listed in **Settings → Skills**. From there you can:

* See all prompt and script skills
* View what each skill does
* Add a skill to an agent
* Create a new skill

## Skills vs. Credentials

|                | Skills                                        | Credentials                                    |
| -------------- | --------------------------------------------- | ---------------------------------------------- |
| **What it is** | Reusable instructions or a packaged script    | An encrypted secret (API key, password, token) |
| **Example**    | Jira prompt skill (teaches Jira API patterns) | Jira API token (authenticates the request)     |
| **Stored as**  | Instructions or code                          | Encrypted key-value pairs                      |
| **Scope**      | Org-wide — any agent can use it               | Org-wide — injected at runtime, never exposed  |

A skill defines _how_ to interact with a service. A credential provides the _authentication_ to actually do it. Most script skills that connect to external services require a matching credential.

See [Credentials](credentials.md) for how to store and manage secrets securely.

## Frequently Asked Questions

<details>

<summary>Can I edit a skill after creating it?</summary>

Yes. Ask WorkflowFiesta to update it:

> "Update the Marketing Copy skill — add a rule that all CTAs should be under 8 words."

Changes take effect immediately for all agents using the skill.

</details>

<details>

<summary>Can I delete a skill?</summary>

Yes. WorkflowFiesta will warn you if any agents are currently using it before deletion.

</details>

<details>

<summary>Do skills affect every conversation or just specific agents?</summary>

Prompt skills are injected into the system prompt of agents they're attached to. They affect every conversation that agent has. Script skills are available to any agent that has them attached and can be invoked when needed.

</details>
