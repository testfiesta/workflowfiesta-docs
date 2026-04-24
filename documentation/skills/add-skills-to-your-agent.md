# Add Skills to Your Agent

Skills extend what your agents can do. This guide covers how skills work, how to add them, and how to use the most common ones.

{% hint style="info" %}
**Skills are org-wide.** Add a skill once and every agent in your organization can use it. There's no per-agent configuration required.
{% endhint %}

***

## How skills work

When you add a skill to your organization, it becomes available to all agents in two ways:

<table data-card-size="small" data-view="cards">
  <thead>
    <tr>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>📝 <strong>LLM Prompt Skills</strong></td>
      <td>Inject additional instructions into the agent's system prompt at runtime. The agent gains new knowledge, behavior, or API documentation without you editing its system prompt.</td>
    </tr>
    <tr>
      <td>⚙️ <strong>Script Skills</strong></td>
      <td>Execute code in a sandboxed container. Used in workflow steps to call external APIs, send emails, read files, and perform actions the LLM can't do on its own.</td>
    </tr>
  </tbody>
</table>

***

## Adding a skill

{% stepper %}
{% step %}
### Go to Settings → Skills

Click **Settings** in the left sidebar, then **Skills**.
{% endstep %}

{% step %}
### Browse the skill library

The library shows all available skills. Each skill has:
- A name and description
- The skill type (LLM Prompt or Script)
- What credentials it requires (if any)
{% endstep %}

{% step %}
### Click Add

Click **Add** on any skill. It's immediately available to all agents in your organization.

No restart required. No agent reconfiguration needed.
{% endstep %}

{% step %}
### Configure credentials (if required)

Some skills require API credentials to function — for example, the Gmail SMTP skill needs your Gmail address and an App Password.

If a skill requires credentials:
1. Go to **Settings → Credentials**
2. Click **Add Credential**
3. Select the service and fill in the fields
4. The skill will automatically use the stored credential

{% hint style="danger" %}
Never paste credentials directly into a system prompt or workflow script. Always use the Credentials vault. Credentials are encrypted at rest and injected securely at runtime.
{% endhint %}
{% endstep %}
{% endstepper %}

***

## The most useful skills

{% tabs %}
{% tab title="📧 Gmail SMTP" %}
### Gmail SMTP

Lets agents and workflow steps send email via Gmail.

**Requires:** Gmail address + App Password (not your regular password)

**Generate an App Password:**
Google Account → Security → 2-Step Verification → App Passwords

**In a workflow step:**
```yaml
- id: send_report
  type: script
  credentials:
    - service: gmail_smtp
      env:
        GMAIL_USER: username
        GMAIL_PASS: app_password
  env:
    RECIPIENT: "team@company.com"
    SUBJECT: "Weekly Report"
    BODY: "{{ steps.write_report.output }}"
  script: |
    #!/usr/bin/env python3
    import os, smtplib
    from email.mime.multipart import MIMEMultipart
    from email.mime.text import MIMEText
    # sends the email
```
{% endtab %}

{% tab title="🎯 Jira" %}
### Jira

Lets agents create, update, and query Jira issues via the REST API v3.

**Requires:** Jira URL, email, and API token

**Generate a Jira API token:**
Atlassian Account → Security → API tokens → Create API token

**What agents can do with it:**
- Create bugs, tasks, epics, and sub-tasks
- Update issue status, priority, and assignee
- Search issues using JQL
- Add comments and attachments
- Build sprint dashboards

{% hint style="success" %}
The Jira skill includes full ADF (Atlassian Document Format) knowledge — agents automatically format descriptions correctly without you needing to know the spec.
{% endhint %}
{% endtab %}

{% tab title="📊 Analytics Pull" %}
### Analytics Pull

Pulls data from Intercom, Google Analytics, Google Ads, and Jira in a single call. Generates cross-platform insights.

**Requires:** Credentials for each connected platform

**Usage:**
```bash
python3 analytics_orchestrator.py --days 7
```

**What it returns:**
- User signups and activity from Intercom
- Traffic and conversions from Google Analytics
- Campaign performance from Google Ads
- Sprint progress from Jira
- Cross-platform insights (e.g. which ad campaigns produce sticky users)
{% endtab %}

{% tab title="🔍 Web Research" %}
### Web Research

Gives agents the ability to search the web and synthesize information from multiple sources.

**No credentials required.**

**What agents can do with it:**
- Research competitors and market trends
- Look up documentation and technical specs
- Find recent news and announcements
- Cross-reference information across sources
- Cite sources with URLs

**Example system prompt addition:**
```
When asked to research a topic, use the web research skill to find
recent, authoritative sources. Always cite your sources.
```
{% endtab %}
{% endtabs %}

***

## Creating a custom skill

You can create your own skills to capture institutional knowledge, API documentation, or reusable behavior.

{% tabs %}
{% tab title="LLM Prompt Skill" %}
**Use for:** Knowledge, behavior rules, API documentation, brand voice guidelines

1. Go to **Settings → Skills → New Skill**
2. Select **LLM Prompt**
3. Write the skill content in markdown — this will be injected into the agent's system prompt

**Example: Brand Voice Skill**
```markdown
## Brand Voice Guidelines

When writing any content for WorkflowFiesta:
- Use confident, direct language — no hedging
- Avoid "revolutionary", "game-changing", "cutting-edge"
- Write in second person ("you can", not "users can")
- Use specific numbers over vague claims ("3x faster" not "much faster")
- Short sentences. Active voice. No jargon.
```
{% endtab %}

{% tab title="Script Skill" %}
**Use for:** API integrations, data transformations, file operations, external actions

1. Go to **Settings → Skills → New Skill**
2. Select **Script**
3. Write the script in Python or bash
4. Specify required credentials and environment variables

**Example: Slack Notification Skill**
```python
#!/usr/bin/env python3
import os, requests

SLACK_WEBHOOK = os.environ['SLACK_WEBHOOK_URL']
MESSAGE = os.environ['SLACK_MESSAGE']

response = requests.post(SLACK_WEBHOOK, json={"text": MESSAGE})
print(f"Slack notification sent: {response.status_code}")
```
{% endtab %}
{% endtabs %}

***

## Skills vs. system prompt instructions

> **When should I put something in a skill vs. directly in the system prompt?**

| Put it in a **skill** when... | Put it in the **system prompt** when... |
|---|---|
| Multiple agents need the same knowledge | It's specific to one agent's job |
| It's reusable across projects | It defines the agent's core identity |
| It's a technical spec (API docs, brand guide) | It describes the agent's specific task |
| You want to update it in one place | It rarely changes |

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
      <td>Use skills in workflow steps to automate multi-step processes.</td>
      <td><a href="../workflows/build-your-first-workflow.md">build-your-first-workflow.md</a></td>
    </tr>
    <tr>
      <td>🔌 <strong>Install the Runner</strong></td>
      <td>Run script skills on your own machine with local file access.</td>
      <td><a href="../runner/install-the-runner.md">install-the-runner.md</a></td>
    </tr>
    <tr>
      <td>🔑 <strong>Key Concepts</strong></td>
      <td>Review the full platform architecture and how skills fit in.</td>
      <td><a href="../getting-started/key-concepts.md">key-concepts.md</a></td>
    </tr>
  </tbody>
</table>
