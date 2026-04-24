# What is WorkflowFiesta?

WorkflowFiesta is an AI workflow automation platform that lets business and operations teams build, run, and manage AI agents — without writing code.

{% hint style="info" %}
If you just want to get something running, start with the [Quickstart](quickstart.md). Come back here when you want to understand how the pieces fit together.
{% endhint %}

## The problem it solves

Most AI tools give you a chat window. You ask a question, you get an answer, you copy it somewhere else and do the next step yourself.

WorkflowFiesta is different. It connects the steps. An agent can read your data, reason about it, take an action, hand off to another agent, and deliver a finished result — all without you in the loop.

The people who get the most out of WorkflowFiesta are the ones who have a repeating process that currently requires a human to sit in the middle of it.

## The three layers

WorkflowFiesta is built in three layers. You don't need to think about all three at once, but understanding them helps you know what to reach for.

### Layer 1 — Agents

An agent is an AI assistant with a specific job. You give it a name, a system prompt that defines its role and behavior, and optionally a set of skills. That's it.

Agents are conversational by default — you can talk to any agent directly in the chat interface. But they're also callable from workflows, from other agents, and from external systems via webhook.

**Example:** A "Support Triage" agent that reads incoming tickets, classifies them by urgency, and drafts a first response.

### Layer 2 — Skills

Skills extend what an agent knows and can do. A skill is a block of instructions — or a script — that gets injected into the agent's context.

Skills are org-wide. Every agent in your organization can use every skill. You don't configure skills per-agent; you attach them at the org level and they're available everywhere.

**Example:** A "Jira" skill that gives any agent the ability to create, update, and query Jira issues via the REST API.

### Layer 3 — Workflows

Workflows are multi-step automation pipelines. They chain together agents, scripts, and HTTP calls into a sequence that runs automatically — on a schedule, on a webhook trigger, or on demand.

A workflow is where you turn a one-off agent conversation into a repeating, reliable process.

**Example:** Every Monday at 7am, pull data from four sources, generate a CMO report, run it through a design review agent, and email it to the leadership team.

## How the pieces connect

```
Trigger (schedule / webhook / manual)
    ↓
Workflow step 1 — Agent reads data
    ↓
Workflow step 2 — Agent generates output
    ↓
Workflow step 3 — Script sends email / posts to Slack / creates Jira ticket
    ↓
Done. No human in the loop.
```

Each step passes its output to the next. Agents can call other agents. Scripts can call external APIs. The whole thing runs in the cloud — or on your own machine if you install the Runner.

## The Runner

The Runner is a lightweight binary you install on your own computer or server. Once connected, agents can read local files, access network drives, run local tools, and interact with systems that aren't exposed to the internet.

It's optional. Most workflows run fine without it. But if your data lives on a local machine or internal network, the Runner is how you bring it in.

## What WorkflowFiesta is not

{% hint style="warning" %}
WorkflowFiesta is not a no-code app builder, a CRM, or a customer-facing chatbot platform. It's an internal automation layer for teams who want AI working across their operations.
{% endhint %}

It's also not locked to one AI model. You can use OpenAI, Anthropic, AWS Bedrock, or any provider you configure. Swap models without rebuilding anything.

## Where to go next

| If you want to… | Go here |
|---|---|
| Build your first agent | [Quickstart](quickstart.md) |
| Understand agents in depth | [Agents](../agents/overview.md) |
| Understand workflows in depth | [Workflows](../workflows/overview.md) |
| Connect your local machine | [Installing the Runner](install-runner.md) |
| See what others are building | [Discord Community](https://discord.gg/XEKxARDkNQ) |
