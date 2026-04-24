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

1. Open [app.workflowfiesta.com](https://app.workflowfiesta.com) and sign in
2. Click **New Agent** in the left sidebar
3. Give your agent a descriptive name — `Support Triage` or `Weekly Report Bot`
4. Write a system prompt in plain English

**Example system prompt:**

```
You are a support triage assistant. When given a customer message,
classify it as Bug, Feature Request, or Billing Question.
Then write a one-sentence suggested reply.
```

5. Click **Save**

Your agent is live immediately. No deploy step.
{% endstep %}

{% step %}
#### Talk to your agent

Click the chat panel on the right and send a message. Try something realistic — a customer email, a piece of data, a question your team gets every day.

The agent responds using the instructions in its system prompt. If the output isn't quite right, edit the prompt and try again. This iteration loop is the core of building with WorkflowFiesta.

{% hint style="success" %}
Every change to the system prompt takes effect on the very next message. No restart, no redeploy.
{% endhint %}
{% endstep %}

{% step %}
#### Add a skill

Skills give your agent new capabilities: sending email, reading data, calling APIs, writing to Jira.

1. Go to **Settings → Skills**
2. Browse the skill library and click **Add** on any skill
3. The skill is now available to every agent in your organization

Skills are org-wide — add once, available everywhere.

{% hint style="info" %}
The **Gmail SMTP** skill lets any agent send email. The **Jira** skill lets any agent create and update tickets. Browse the full library in Settings.
{% endhint %}
{% endstep %}

{% step %}
#### Run a workflow

Workflows chain agents, scripts, and HTTP calls into automated pipelines.

1. Go to **Workflows** in the left sidebar
2. Click **New Workflow**
3. Add a trigger — choose **Manual**, **Schedule**, or **Webhook**
4. Add a step — select **Agent**, pick your agent, write a prompt
5. Click **Run** to test it

{% tabs %}
{% tab title="Manual trigger" %}
A manual trigger lets you run the workflow on demand from the UI or via the API. Good for testing and one-off tasks.

```yaml
trigger:
  type: manual
```
{% endtab %}

{% tab title="Schedule trigger" %}
A schedule trigger runs the workflow automatically on a cron schedule. Good for daily reports and recurring syncs.

```yaml
trigger:
  type: schedule
  cron: "0 9 * * 1"   # Every Monday at 9am UTC
```
{% endtab %}

{% tab title="Webhook trigger" %}
A webhook trigger fires when an external service sends an HTTP request to your workflow's URL. Good for responding to form submissions, Stripe events, or GitHub webhooks.

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

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>🧠 <strong>Key Concepts</strong></td><td>Understand agents, skills, workflows, and runners in depth.</td><td><a href="/broken/pages/NTG9K8RkGRICSNDTJpqN">Broken link</a></td></tr><tr><td>🤖 <strong>Build Your First Agent</strong></td><td>A deeper guide to system prompts, tools, and agent design.</td><td><a href="/broken/pages/Z4nwOkbhpuz9xKs806RE">Broken link</a></td></tr><tr><td>⚙️ <strong>Build Your First Workflow</strong></td><td>Chain multiple steps, pass data between them, and schedule runs.</td><td><a href="/broken/pages/rLfM8h3XRBsPDW5iRAIc">Broken link</a></td></tr></tbody></table>
