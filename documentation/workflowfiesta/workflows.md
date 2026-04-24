---
icon: grid-2
---

# Workflows

A workflow is a multi-step automation that runs on a schedule, responds to an event, or is triggered from chat. Workflows connect agents, scripts, and external services into a single automated pipeline.

{% hint style="success" %}
**Workflows are built through conversation.** Describe what you want to automate, answer a few questions, and WorkflowFiesta builds and schedules it for you.
{% endhint %}

## What Is a Workflow?

A workflow is a sequence of steps that runs automatically. Each step can:

- **Invoke an agent** — pass it a prompt and use its output
- **Run a script** — execute Python, bash, or any code in a container
- **Make an HTTP call** — send data to or receive data from any external service

Steps pass data to each other. The output of step 1 becomes the input to step 2. The output of step 2 feeds step 3. And so on.

## Creating a Workflow

Start a conversation:

> "Create a workflow that runs every Monday at 9am, pulls last week's data from Google Analytics, writes a summary using the Analytics Agent, and emails it to our marketing team."

WorkflowFiesta will ask:
- Which Google Analytics property?
- What email addresses should receive the report?
- What format should the summary be in?
- Any specific metrics to highlight?

Answer the questions, and the workflow is built and scheduled. It runs automatically without any further action from you.

---

## Two Automation Patterns

WorkflowFiesta supports two distinct patterns for building automation. Understanding the difference helps you pick the right one.

{% tabs %}
{% tab title="Sequential Workflow" %}
### Pattern 1 — Multi-Agent Workflow

A YAML workflow where each step calls a different specialist agent in order (or in parallel). The workflow is the conductor — it decides what runs, when, and in what order.

**Best for:**
- A defined process with a clear start and end
- Steps that depend on each other's output
- Repeatable pipelines you want to schedule or trigger automatically

**Example — Blog Pipeline:**

```
SERP Analyst → Keyword Auditor → SEO Architect → Copywriter →
Humanizer → Fact Checker → SEO Auditor → SEO Fixer →
Cover Photo Builder → Article Reviewer → GitHub Push
```

Each agent receives the previous agent's output. The workflow is fixed and predictable.

**When to use:** Anytime the process is predictable and the steps are known upfront.
{% endtab %}

{% tab title="Orchestrator Agent" %}
### Pattern 2 — Orchestrator Agent + Sub-Agents

A master agent that dynamically invokes specialist sub-agents based on what's needed — deciding at runtime which agents to call and in what order.

**Best for:**
- Processes where the path is not fixed (decisions need to be made mid-run)
- Interactive workflows where a human is in the loop
- Complex tasks where the orchestrator needs to reason about what to do next

**Example — Agent Architect Pipeline:**

```
Agent Architect (master)
  ├── calls Design Auditor
  ├── calls Edge Case Analyst
  └── calls Enhancement Scout
         ↓
  synthesizes all three → presents to user → builds on approval
```

The master agent decides what to call, synthesizes the results, and adapts based on what it finds.

**When to use:** When the process requires judgment, branching, or dynamic routing.
{% endtab %}

{% tab title="Combined" %}
### Pattern 3 — Workflow + Orchestrator

You can combine both patterns. A scheduled workflow triggers an orchestrator agent, which then dynamically calls sub-agents based on what it discovers.

**Example — Weekly CMO Report:**

```
Scheduled Trigger (Monday 7am)
  → Report Orchestrator Agent
      ├── calls Intercom Analytics Agent
      ├── calls Jira Analytics Agent
      ├── calls Google Ads Agent
      └── calls GA4 Agent
           ↓
      synthesizes → generates HTML report → emails to team
```

The workflow handles scheduling and delivery. The orchestrator handles the reasoning and routing inside.

**When to use:** Scheduled pipelines that need intelligent, adaptive behavior inside them.
{% endtab %}
{% endtabs %}

### Which Pattern Should You Use?

| Situation | Use |
|---|---|
| Fixed steps, always in the same order | Sequential Workflow |
| Scheduled / runs automatically | Sequential Workflow |
| Steps depend on previous output | Sequential Workflow |
| Path depends on conditions or user input | Orchestrator Agent |
| Human approval needed mid-process | Orchestrator Agent |
| Scheduled pipeline with adaptive behavior inside | Workflow + Orchestrator |

{% hint style="info" %}
**Start with a workflow** if you can draw a flowchart of the steps upfront. **Use an orchestrator agent** when the process needs to think and adapt. Both patterns are first-class in WorkflowFiesta.
{% endhint %}

---

## Trigger Types

{% tabs %}
{% tab title="Schedule" %}
### Scheduled Triggers

Run a workflow at a fixed time or interval.

**Examples:**
- Every Monday at 7am
- Every day at 9am
- Every hour
- First day of the month at 8am

Just describe the schedule in plain language when creating the workflow.
{% endtab %}

{% tab title="Webhook" %}
### Webhook Triggers

Run a workflow when an external system sends an HTTP request to the workflow's unique URL.

**Examples:**
- A new Stripe payment is made
- A form is submitted on your website
- A GitHub push event fires
- A Zapier zap triggers it

WorkflowFiesta generates a unique webhook URL for each workflow. Share it with the external system and the workflow fires automatically.
{% endtab %}

{% tab title="Chat" %}
### Chat Triggers

Run a workflow directly from a conversation using a slash command.

> "/report" — triggers the weekly report workflow immediately
> "/triage" — triggers the support triage workflow

See [Custom Commands](custom-commands.md) to set up slash commands for your workflows.
{% endtab %}

{% tab title="API" %}
### API Triggers

Trigger a workflow programmatically from any system using the WorkflowFiesta API.

Useful for:
- Triggering workflows from your own application code
- Chaining WorkflowFiesta into a larger automation pipeline
- CI/CD integrations
{% endtab %}
{% endtabs %}

---

## Workflow Steps

### Agent Steps

An agent step invokes one of your agents with a prompt. The agent's response becomes the step's output.

```yaml
- id: summarize
  type: agent
  agent: Analytics Agent
  prompt: "Summarize this week's data: {{ steps.pull_data.output }}"
```

### Script Steps

A script step runs code in a container (or on your local machine via the Runner). Use this for data processing, API calls, file operations, and anything that requires real computation.

```yaml
- id: pull_data
  type: script
  script: |
    python3 analytics_pull.py --days 7
```

### HTTP Steps

An HTTP step makes an outbound request to any URL — a Slack webhook, a CRM API, a notification service.

```yaml
- id: notify_slack
  type: http
  url: "https://hooks.slack.com/services/YOUR/WEBHOOK/URL"
  method: POST
  body: '{ "text": "{{ steps.summarize.output }}" }'
```

---

## Passing Data Between Steps

Steps reference each other's output using template syntax:

```
{{ steps.step_id.output }}
```

The output of one step flows automatically into the next. You can reference any previous step's output anywhere in a subsequent step's prompt, script, or HTTP body.

You can also reference trigger inputs:

```
{{ trigger.input.field_name }}
```

---

## Credentials in Workflows

If a workflow step needs access to an external service, credentials are injected securely — never hardcoded.

> "This workflow needs to send emails via Gmail. How do I connect it?"

WorkflowFiesta will prompt you to add your Gmail credentials through a secure form. Once saved, they are referenced in the workflow automatically and never exposed in logs or code.

See [Credentials](credentials.md) for how credential storage works.

---

## Monitoring Workflow Runs

Every workflow run is logged. From the **Workflows** section of the platform you can:

- See a history of every run — when it ran, how long it took, whether it succeeded
- Drill into any run to see each step's output
- View agent reasoning and tool calls within a step
- Identify exactly where a failure occurred

{% hint style="warning" %}
**Workflow runs are asynchronous.** After triggering a workflow, WorkflowFiesta will notify you when it completes. You do not need to wait or watch — it runs in the background.
{% endhint %}

---

## What to Read Next

| Topic | Link |
|---|---|
| Build your first workflow | [Quickstart](../getting-started/quickstart.md) |
| Understand agent steps | [Agents](agents.md) |
| Connect external services | [Credentials](credentials.md) |
| Run scripts on your machine | [Runner](runner.md) |
| Add slash command triggers | [Custom Commands](custom-commands.md) |
