---
icon: bolt-lightning
---

# Quickstart

Get your first AI agent running in five minutes. No code. No configuration files. Just a conversation.

{% hint style="info" %}
**Prerequisites:** A WorkflowFiesta account. [Sign up free](https://app.workflowfiesta.com) if you haven't already.
{% endhint %}

***

## What you'll build

By the end of this guide you'll have a working AI agent that can receive messages, respond intelligently, and be wired into a workflow. The whole thing takes about five minutes.

***

## Steps

{% stepper %}
{% step %}
#### Create your first agent

Open [app.workflowfiesta.com](https://app.workflowfiesta.com) and sign in. Then just tell WorkflowFiesta what you want to build:

> "Create a support triage agent. When given a customer message, classify it as Bug, Feature Request, or Billing Question, then write a one-sentence suggested reply."

WorkflowFiesta will ask a few clarifying questions — tone, escalation rules, any specific constraints — then create the agent. It's live immediately. No deploy step.

{% hint style="success" %}
You can also create agents from **Settings → Agents → New Agent** if you prefer to fill in the details yourself.
{% endhint %}
{% endstep %}

{% step %}
#### Talk to your agent

Click the chat panel and send a message. Try something realistic — a customer email, a piece of data, a question your team gets every day.

The agent responds using the instructions in its system prompt. If the output isn't quite right, just tell it:

> "Be more concise. Keep replies under two sentences."

Every change takes effect on the very next message. No restart, no redeploy. This iteration loop is the core of building with WorkflowFiesta.
{% endstep %}

{% step %}
#### Add a skill (optional)

Skills are reusable building blocks that make agent behavior consistent across your organization. There are two types:

- **Prompt skills** inject domain expertise or style rules into the agent's system prompt
- **Script skills** package a specific script the agent can execute

> "Add the Jira skill to this agent so it follows our ticket format every time."

> "Give this agent the Marketing Copy skill so it always writes in our brand voice."

Skills are org-wide — once created, any agent can use them. Browse what's available in **Settings → Skills**.

{% hint style="info" %}
Skills don't unlock capabilities an agent doesn't otherwise have. An agent's ability to take action comes from its platform access level and tools. Skills make behavior consistent and reusable.
{% endhint %}
{% endstep %}

{% step %}
#### Run a workflow

Workflows chain agents, scripts, and HTTP calls into automated pipelines that run on a schedule or trigger.

> "Create a workflow that runs every Monday at 9am, uses this agent to summarize last week's support tickets, and emails the summary to our team."

WorkflowFiesta asks what data you need, what format, and who to send it to — then builds and schedules it automatically.

{% tabs %}
{% tab title="Manual trigger" %}
Run on demand from the UI or via the API. Good for testing and one-off tasks.

```yaml
trigger:
  type: manual
```
{% endtab %}

{% tab title="Schedule trigger" %}
Run automatically on a cron schedule. Good for daily reports and recurring syncs.

```yaml
trigger:
  type: schedule
  cron: "0 9 * * 1"   # Every Monday at 9am UTC
```
{% endtab %}

{% tab title="Webhook trigger" %}
Fire when an external service sends an HTTP request to your workflow's URL.

```yaml
trigger:
  type: webhook
```
{% endtab %}
{% endtabs %}
{% endstep %}

{% step %}
#### Install the Runner (optional)

The Runner is a lightweight binary you install on your own machine or server. Once connected, agents can read local files, access internal databases, and run scripts on your hardware.

{% tabs %}
{% tab title="macOS" %}
```bash
# Download
curl -L https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-darwin-arm64 -o wff-runner
chmod +x wff-runner

# Register (get your code from Settings → Runners → Add Runner)
./wff-runner --code YOUR_REGISTRATION_CODE
```
{% endtab %}

{% tab title="Linux" %}
```bash
# Download
curl -L https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-linux-amd64 -o wff-runner
chmod +x wff-runner

# Register
./wff-runner --code YOUR_REGISTRATION_CODE
```
{% endtab %}

{% tab title="Windows" %}
```powershell
# Download the GUI app
# https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-windows-amd64-gui.exe

# Run it, paste your registration code from Settings → Runners → Add Runner
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
The Runner is optional. You only need it if you want agents to access files or systems on your local machine or private network.
{% endhint %}
{% endstep %}
{% endstepper %}

***

## You're set up. What's next?

| | |
|---|---|
| [🧠 What is WorkflowFiesta?](what-is-workflowfiesta.md) | Understand the platform before you build deeper |
| [⚙️ Agents](../workflowfiesta/agents.md) | Deep dive into system prompts, tools, and agent design |
| [🔁 Workflows](../workflowfiesta/workflows.md) | Chain steps, pass data, and schedule runs |
| [🔧 Skills](../workflowfiesta/skills.md) | What skills are and how to use them |
| [👥 Discord](https://discord.gg/XEKxARDkNQ) | Ask the community |
