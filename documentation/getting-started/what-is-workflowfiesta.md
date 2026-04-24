---
icon: microchip-ai
---

# What is WorkflowFiesta?

WorkflowFiesta is a conversational AI automation platform for business teams. You describe what you want automated — a report, a workflow, an AI assistant — and WorkflowFiesta builds it through conversation.

{% hint style="info" %}
WorkflowFiesta is not a no-code app builder. It's a platform where AI agents do real work: reading emails, updating CRMs, analyzing data, writing content, and running multi-step workflows — all triggered by conversation or schedule.
{% endhint %}

## The problem it solves

Most AI tools give you a chat window. You ask a question, you get an answer, and that's it. Nothing is connected. Nothing runs automatically. Every task requires you to be present.

WorkflowFiesta connects the steps. An agent can read your emails, pull data from your CRM, generate a report, and send it to your team — without you doing anything after the initial setup. That setup happens through conversation.

## The three layers

{% tabs %}
{% tab title="Agents" %}
#### Agents — your AI specialists

An agent is an AI with a specific job. You give it a name, a purpose, and instructions. It uses the AI model you choose and behaves according to the system prompt you define.

**Example agents:**

* A **Customer Support Agent** that reads incoming support emails, drafts responses, and flags urgent issues
* A **Marketing Agent** that writes blog posts, social copy, and ad creative on demand
* A **Sales Agent** that researches prospects, drafts outreach emails, and logs activity to your CRM

Agents are created through conversation:

> "Create a support agent that handles refund requests. It should be empathetic, escalate anything over $500, and always CC the billing team."

WorkflowFiesta asks a few clarifying questions, then creates the agent. You can refine it by talking to it.
{% endtab %}

{% tab title="Skills" %}
#### Skills — consistent, reusable behavior

A skill is a reusable building block that extends agent behavior across your organization. Once a skill exists, any agent can use it.

**Two types:**

* **Prompt skills** inject additional instructions into an agent's system prompt — encoding domain expertise, style rules, or institutional knowledge so the agent behaves consistently every time. Examples: Marketing Copy, Code Review, Natural Writing, Jira.

* **Script skills** package a specific script an agent can execute for repeatable tasks — querying an API, processing data, reading files. Examples: Analytics Pull, Keyword Analyzer, Cohort Retention.

Skills are org-wide. You add a skill to an agent by asking:

> "Give my marketing agent the Marketing Copy skill so it always follows our brand voice."

If the skill requires credentials (an API key, OAuth connection, etc.), WorkflowFiesta walks you through connecting it securely — it opens a form, you paste the key, it's encrypted and stored. The key is never exposed in chat.

{% hint style="info" %}
Skills don't unlock capabilities an agent doesn't otherwise have. An agent's ability to take action comes from its platform access level and tools. Skills make behavior consistent and reusable.
{% endhint %}
{% endtab %}

{% tab title="Workflows" %}
#### Workflows — automation that runs itself

A workflow is a sequence of steps that runs automatically. It can be triggered by a schedule, a webhook, an event, or a chat message.

**Example workflows:**

* Every Monday at 7am: pull Intercom data, generate a CMO report, email it to the leadership team
* When a new lead is created in HubSpot: research the company, draft a personalized outreach email, assign it to the right rep
* Every night: scan all open support tickets, summarize unresolved issues, post a digest to Slack

Workflows are built through conversation:

> "Every Friday at 4pm, pull this week's closed deals from HubSpot, calculate total revenue, and email me a summary with a chart."

WorkflowFiesta asks what data you need, what format you want, and who to send it to. Then it builds the workflow, schedules it, and runs it automatically.
{% endtab %}
{% endtabs %}

## How the pieces connect

```
You say what you want
        ↓
WorkflowFiesta asks clarifying questions
        ↓
You answer (and provide credentials if needed)
        ↓
WorkflowFiesta builds the agent / skill / workflow
        ↓
It runs automatically — on schedule, on trigger, or on demand
        ↓
Results delivered to you (email, Slack, chat, dashboard)
```

## The Runner — your local machine

The Runner is a lightweight app you install on your computer or server. Once connected, agents can access your local files, internal databases, network drives, and tools that aren't on the internet.

**You need the Runner if you want to:**

* Read files from your local filesystem or network drive
* Connect to an internal database not exposed to the internet
* Run scripts on your own machine
* Access tools behind a corporate firewall

The Runner is optional. If everything you need is cloud-based (Gmail, HubSpot, Jira, Slack), you don't need it.

## What WorkflowFiesta is not

{% hint style="warning" %}
**Not a no-code app builder.** WorkflowFiesta doesn't build web apps, dashboards, or user-facing interfaces. It automates work that happens behind the scenes.

**Not a single-model AI tool.** WorkflowFiesta supports OpenAI, Anthropic, AWS Bedrock, and more. You choose the model. You can switch at any time.

**Not a replacement for your existing tools.** WorkflowFiesta connects to the tools you already use — it doesn't replace them.
{% endhint %}

## What to read next

| | |
| --- | --- |
| [🚀 Quickstart](quickstart.md) | Get your first agent running in 5 minutes |
| [⚙️ Agents](../workflowfiesta/agents.md) | Deep dive into how agents work |
| [🔁 Workflows](../workflowfiesta/workflows.md) | How to build automated pipelines |
| [🔧 Skills](../workflowfiesta/skills.md) | What skills are and how to use them |
| [👥 Discord](https://discord.gg/XEKxARDkNQ) | Ask the community |
