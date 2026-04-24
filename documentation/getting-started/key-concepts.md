# Key Concepts

WorkflowFiesta uses a small set of building blocks. Once you understand each one and how they connect, the rest of the platform makes sense immediately.

---

## Agent

An agent is an AI assistant you configure for a specific job.

Every agent has:
- A **name** — how you and your team refer to it
- A **system prompt** — instructions that define its role, tone, and behavior
- A **model** — the AI model it runs on (Claude, GPT-4, and others)

Agents respond to messages in chat, get invoked by workflows, or call other agents as sub-agents in a pipeline.

{% hint style="info" %}
Think of an agent as a specialist on your team. One agent handles customer support. Another writes blog posts. Another pulls analytics. Each one is configured for its job and nothing else.
{% endhint %}

**Where to go next:** [Build Your First Agent](../agents/build-your-first-agent.md)

---

## Skill

A skill extends what an agent knows or can do.

Skills are **org-wide** — once a skill exists, any agent in your organization can use it. There are two types:

| Type | What it does |
|------|-------------|
| **LLM Prompt** | Injects additional instructions into the agent's system prompt at runtime |
| **Script** | Executes code in a sandboxed container as a workflow step |

Examples of LLM prompt skills: writing style guidelines, brand voice rules, a library of SQL patterns, a security checklist.

Examples of script skills: send an email via Gmail SMTP, pull data from a Jira board, run a Python analysis script.

{% hint style="info" %}
Skills are additive. An agent's effective capability is its system prompt plus every skill attached to it. You can mix and match without touching the agent's core configuration.
{% endhint %}

---

## Workflow

A workflow is a multi-step automation pipeline.

Each workflow has:
- A **trigger** — what starts it (a schedule, a webhook, a chat message, or an API call)
- One or more **steps** — agent calls, scripts, or HTTP requests executed in sequence
- **Data passing** — outputs from one step flow into the next via template variables

```yaml
# Example: a simple two-step workflow
steps:
  - id: analyze
    type: agent
    agent: Analytics Agent
    prompt: "Summarize last week's signups from Intercom"

  - id: send
    type: script
    script: |
      # send the summary by email
```

{% hint style="success" %}
Workflows are how you turn a one-off agent conversation into something that runs automatically — every day, every Monday at 9am, or every time a webhook fires.
{% endhint %}

**Where to go next:** [Build Your First Workflow](../workflows/build-your-first-workflow.md)

---

## Trigger

A trigger is what starts a workflow.

| Trigger type | When it fires |
|---|---|
| **Manual** | You click "Run" in the UI or call the API |
| **Schedule** | A cron expression — e.g. every Monday at 9am |
| **Webhook** | An inbound HTTP POST from an external service |
| **Chat** | A user message in a conversation invokes the workflow |

Trigger inputs (the payload that comes in) are available in workflow steps as `{{ trigger.input.field_name }}`.

---

## Step

A step is one unit of work inside a workflow.

There are three step types:

| Type | What it does |
|---|---|
| **agent** | Invokes an agent with a prompt and captures its response |
| **script** | Runs a shell or Python script in a container or on your Runner |
| **http** | Makes an outbound HTTP request to any URL |

Steps run in sequence by default. The output of each step is available to every step that follows it via `{{ steps.step_id.output }}`.

---

## Environment

An environment defines where script steps run.

Each environment specifies:
- A **Docker image** — the container image used to execute scripts (e.g. `python:3.11-slim`, `debian:latest`)
- **Environment variables** — values injected into every script that runs in this environment
- A **runner** — optionally, a self-hosted runner attached to this environment

If no environment is specified, script steps run in the default platform container.

{% hint style="info" %}
Environments let you control exactly what's available when a script runs — the OS, installed packages, environment variables, and whether it runs in the cloud or on your own machine.
{% endhint %}

---

## Runner

A runner is a lightweight agent you install on your own computer or server.

Once a runner is connected, any workflow step or bash command can run **natively on that machine** — with full access to its local filesystem, network drives, databases, and installed tools.

Runners are optional. You only need one if your workflows need to:
- Read or write local files
- Access systems that aren't on the public internet
- Use tools installed on a specific machine

{% hint style="success" %}
The runner is a single binary. It takes about two minutes to install and connects immediately. No firewall changes required — it opens an outbound connection to the platform.
{% endhint %}

**Where to go next:** [Install the Runner](../runner/install.md)

---

## Credential

A credential is a securely stored secret — an API key, password, token, or OAuth connection.

Credentials are stored encrypted at the org level. Workflow steps reference them by name; the actual values are never exposed in logs, YAML, or chat.

```yaml
# Reference a credential in a workflow step
steps:
  - id: send_email
    type: script
    credentials:
      - gmail_smtp
    script: |
      # GMAIL_USER and GMAIL_PASS are injected automatically
```

{% hint style="danger" %}
Never paste credentials directly into a system prompt, workflow YAML, or chat message. Always store them in Settings → Credentials and reference them by name.
{% endhint %}

---

## Guard

A guard is a safety policy that runs on agent inputs or outputs.

Guards can:
- Block messages that match a pattern (e.g. requests to reveal the system prompt)
- Redact sensitive data before it reaches the agent or leaves in a response
- Enforce topic restrictions for customer-facing agents

Guards are configured at the org level and applied per agent.

---

## How the pieces connect

```
Trigger
  └── Workflow
        ├── Step 1: Agent (uses Skills)
        │     └── runs in Environment (on Runner if local)
        ├── Step 2: Script
        │     └── uses Credentials
        └── Step 3: HTTP
```

Every automation on WorkflowFiesta is some combination of these eight concepts. You don't need all of them for every use case — most workflows use three or four.

---

## What to read next

| If you want to... | Go here |
|---|---|
| Build your first agent | [Build Your First Agent](../agents/build-your-first-agent.md) |
| Automate something on a schedule | [Build Your First Workflow](../workflows/build-your-first-workflow.md) |
| Access local files and systems | [Install the Runner](../runner/install.md) |
| Understand the platform architecture | [What is WorkflowFiesta?](what-is-workflowfiesta.md) |
| Get unstuck | [Discord Community](https://discord.gg/XEKxARDkNQ) |
