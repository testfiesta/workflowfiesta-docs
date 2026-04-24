# Quickstart

Get your first AI agent running in five minutes. No code. No configuration files. Just a conversation.

{% hint style="info" %}
You need a WorkflowFiesta account to follow this guide. [Sign up free](https://app.workflowfiesta.com) if you have not already.
{% endhint %}

## Step 1 — Create your first agent

1. Open [app.workflowfiesta.com](https://app.workflowfiesta.com) and sign in
2. Click **New Agent** in the left sidebar
3. Give your agent a name — something descriptive like "Support Triage" or "Weekly Report Bot"
4. Write a system prompt in plain English describing what the agent should do

**Example system prompt:**
```text
You are a support triage assistant. When given a customer message, classify it as Bug, Feature Request, or Billing Question. Then write a one-sentence suggested reply.
```

5. Click **Save**

Your agent is now live. You can talk to it immediately from the chat panel on the right.

---

## Step 2 — Talk to your agent

Click the chat panel and type a message. The agent responds using the instructions you gave it in the system prompt.

Try sending it something realistic — a customer email, a piece of data, a question. See how it responds. If the output is not quite right, edit the system prompt and try again. This iteration loop is the core of building with WorkflowFiesta.

{% hint style="success" %}
There is no deploy step. Every change to the system prompt takes effect immediately in the next message.
{% endhint %}

---

## Step 3 — Connect a skill

Skills give your agent new capabilities: sending email, reading data, calling APIs, writing to Jira.

1. Go to **Settings → Skills**
2. Browse the skill library and click **Add** on any skill
3. The skill is now available to every agent in your org

Skills are org-wide — you add them once and all agents can use them.

---

## Step 4 — Run a workflow

Workflows let you chain agents together, schedule them to run automatically, or trigger them from a webhook.

1. Click **New Workflow** in the left sidebar
2. Choose a trigger: **Manual**, **Schedule**, or **Webhook**
3. Add a step — select **Agent** and choose the agent you just created
4. Write a prompt for that step
5. Click **Save**, then **Run**

You will see the workflow execute in real time in the run log.

{% hint style="info" %}
For a scheduled workflow — for example, a Monday morning report — set the trigger to **Schedule** and pick a cron time. The workflow runs automatically from that point on.
{% endhint %}

---

## Step 5 — Connect your local machine (optional)

If you want your agents to read local files, access internal systems, or run scripts on your own infrastructure, install the WorkflowFiesta Runner.

1. Go to **Settings → Runners**
2. Click **Add Runner** and follow the setup instructions
3. Download the runner binary for your OS and run it with the registration code

Once connected, your runner appears as an available environment. Any workflow step can target it directly.

{% tabs %}
{% tab title="macOS / Linux" %}
```bash
./workflowfiesta-runner --code YOUR_REGISTRATION_CODE
```
{% endtab %}
{% tab title="Windows" %}
```bash
workflowfiesta-runner.exe --code YOUR_REGISTRATION_CODE
```
{% endtab %}
{% endtabs %}

---

## What to do next

You have an agent, a skill, and a workflow. Here is where to go from here:

| I want to… | Go to |
|---|---|
| Understand agents, skills, and workflows in depth | [Key Concepts](key-concepts.md) |
| See what WorkflowFiesta is built for | [What is WorkflowFiesta?](what-is-workflowfiesta.md) |
| Connect my local machine | [Install the Runner](install-runner.md) |
| Join the community | [Discord](https://discord.gg/XEKxARDkNQ) |

