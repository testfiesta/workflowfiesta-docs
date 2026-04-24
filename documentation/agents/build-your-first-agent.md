# Build Your First Agent

Agents are the core building block of WorkflowFiesta. This guide walks you through building a real, useful agent from scratch — and explains the design decisions along the way.

{% hint style="info" %}
**Time:** ~10 minutes. **Prerequisites:** A WorkflowFiesta account and the [Quickstart](../getting-started/quickstart.md) completed.
{% endhint %}

***

## What makes a good agent?

Before writing a single word of a system prompt, answer three questions:

<table data-card-size="small" data-view="cards">
  <thead>
    <tr>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>🎯 <strong>What is the one job?</strong></td>
      <td>Agents work best with a single, well-defined responsibility. "Triage support tickets" is good. "Handle all of customer support" is too broad.</td>
    </tr>
    <tr>
      <td>📥 <strong>What does it receive?</strong></td>
      <td>What input will the agent get? A customer message? A data export? A URL? Define this clearly in the system prompt.</td>
    </tr>
    <tr>
      <td>📤 <strong>What does it produce?</strong></td>
      <td>What should the output look like? Plain text? JSON? A formatted report? Specify the format explicitly.</td>
    </tr>
  </tbody>
</table>

***

## Step-by-step: build a support triage agent

We'll build a practical agent that classifies incoming support messages and drafts a suggested reply.

{% stepper %}
{% step %}
### Create the agent

1. Go to **Agents** in the left sidebar
2. Click **New Agent**
3. Set the name: `Support Triage`
4. Leave the model as the default for now
{% endstep %}

{% step %}
### Write the system prompt

The system prompt is the most important part. Be specific about inputs, outputs, and format.

```text
You are a support triage assistant for WorkflowFiesta.

When you receive a customer message, do the following:

1. CLASSIFY the message as one of:
   - Bug Report
   - Feature Request
   - Billing Question
   - General Question

2. ASSIGN a priority:
   - High: service is down, data loss, billing error
   - Medium: feature not working as expected
   - Low: general question, feature request

3. DRAFT a one-sentence suggested reply that acknowledges the issue
   and sets expectations for next steps.

Respond in this exact JSON format:
{
  "category": "...",
  "priority": "...",
  "suggested_reply": "..."
}
```

{% hint style="success" %}
**Why JSON?** When this agent is used in a workflow, the next step can parse the JSON output and route the ticket automatically — High priority to Slack, Low priority to email.
{% endhint %}
{% endstep %}

{% step %}
### Test it in chat

Click the chat panel on the right. Send a realistic customer message:

> *"Hey, I've been charged twice for my subscription this month and I can't reach anyone. This is urgent."*

The agent should respond with:
```json
{
  "category": "Billing Question",
  "priority": "High",
  "suggested_reply": "We're sorry to hear about the duplicate charge — our billing team will review your account and respond within 2 hours."
}
```

If the output isn't right, refine the prompt. Common fixes:

<details>

<summary>Output isn't in JSON format</summary>

Add this line to the end of your system prompt:

```
Always respond with valid JSON only. No preamble, no explanation, no markdown code fences.
```

</details>

<details>

<summary>Priority classification is off</summary>

Add more examples to the priority definitions:

```
- High: service is down, data loss, billing error, account locked
- Medium: feature not working as expected, slow performance, UI bug
- Low: general question, feature request, "how do I..." questions
```

</details>
{% endstep %}

{% step %}
### Set the temperature

Temperature controls how creative vs. consistent the agent's responses are.

| Temperature | Best for |
|---|---|
| `0.0 – 0.3` | Structured outputs, classification, JSON — consistent and predictable |
| `0.4 – 0.7` | General-purpose agents — balanced |
| `0.8 – 1.2` | Creative writing, brainstorming — more varied |

For a triage agent producing JSON, set temperature to `0.1`.

Go to **Agent Settings → Advanced → Temperature** and set it to `0.1`.
{% endstep %}

{% step %}
### Add a skill (optional)

If you want this agent to automatically create a Jira ticket after triaging, add the **Jira** skill:

1. Go to **Settings → Skills**
2. Find **Jira** and click **Add**
3. Update your system prompt to include Jira ticket creation instructions

The skill injects Jira API knowledge directly into the agent's context.
{% endstep %}
{% endstepper %}

***

## Agent design patterns

{% tabs %}
{% tab title="Specialist Agent" %}
### Specialist Agent

Does one job extremely well. Called by a director agent or a workflow step.

**When to use:** Any time you have a discrete, repeatable task.

**Example system prompts:**
- "Classify this support message and return JSON."
- "Write a meta description for this blog post. Max 160 characters."
- "Extract all action items from this meeting transcript."
{% endtab %}

{% tab title="Director Agent" %}
### Director Agent

Orchestrates other agents. Receives a high-level goal, breaks it into sub-tasks, and delegates.

**When to use:** Multi-step tasks that require different types of expertise.

**Example system prompt:**
```
You are a blog production director. When given a topic:
1. Call the Keyword Researcher to find target keywords
2. Call the SEO Architect to build the article outline
3. Call the Copywriter to write the full draft
4. Return the completed article
```
{% endtab %}

{% tab title="Conversational Agent" %}
### Conversational Agent

Maintains context across a multi-turn conversation. Designed for interactive use.

**When to use:** Customer support, internal Q&A, interactive data exploration.

**Tips:**
- Include persona and tone instructions ("Be concise and professional")
- Define escalation triggers ("If the user mentions legal action, escalate immediately")
- Specify what the agent should NOT do ("Never promise refunds without manager approval")
{% endtab %}
{% endtabs %}

***

## Common mistakes

{% hint style="danger" %}
**Vague system prompts produce vague outputs.** "Be helpful" is not a system prompt. "When given a customer email, extract the customer's name, issue type, and urgency level, then return JSON" is.
{% endhint %}

{% hint style="warning" %}
**Don't give one agent too many jobs.** An agent that triages tickets, writes blog posts, and manages your calendar will do all three poorly. Build specialists.
{% endhint %}

{% hint style="warning" %}
**Don't hardcode credentials in system prompts.** Never paste API keys or passwords into a system prompt. Use the Credentials vault and the credentials block in workflows.
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
      <td>⚙️ <strong>Build Your First Workflow</strong></td>
      <td>Wire your agent into an automated pipeline that runs on a schedule.</td>
      <td><a href="../workflows/build-your-first-workflow.md">build-your-first-workflow.md</a></td>
    </tr>
    <tr>
      <td>🧩 <strong>Add Skills to Your Agent</strong></td>
      <td>Give your agent the ability to send email, create tickets, and call APIs.</td>
      <td><a href="../skills/add-skills-to-your-agent.md">add-skills-to-your-agent.md</a></td>
    </tr>
    <tr>
      <td>🔑 <strong>Key Concepts</strong></td>
      <td>Review agents, skills, workflows, and how they connect.</td>
      <td><a href="../getting-started/key-concepts.md">key-concepts.md</a></td>
    </tr>
  </tbody>
</table>
