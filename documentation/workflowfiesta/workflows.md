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

## Passing Data Between Steps

Steps reference each other's output using template syntax:

```
{{ steps.step_id.output }}
```

The output of one step flows automatically into the next. You can reference any previous step's output anywhere in a subsequent step's prompt, script, or HTTP body.

## Credentials in Workflows

If a workflow step needs to authenticate with an external service, it uses credentials stored in WorkflowFiesta's secure credential store. Credentials are injected as environment variables at runtime — they never appear in the workflow definition or logs.

> "Add a step that sends the report via Gmail."

WorkflowFiesta will check if Gmail credentials exist. If not, it will open a secure form to collect them before adding the step.

See [Credentials](credentials.md).

## Monitoring Workflow Runs

Every time a workflow runs, a run record is created. You can see:
- When it ran and how long it took
- The output of each step
- Any errors that occurred
- The full agent conversation for agent steps

If a workflow fails, WorkflowFiesta will show you exactly which step failed and why.

## Frequently Asked Questions

<details>
<summary>Can a workflow call multiple agents?</summary>
Yes. A workflow can have as many agent steps as needed. Each agent step can call a different agent. This is how complex multi-agent pipelines work — a research agent gathers data, a writing agent drafts content, a review agent checks it, and a publishing agent sends it.
</details>

<details>
<summary>Can workflows trigger other workflows?</summary>
Yes, via HTTP steps. One workflow can POST to another workflow's webhook URL to chain them together.
</details>

<details>
<summary>What happens if a step fails?</summary>
The workflow stops at the failed step and logs the error. You can view the failure in the run history, fix the issue, and re-run from the beginning.
</details>

<details>
<summary>Can I test a workflow before scheduling it?</summary>
Yes. You can trigger any workflow manually from chat or from the workflow detail page to test it before enabling the schedule.
</details>
