# Workflows

A workflow is an automated pipeline that runs a sequence of steps — without you having to be present. You describe what you want to happen, and WorkflowFiesta builds and runs it.

{% hint style="info" %}
**Workflows are conversational.** Tell WorkflowFiesta what you want to automate. It will ask you questions, confirm the details, and build the workflow for you.
{% endhint %}

## What a workflow does

A workflow connects a trigger to a series of actions. When something happens (a schedule fires, a webhook arrives, someone sends a message), the workflow runs — calling agents, processing data, sending emails, updating systems — and delivers a result.

**Example:** Every Monday at 7am, pull data from Intercom and Google Analytics, generate a report, and email it to your team. You set it up once. It runs forever.

## How to create a workflow

Just describe what you want to automate in the chat:

> *"Every Monday morning, pull last week's analytics data, summarize the key metrics, and email me a report."*

WorkflowFiesta will:
1. Ask clarifying questions (which data sources? what time? who receives it?)
2. Confirm the design with you
3. Build and activate the workflow

You can also ask WorkflowFiesta to modify, pause, or delete any workflow at any time.

## Triggers — what starts a workflow

{% tabs %}
{% tab title="Schedule" %}
**Runs automatically on a time-based schedule.**

Examples:
- Every Monday at 7am
- First day of each month
- Every weekday at 9am

Just describe the schedule in plain language — WorkflowFiesta handles the rest.
{% endtab %}

{% tab title="Manual" %}
**You trigger it yourself, on demand.**

Run it from the chat whenever you need it. Useful for reports, one-off processes, or anything you want to control manually.
{% endtab %}

{% tab title="Webhook" %}
**Triggered by an external system sending a signal.**

When another tool (like GitHub, Stripe, or your CRM) fires an event, your workflow starts automatically. WorkflowFiesta gives you a webhook URL to paste into the external service.
{% endtab %}

{% tab title="Chat" %}
**Triggered by a message in a conversation.**

A workflow can be kicked off directly from a chat with an agent — useful for interactive pipelines where a human starts the process and automation takes over.
{% endtab %}
{% endtabs %}

## Two automation patterns

WorkflowFiesta supports two distinct patterns for automation. Understanding the difference helps you choose the right approach.

### Pattern 1 — Sequential workflow

A defined sequence of steps that always run in the same order. Each step receives the output of the previous one.

**Best for:**
- Processes with a clear start and end
- Steps that always happen in the same order
- Anything you want to schedule and run automatically

**Example — Weekly CMO Report:**
Pull Intercom data → Pull Google Analytics → Pull Jira data → Generate report → Design audit → Email to team

Each step feeds the next. The workflow is the conductor.

### Pattern 2 — Orchestrator agent

A master agent that decides at runtime which specialist agents to call and in what order — based on what it discovers along the way.

**Best for:**
- Processes where the path isn't fixed
- Tasks that require judgment or branching
- Workflows where a human needs to approve something mid-process

**Example — Agent Architect:**
The Agent Architect interviews you, then dynamically calls a Design Auditor, Edge Case Analyst, and Enhancement Scout in parallel — synthesizing all three before presenting a recommendation. The path depends on what you ask for.

### Combining both

You can also combine the patterns: a scheduled workflow triggers an orchestrator agent, which then dynamically calls sub-agents based on what it finds.

{% hint style="success" %}
**Rule of thumb:** If you can draw a flowchart of the steps upfront, use a sequential workflow. If the process needs to think and adapt, use an orchestrator agent.
{% endhint %}

## What workflows can do

Workflows can call any agent, connect to any external service you have credentials for, send emails, post to Slack, create Jira tickets, read and write files, and much more. The scope of what a workflow can do is determined by the agents and credentials you have set up.

## Managing workflows

You can view, edit, pause, and delete all your workflows from the **Workflows** tab in the platform. You can also ask WorkflowFiesta to make changes conversationally at any time.

{% content-ref url="agents.md" %}
[Learn about Agents](agents.md)
{% endcontent-ref %}

{% content-ref url="credentials.md" %}
[Connect external services](credentials.md)
{% endcontent-ref %}
