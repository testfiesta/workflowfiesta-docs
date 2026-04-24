# What is WorkflowFiesta?

WorkflowFiesta is an AI orchestration platform. It connects AI agents, automated workflows, and your existing business tools into a single system that runs without constant human intervention.

***

## The problem it solves

Most AI tools give you a chat window. You ask a question, you get an answer, and then you manually do something with that answer. Every time.

WorkflowFiesta connects the steps. An agent doesn't just answer a question — it can send the answer as an email, create a Jira ticket, update a spreadsheet, or trigger the next agent in a pipeline. Automatically.

> "AI that actually does things, not just says things."

***

## The three layers

WorkflowFiesta is built in three layers that work together:

{% tabs %}
{% tab title="Layer 1 — Agents" %}
### Agents

An agent is an AI assistant with a specific job. You define its job in plain English via a **system prompt**. The agent uses that prompt to respond to every message it receives.

**Example:** A `Support Triage Agent` with the prompt:
> *"Classify incoming support messages as Bug, Feature Request, or Billing Question. Write a one-sentence suggested reply for each."*

Agents can be:
- Conversational (chat-based, interactive)
- Automated (invoked by a workflow step, no human in the loop)
- Specialist (one narrow job, called by a director agent)
- Director (orchestrates other agents, delegates sub-tasks)
{% endtab %}

{% tab title="Layer 2 — Skills" %}
### Skills

A skill extends what an agent can do. Skills are org-wide — add a skill once and every agent in your organization can use it.

There are two types:

| Type | What it does |
|---|---|
| **LLM Prompt** | Injects additional instructions into the agent's system prompt — teaches the agent new knowledge or behavior |
| **Script** | Executes code in a sandboxed container — lets the agent call APIs, read files, send emails, query databases |

**Example skills:** Gmail SMTP, Jira, Google Analytics, Slack, GitHub, HubSpot
{% endtab %}

{% tab title="Layer 3 — Workflows" %}
### Workflows

A workflow is an automated pipeline. It has a **trigger** (what starts it) and **steps** (what it does). Steps can invoke agents, run scripts, or make HTTP calls. Each step can pass its output to the next.

**Example workflow:**
1. **Trigger:** Every Monday at 8am
2. **Step 1:** Agent pulls last week's analytics data
3. **Step 2:** Agent writes an executive summary
4. **Step 3:** Script sends the summary as an HTML email

No human involvement after setup.
{% endtab %}
{% endtabs %}

***

## How the pieces connect

```
TRIGGER
   │
   ▼
WORKFLOW STEP 1 ──► Agent (reads data, reasons, writes output)
   │
   ▼
WORKFLOW STEP 2 ──► Script (sends email, updates database, calls API)
   │
   ▼
WORKFLOW STEP 3 ──► Agent (reviews output, flags issues, notifies team)
   │
   ▼
DONE ✓
```

Data flows from step to step using template syntax: `{{ steps.step1.output }}`. No manual copy-paste between tools.

***

## The Runner — connecting to your world

{% hint style="info" %}
The Runner is optional. Most workflows run entirely in the cloud. You only need the Runner if you want to access files or systems on your own machine or private network.
{% endhint %}

The WorkflowFiesta Runner is a lightweight binary you install on your own computer or server. Once connected:

- Agents can **read and write local files** — documents, spreadsheets, code repositories
- Agents can **query internal databases** that aren't exposed to the internet
- Agents can **run scripts on your hardware** with full OS access
- Agents can **access tools behind your firewall** — internal APIs, VPN-protected services

The Runner connects outbound to WorkflowFiesta's servers. No inbound ports required. No firewall changes.

***

## What WorkflowFiesta is not

{% hint style="warning" %}
**Not a no-code app builder.** WorkflowFiesta automates processes and orchestrates AI — it doesn't build customer-facing web apps or replace tools like Webflow or Bubble.
{% endhint %}

{% hint style="warning" %}
**Not a CRM or project management tool.** WorkflowFiesta connects to your CRM (HubSpot, Salesforce) and project tools (Jira, Linear) — it doesn't replace them.
{% endhint %}

{% hint style="warning" %}
**Not locked to one AI model.** WorkflowFiesta supports OpenAI, Anthropic, AWS Bedrock, and more. You choose the model per agent. You can switch at any time.
{% endhint %}

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
      <td>⚡ <strong>Quickstart</strong></td>
      <td>Build your first agent in 5 minutes.</td>
      <td><a href="quickstart.md">quickstart.md</a></td>
    </tr>
    <tr>
      <td>🔑 <strong>Key Concepts</strong></td>
      <td>The full glossary — every term defined with examples.</td>
      <td><a href="key-concepts.md">key-concepts.md</a></td>
    </tr>
    <tr>
      <td>🤖 <strong>Agents</strong></td>
      <td>Deep dive into building, configuring, and chaining agents.</td>
      <td><a href="../agents/build-your-first-agent.md">build-your-first-agent.md</a></td>
    </tr>
  </tbody>
</table>
