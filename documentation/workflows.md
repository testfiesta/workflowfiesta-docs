---
icon: grid-2
---

# Workflows

{% hint style="success" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


A workflow is an automated pipeline that runs a sequence of agents — or other actions — from start to finish, without you having to be present.

You describe what you want to automate. WorkflowFiesta asks you questions, understands the process, and builds the workflow with you through conversation.

{% hint style="info" %}
**Conversation-first:** You do not need to configure anything manually. Just tell WorkflowFiesta what you want to automate and it will design and build the workflow with you.
{% endhint %}

## What a workflow does

A workflow takes a trigger — a schedule, an event, a message, or a manual run — and executes a series of steps automatically. Each step can involve an agent doing work, a tool being called, or data being passed from one place to another.

The result is a process that runs reliably, on its own, every time — without you having to kick it off or monitor it.

## How to create a workflow

Start a conversation with WorkflowFiesta and describe what you want to automate:

> _"Every Monday morning, pull last week's analytics from Google Analytics and Intercom, summarize the key numbers, and email me a report."_

WorkflowFiesta will:

1. Ask clarifying questions to understand the process
2. Identify which agents and tools are needed
3. Design the workflow and show you what it will do
4. Build it and activate it — ready to run

You review and approve before anything goes live.

## Triggers — what starts a workflow

{% tabs %}
{% tab title="Schedule" %}
Run automatically on a recurring schedule. Examples:

* Every Monday at 7am
* First day of every month
* Every night at midnight

Just describe the schedule in plain language and WorkflowFiesta sets it up.
{% endtab %}

{% tab title="Manual" %}
Run on demand — you trigger it yourself whenever you need it. Useful for processes you want to control but not repeat automatically.
{% endtab %}

{% tab title="Webhook" %}
Run when an external system sends a signal. For example: when a new lead is created in your CRM, when a payment is received, or when a form is submitted.
{% endtab %}

{% tab title="Chat" %}
Run directly from a conversation. You can trigger a workflow by asking for it in chat — WorkflowFiesta will kick it off and report back when it is done.
{% endtab %}
{% endtabs %}

## Two automation patterns

WorkflowFiesta supports two distinct patterns for automation. Understanding the difference helps you choose the right approach.

### Pattern 1 — Sequential workflow

A defined pipeline where agents run in a fixed order. Each agent receives the previous agent's output and passes its own output to the next.

**Best for:**

* Processes with a clear start and end
* Steps that always happen in the same order
* Pipelines you want to schedule or run automatically

**Example — Weekly CMO Report:** Analytics Agent → Jira Agent → Report Builder → Design Auditor → Email

Each agent does its job and hands off to the next. The workflow is the conductor.

### Pattern 2 — Orchestrator agent

A master agent that dynamically decides which specialist agents to call, in what order, based on what it discovers along the way.

**Best for:**

* Processes where the path is not fixed
* Tasks that require judgment or branching
* Workflows where a human needs to review and approve mid-process

**Example — Agent Architect:** The Agent Architect interviews you, then calls the Design Auditor, Edge Case Analyst, and Enhancement Scout in parallel — synthesizes their findings — then presents a revised design for your approval before building anything.

### Choosing the right pattern

| Situation                                         | Use                                       |
| ------------------------------------------------- | ----------------------------------------- |
| Fixed steps, always in the same order             | Sequential workflow                       |
| Runs automatically on a schedule                  | Sequential workflow                       |
| Path depends on conditions or what is discovered  | Orchestrator agent                        |
| Human approval needed mid-process                 | Orchestrator agent                        |
| Complex process with both fixed and dynamic parts | Workflow that calls an orchestrator agent |

{% hint style="info" %}
You can combine both patterns. A scheduled workflow can trigger an orchestrator agent, which then dynamically calls sub-agents based on what it finds.
{% endhint %}

## Managing workflows

All your workflows are listed in the **Workflows** section of the platform. From there you can:

* See which workflows are active or paused
* View the run history for any workflow
* Trigger a workflow manually
* Ask WorkflowFiesta to modify or extend a workflow through conversation

## Examples of workflows teams use

| Team            | Workflow                                                                    |
| --------------- | --------------------------------------------------------------------------- |
| **Marketing**   | Weekly blog pipeline — research to published article, fully automated       |
| **Leadership**  | Monday morning CMO report — analytics, Jira, and campaign data in one email |
| **Sales**       | New lead enrichment — CRM entry triggers research and outreach draft        |
| **Operations**  | Daily standup summary — pulls updates from Jira and posts to Slack          |
| **Development** | PR review digest — summarizes open PRs and flags blockers every morning     |
