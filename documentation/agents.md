---
icon: user-hat-tie
---

# Agents

{% hint style="info" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


An agent is an AI specialist you create through conversation. It has a defined purpose, a set of instructions, and access to the tools it needs to do its job.

{% hint style="success" %}
**Agents are created through conversation.** You don't fill out a form or write a config file. You describe what you want, and WorkflowFiesta builds it with you.
{% endhint %}

## What Is an Agent?

Think of an agent as a team member with a specific role. You might have:

* A **Customer Support Agent** that handles incoming support emails with empathy and escalates billing issues
* A **Marketing Agent** that writes ad copy following your brand guidelines
* A **Data Agent** that queries your analytics tools and summarizes findings
* A **Jira Agent** that creates, updates, and triages tickets from conversation

Each agent is configured with:

| Property            | What it does                                                      |
| ------------------- | ----------------------------------------------------------------- |
| **Name**            | How you and your team refer to the agent                          |
| **Description**     | What the agent does — shown in the agent directory                |
| **System Prompt**   | The agent's instructions, personality, constraints, and expertise |
| **Model**           | Which AI model powers the agent (Claude, GPT-4, etc.)             |
| **Temperature**     | How creative vs. precise the agent's responses are (0–2)          |
| **Platform Access** | What tools and actions the agent can take                         |

## Creating an Agent

Start a conversation with WorkflowFiesta and describe what you want:

> "Create an agent for our sales team. It should help reps draft outreach emails, research prospects, and suggest follow-up timing. Keep the tone professional but warm."

WorkflowFiesta will ask clarifying questions:

* Should it follow a specific email framework (AIDA, PAS)?
* Does it need access to your CRM?
* Should it be aware of your product's pricing and positioning?

Answer the questions, and the agent is created. It is available to your team immediately.

{% hint style="info" %}
**The more specific you are, the better the agent.** "Write emails" creates a generic agent. "Write cold outreach emails for a B2B SaaS product targeting QA engineers, using a problem-first approach, under 150 words" creates a specialist.
{% endhint %}

## Updating an Agent

You can update any agent through conversation at any time:

> "Update the Sales Agent — it should now also help reps prepare for discovery calls by generating a list of questions based on the prospect's company."

Or be more direct:

> "Change the Sales Agent's tone to be more direct and less formal."

WorkflowFiesta will show you a preview of the change and ask for confirmation before applying it.

***

## Agent Capabilities

An agent's ability to take action comes from its **platform access level** and **available tools** — not from skills. An agent with the right access level can already:

* Run bash scripts and execute code
* Call external APIs
* Send emails via Gmail or Outlook
* Create and update Jira tickets
* Read files from your local machine (with the Runner installed)
* Search the web
* Trigger and call other agents

**Skills** extend this by providing consistent, reusable instructions or pre-built scripts — but they do not gate what an agent is capable of. See [Skills](skills.md) for how skills work.

### Platform Access Levels

| Level     | What the agent can do                                           |
| --------- | --------------------------------------------------------------- |
| **Read**  | Read platform resources — list agents, workflows, skills        |
| **Write** | Create and update platform resources with user confirmation     |
| **Admin** | Full access — create, update, delete without confirmation gates |
| **None**  | Conversational only — no platform tool access                   |

***

## Agent Patterns

{% tabs %}
{% tab title="Specialist" %}
#### Specialist Agent

A focused agent with deep expertise in one domain. Given a clear, narrow system prompt and the tools it needs for that domain.

**Examples:**

* SEO Auditor — reviews articles against a 100-point SEO checklist
* Jira Agent — manages tickets, sprints, and boards via the Jira API
* Keyword Researcher — pulls search volume data and categorizes keywords by tier

**When to use:** When you have a repeatable task that benefits from consistent, expert-level behavior every time.
{% endtab %}

{% tab title="Orchestrator" %}
#### Orchestrator Agent

A master agent that coordinates other specialist agents. It receives a high-level goal, breaks it into sub-tasks, calls the right specialists, synthesizes their outputs, and delivers a final result.

**Examples:**

* Report Orchestrator — calls Intercom, Jira, GA4, and Google Ads agents, then synthesizes a CMO brief
* Agent Architect — interviews the user, calls Design Auditor + Edge Case Analyst + Enhancement Scout in parallel, then builds the approved design

**When to use:** When a task requires multiple specialists working together, or when the path through a process depends on what is discovered along the way.
{% endtab %}

{% tab title="Director" %}
#### Director Agent

Similar to an orchestrator, but focused on managing a long-running pipeline. A director agent runs a fixed sequence of specialists end-to-end — like a production line.

**Example — Blog Director:**

```
Brief → SERP Analyst → Keyword Auditor → SEO Architect →
Copywriter → Humanizer → Fact Checker → SEO Fixer →
Cover Photo Builder → Article Reviewer → GitHub Push
```

**When to use:** When you have a defined multi-step process that always runs in the same order and produces a finished artifact.
{% endtab %}

{% tab title="General" %}
#### General Agent

A broad-purpose agent that handles a wide range of tasks for a team or department. Less specialized than a specialist, but more capable across domains.

**Examples:**

* Marketing Assistant — handles copy, briefs, research, and scheduling questions
* Operations Agent — answers process questions, creates tickets, drafts SOPs

**When to use:** As a team's day-to-day assistant — a first stop before routing to a specialist.
{% endtab %}
{% endtabs %}

***

## Slash Commands

Every agent can be given a slash command — a shortcut that lets your team switch to it instantly from any conversation.

> "Create a slash command /sales for the Sales Agent."

Now anyone on your team can type `/sales` in chat to immediately switch to the Sales Agent.

See [Custom Commands](custom-commands.md) for more.

***

## Agent Directory

All agents in your organization are listed in the **Agents** section of the platform. From there you can:

* See all agents and their descriptions
* Switch to any agent directly
* View an agent's configuration
* Edit or delete agents

{% hint style="warning" %}
**Agents are org-wide.** Any agent you create is available to everyone in your organization. If you want a private agent, create a separate workspace.
{% endhint %}

***

## Agents vs. Workflows

Agents and workflows are complementary — not competing.

|                       | Agent                                 | Workflow                                    |
| --------------------- | ------------------------------------- | ------------------------------------------- |
| **Best for**          | Conversation, judgment, dynamic tasks | Scheduled, repeatable, multi-step pipelines |
| **Triggered by**      | A message in chat                     | Schedule, webhook, API, or chat command     |
| **Runs**              | Until the conversation ends           | Until all steps complete                    |
| **Can call**          | Other agents, tools, APIs             | Agents, scripts, HTTP endpoints             |
| **Human in the loop** | Always                                | Optional                                    |

Most production systems use both: a workflow handles scheduling and orchestration, and agents handle the reasoning and action within each step.

See [Workflows](workflows.md) for how the two patterns work together.

***

## What to Read Next

| Topic                               | Link                                  |
| ----------------------------------- | ------------------------------------- |
| Add reusable behavior to agents     | [Skills](skills.md)                   |
| Put agents into automated pipelines | [Workflows](workflows.md)             |
| Give agents access to local files   | [Runner](runner.md)                   |
| Connect agents to external services | [Credentials](credentials.md)         |
| Create slash command shortcuts      | [Custom Commands](custom-commands.md) |
