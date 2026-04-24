---
icon: user-hat-tie
---

# Agents

An agent is an AI specialist you create through conversation. It has a defined purpose, a personality, a set of capabilities, and access to the tools it needs to do its job.

{% hint style="success" %}
**Agents are created through conversation.** You don't fill out a form or write a config file. You describe what you want, and WorkflowFiesta builds it with you.
{% endhint %}

## What Is an Agent?

Think of an agent as a team member with a specific role. You might have:

- A **Customer Support Agent** that handles incoming support emails with empathy and escalates billing issues
- A **Marketing Agent** that writes ad copy following your brand guidelines
- A **Data Agent** that queries your analytics tools and summarizes findings
- A **Jira Agent** that creates, updates, and triages tickets from conversation

Each agent is configured with:

| Property | What it does |
|---|---|
| **Name** | How you and your team refer to the agent |
| **Description** | What the agent does — shown in the agent directory |
| **System Prompt** | The agent's instructions, personality, constraints, and expertise |
| **Model** | Which AI model powers the agent (Claude, GPT-4, etc.) |
| **Temperature** | How creative vs. precise the agent's responses are (0–2) |
| **Platform Access** | What tools and actions the agent can take |

## Creating an Agent

Start a conversation with WorkflowFiesta and describe what you want:

> "Create an agent for our sales team. It should help reps draft outreach emails, research prospects, and suggest follow-up timing. Keep the tone professional but warm."

WorkflowFiesta will ask clarifying questions:
- Should it follow a specific email framework (AIDA, PAS)?
- Does it need access to your CRM?
- Should it be aware of your product's pricing and positioning?

Answer the questions, and the agent is created. It's available to your team immediately.

{% hint style="info" %}
**The more specific you are, the better the agent.** "Write emails" creates a generic agent. "Write cold outreach emails for a B2B SaaS product targeting QA engineers, using a problem-first approach, under 150 words" creates a specialist.
{% endhint %}

## Updating an Agent

You can update any agent through conversation at any time:

> "Update the Sales Agent — it should now also help reps prepare for discovery calls by generating a list of questions based on the prospect's company."

Or be more direct:

> "Change the Sales Agent's tone to be more direct and less formal."

WorkflowFiesta will show you a preview of the change and ask for confirmation before applying it.

## Agent Skills

Skills extend agent behavior — making it consistent, efficient, and reusable across your organization. There are two types:

**Prompt skills** inject additional instructions into the agent's system prompt. They encode domain expertise, style rules, or institutional knowledge so the agent behaves correctly every time without re-prompting.

**Script skills** package a specific script the agent can execute — for repeatable tasks like querying an API, processing data, or reading files.

{% hint style="info" %}
Skills don't unlock capabilities an agent doesn't otherwise have. An agent's ability to take action — run code, call APIs, send emails, create tickets — comes from its platform access level and available tools. Skills make behavior consistent and reusable.
{% endhint %}

To add a skill to an agent:

> "Add the Marketing Copy skill to the Content Agent so it always follows our brand voice."

> "Give the Support Agent the Jira skill so it can create tickets from conversations."

See [Skills](skills.md) for the full reference.

## Slash Commands

Every agent can be given a slash command — a shortcut that lets your team switch to it instantly from any conversation.

> "Create a slash command /sales for the Sales Agent."

Now anyone on your team can type `/sales` in chat to immediately switch to the Sales Agent.

See [Custom Commands](custom-commands.md) for more.

## Agent Directory

All agents in your organization are listed in the **Agents** section of the platform. From there you can:

- See all agents and their descriptions
- Switch to any agent directly
- View an agent's configuration
- Edit or delete agents

{% hint style="warning" %}
**Agents are org-wide.** Any agent you create is available to everyone in your organization. If you want a private agent, create a separate workspace.
{% endhint %}

## Specialist vs. General Agents

{% tabs %}
{% tab title="Specialist agents" %}
A specialist agent has a narrow, well-defined job. It's better at that job than a general agent because its system prompt is focused and its instructions are targeted.

**Examples:**
- SEO Copywriter — writes blog posts following SEO best practices
- Incident Responder — manages production incidents with a structured runbook
- Contract Reviewer — extracts key terms and flags risks in legal documents

**When to use:** When a task is repeated often and quality matters.
{% endtab %}
{% tab title="General agents" %}
A general agent can handle a wide range of tasks. It's useful for exploration, ad-hoc work, and situations where you don't know exactly what you need yet.

**Examples:**
- Chat Assistant — answers questions, helps with writing, does research
- Dynamic Agent — activates only the skills relevant to each request

**When to use:** For day-to-day work, one-off tasks, and getting started.
{% endtab %}
{% endtabs %}

## Frequently Asked Questions

<details>
<summary>How many agents can I create?</summary>
There's no hard limit on the number of agents. Create as many specialists as your team needs.
</details>

<details>
<summary>Can agents talk to each other?</summary>
Yes. Workflows can chain agents together — one agent's output becomes another agent's input. This is how multi-step pipelines work. See [Workflows](workflows.md).
</details>

<details>
<summary>Can I use different AI models for different agents?</summary>
Yes. Each agent can be configured with a different model. See [Models & Providers](models.md).
</details>

<details>
<summary>What happens if I delete an agent?</summary>
The agent is removed from the directory and can no longer be used. Any workflows that reference it will fail. WorkflowFiesta will warn you before deletion.
</details>
