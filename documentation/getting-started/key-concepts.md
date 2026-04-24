# Key Concepts

A reference guide to every core concept in WorkflowFiesta. Bookmark this page — it's the one you'll return to when something needs clarifying.

***

## Platform architecture at a glance

```
┌─────────────────────────────────────────────────────────┐
│                    WorkflowFiesta                        │
│                                                         │
│  ┌──────────┐    ┌──────────┐    ┌──────────────────┐  │
│  │  Agents  │◄──►│  Skills  │    │    Workflows     │  │
│  └──────────┘    └──────────┘    │  ┌────────────┐  │  │
│       │                          │  │  Trigger   │  │  │
│       │                          │  └─────┬──────┘  │  │
│  ┌────▼─────┐    ┌──────────┐    │        │         │  │
│  │  Guards  │    │ Credentials│  │  ┌─────▼──────┐  │  │
│  └──────────┘    └──────────┘    │  │   Steps    │  │  │
│                                  │  └────────────┘  │  │
│  ┌──────────┐    ┌──────────┐    └──────────────────┘  │
│  │ Runners  │◄──►│Environments│                        │
│  └──────────┘    └──────────┘                          │
└─────────────────────────────────────────────────────────┘
```

***

## Agent

An agent is an AI assistant with a specific job. It has a name, a **system prompt** (plain English instructions), and a model configuration.

**System prompt** — the instructions that define what the agent does, how it responds, and what it knows. Written in plain English. No code required.

**Model** — the AI model powering the agent (GPT-4o, Claude Sonnet, etc.). You choose per agent. You can switch at any time.

{% hint style="info" %}
Agents can be conversational (you chat with them) or automated (a workflow invokes them with a prompt and uses their output). The same agent can do both.
{% endhint %}

<details>

<summary>Example: a support triage agent</summary>

**Name:** Support Triage

**System prompt:**
```
You are a support triage assistant. When given a customer message:
1. Classify it as: Bug, Feature Request, or Billing Question
2. Assign a priority: High, Medium, or Low
3. Write a one-sentence suggested reply

Respond in JSON format.
```

**Used in:** A webhook workflow that fires when a new Intercom message arrives.

</details>

***

## Skill

A skill extends what an agent can do. Skills are **org-wide** — add a skill once and every agent in your organization can use it.

| Type | What it does | Example |
|---|---|---|
| **LLM Prompt** | Injects instructions into the agent's system prompt | Jira knowledge, brand voice guidelines, API documentation |
| **Script** | Executes code in a sandboxed container | Send email via Gmail, create a Jira ticket, query a database |

{% hint style="success" %}
Skills are additive. An agent with the Gmail skill + the Jira skill can send emails **and** create tickets. Stack as many as you need.
{% endhint %}

***

## Workflow

A workflow is an automated pipeline. It has a **trigger** that starts it and **steps** that run in sequence. Each step can pass its output to the next using template syntax.

```yaml
name: Weekly Report
steps:
  - id: pull_data
    type: agent
    agent: Analytics Agent
    prompt: "Pull last week's key metrics"

  - id: write_summary
    type: agent
    agent: Report Writer
    prompt: "Write an executive summary from: {{ steps.pull_data.output }}"

  - id: send_email
    type: script
    script: |
      # sends the summary via Gmail SMTP
```

{% hint style="info" %}
Workflows are defined in YAML but you don't need to write YAML by hand. The Workflow Builder agent can generate and iterate on YAML from a plain English description.
{% endhint %}

***

## Trigger

A trigger defines what starts a workflow. There are four types:

<table data-card-size="small" data-view="cards">
  <thead>
    <tr>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>🖱️ <strong>Manual</strong></td>
      <td>You click Run in the UI, or call the API. Good for testing and on-demand tasks.</td>
    </tr>
    <tr>
      <td>🕐 <strong>Schedule</strong></td>
      <td>Runs automatically on a cron schedule. Good for daily reports and recurring syncs.</td>
    </tr>
    <tr>
      <td>🔗 <strong>Webhook</strong></td>
      <td>Fires when an external service sends an HTTP request to your workflow's URL.</td>
    </tr>
    <tr>
      <td>💬 <strong>Chat</strong></td>
      <td>Triggered by a message in a chat conversation. Good for interactive agent pipelines.</td>
    </tr>
  </tbody>
</table>

***

## Step

A step is a single unit of work inside a workflow. Steps run in sequence. There are three types:

{% tabs %}
{% tab title="Agent Step" %}
Invokes an agent with a prompt. The agent's response becomes the step's output.

```yaml
- id: write_summary
  type: agent
  agent: Report Writer
  prompt: "Summarize this data: {{ steps.pull_data.output }}"
```
{% endtab %}

{% tab title="Script Step" %}
Runs a shell or Python script in a container (or on your Runner). Good for API calls, file operations, and data transformations.

```yaml
- id: send_email
  type: script
  script: |
    #!/usr/bin/env python3
    import smtplib
    # send the email
  env:
    RECIPIENT: "team@company.com"
```
{% endtab %}

{% tab title="HTTP Step" %}
Makes an outbound HTTP request to any URL. Good for calling external APIs or triggering webhooks.

```yaml
- id: notify_slack
  type: http
  url: "https://hooks.slack.com/services/YOUR/WEBHOOK/URL"
  method: POST
  body: '{"text": "{{ steps.write_summary.output }}"}'
```
{% endtab %}
{% endtabs %}

***

## Environment

An environment defines where and how script steps run. It specifies:

- **Docker image** — the container image (e.g. `python:3.11-slim`, `node:20`, `debian:latest`)
- **Environment variables** — values injected into every script in this environment
- **Runner** — optionally attach a self-hosted Runner so scripts run on your own machine

{% hint style="info" %}
If you don't specify an environment, script steps run in the default platform container with Python, Node.js, curl, and common tools pre-installed.
{% endhint %}

***

## Runner

The Runner is a lightweight binary you install on your own computer or server. Once connected, agents and workflow steps can run commands natively on that machine.

**When you need it:**
- Reading files from your local drive or network share
- Querying internal databases not exposed to the internet
- Running scripts that require local tools or VPN access
- Accessing systems behind your firewall

**When you don't need it:**
- Most workflows that call external APIs
- Agents that work with data passed directly in prompts
- Anything that runs entirely in the cloud

{% tabs %}
{% tab title="macOS / Linux" %}
```bash
curl -L https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-linux-amd64 -o wff-runner
chmod +x wff-runner
./wff-runner --code YOUR_REGISTRATION_CODE
```
{% endtab %}

{% tab title="Windows" %}
Download the GUI app from the [releases page](https://github.com/ss-libs/workflowfiesta-runner/releases/latest) and paste your registration code from **Settings → Runners → Add Runner**.
{% endtab %}
{% endtabs %}

***

## Credential

A credential is an encrypted secret stored in WorkflowFiesta's credential vault. Credentials are never exposed in logs or UI — they're injected into workflow steps at runtime.

{% hint style="danger" %}
Never paste API keys, passwords, or tokens directly into a system prompt or workflow YAML. Always store them as credentials and reference them via the credentials block.
{% endhint %}

**In a workflow step:**
```yaml
- id: send_email
  type: script
  credentials:
    - service: gmail_smtp
      env:
        GMAIL_USER: username
        GMAIL_PASS: app_password
  script: |
    # GMAIL_USER and GMAIL_PASS are now available as env vars
```

***

## Guard

A guard is a safety policy applied to agent inputs or outputs. Guards can:

- **Block** messages that match a pattern (e.g. prompt injection attempts)
- **Redact** sensitive data before it reaches the model
- **Flag** outputs that contain disallowed content

Guards are configured at the org level and apply to all agents.

***

## What to read next

<table data-view="cards">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th data-hidden data-card-target data-type="content-ref"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>🤖 <strong>Build Your First Agent</strong></td>
      <td>Put these concepts into practice — build a real agent step by step.</td>
      <td><a href="../agents/build-your-first-agent.md">build-your-first-agent.md</a></td>
    </tr>
    <tr>
      <td>⚙️ <strong>Build Your First Workflow</strong></td>
      <td>Chain steps, pass data, and schedule your first automated pipeline.</td>
      <td><a href="../workflows/build-your-first-workflow.md">build-your-first-workflow.md</a></td>
    </tr>
    <tr>
      <td>🔌 <strong>Install the Runner</strong></td>
      <td>Connect your local machine so agents can access your files and systems.</td>
      <td><a href="../runner/install-the-runner.md">install-the-runner.md</a></td>
    </tr>
  </tbody>
</table>
