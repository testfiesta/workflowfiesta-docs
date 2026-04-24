# Build Your First Workflow

Workflows are automated pipelines that chain agents, scripts, and HTTP calls together. This guide walks you through building a real workflow — a Monday morning report that runs itself.

{% hint style="info" %}
**Time:** ~15 minutes. **Prerequisites:** [Quickstart](../getting-started/quickstart.md) completed and at least one agent created.
{% endhint %}

***

## What we're building

A workflow that runs every Monday at 8am, pulls last week's key metrics, writes an executive summary, and emails it to your inbox. Zero manual work after setup.

```
TRIGGER: Every Monday 8am
       │
       ▼
STEP 1: Analytics Agent → pulls metrics, returns structured data
       │
       ▼
STEP 2: Report Writer Agent → writes executive summary from metrics
       │
       ▼
STEP 3: Script → sends HTML email via Gmail SMTP
       │
       ▼
DONE ✓ (inbox has the report before you open your laptop)
```

***

## Step-by-step

{% stepper %}
{% step %}
### Create the workflow

1. Go to **Workflows** in the left sidebar
2. Click **New Workflow**
3. Name it `Weekly Monday Report`
4. Add a description: `Pulls weekly metrics and emails an executive summary every Monday morning`
{% endstep %}

{% step %}
### Set the trigger

Click **Add Trigger** and select **Schedule**.

Set the cron expression:

```
0 8 * * 1
```

This means: **at 8:00am, every Monday** (UTC). Adjust the hour for your timezone.

{% hint style="info" %}
**Cron format:** `minute hour day-of-month month day-of-week`

Common examples:
- `0 9 * * 1-5` — 9am every weekday
- `0 7 * * 1` — 7am every Monday
- `0 0 1 * *` — midnight on the 1st of every month
{% endhint %}
{% endstep %}

{% step %}
### Add Step 1 — pull the data

Click **Add Step** → **Agent Step**.

| Field | Value |
|---|---|
| Step ID | `pull_metrics` |
| Agent | Your analytics agent (or any agent) |
| Prompt | `Pull last week's key metrics. Return structured data including: total signups, active users, top traffic sources, and any notable anomalies.` |

{% hint style="success" %}
The step ID matters — you'll reference it in later steps as `{{ steps.pull_metrics.output }}`.
{% endhint %}
{% endstep %}

{% step %}
### Add Step 2 — write the summary

Click **Add Step** → **Agent Step**.

| Field | Value |
|---|---|
| Step ID | `write_summary` |
| Agent | Report Writer (or any writing agent) |
| Prompt | `Write a concise executive summary from this data: {{ steps.pull_metrics.output }}. Format it as HTML with clear sections and a highlights table.` |

**Template syntax** — `{{ steps.pull_metrics.output }}` passes the output of Step 1 directly into Step 2's prompt. This is how data flows between steps.
{% endstep %}

{% step %}
### Add Step 3 — send the email

Click **Add Step** → **Script Step**.

Set the script:

```python
#!/usr/bin/env python3
import os, smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

GMAIL_USER = os.environ['GMAIL_USER']
GMAIL_PASS = os.environ['GMAIL_PASS']
RECIPIENT  = os.environ['RECIPIENT']
SUBJECT    = os.environ['SUBJECT']
BODY_HTML  = os.environ['REPORT_BODY']

msg = MIMEMultipart('alternative')
msg['Subject'] = SUBJECT
msg['From']    = GMAIL_USER
msg['To']      = RECIPIENT
msg.attach(MIMEText(BODY_HTML, 'html'))

with smtplib.SMTP('smtp.gmail.com', 587) as smtp:
    smtp.ehlo()
    smtp.starttls()
    smtp.login(GMAIL_USER, GMAIL_PASS)
    smtp.sendmail(GMAIL_USER, RECIPIENT, msg.as_string())

print("Report sent successfully.")
```

Add the environment variables:

```yaml
env:
  RECIPIENT: "you@yourcompany.com"
  SUBJECT: "Weekly Report — {{ trigger.scheduled_at }}"
  REPORT_BODY: "{{ steps.write_summary.output }}"
```

Add the credentials block:

```yaml
credentials:
  - service: gmail_smtp
    env:
      GMAIL_USER: username
      GMAIL_PASS: app_password
```

{% hint style="danger" %}
Never hardcode your Gmail password in the script. Always use the credentials block — credentials are encrypted and injected at runtime.
{% endhint %}
{% endstep %}

{% step %}
### Test it

Click **Run Now** to trigger the workflow manually. Watch the run log — each step shows its status, output, and any errors in real time.

If a step fails:
1. Click on the failed step in the run log
2. Read the error output
3. Fix the script or prompt
4. Click **Run Now** again

{% hint style="info" %}
You can run a workflow manually as many times as you need. The schedule trigger only fires on the configured schedule — manual runs don't count against it.
{% endhint %}
{% endstep %}

{% step %}
### Activate the schedule

Once the workflow runs successfully end-to-end, set the status to **Active**.

The workflow will now run automatically every Monday at 8am. You don't need to do anything else.
{% endstep %}
{% endstepper %}

***

## Workflow YAML reference

Every workflow is stored as YAML. You can edit it directly if you prefer.

{% tabs %}
{% tab title="Full example" %}
```yaml
name: Weekly Monday Report
description: Pulls weekly metrics and emails an executive summary every Monday morning

trigger:
  type: schedule
  cron: "0 8 * * 1"

steps:
  - id: pull_metrics
    type: agent
    agent: Analytics Agent
    prompt: "Pull last week's key metrics and return structured data."

  - id: write_summary
    type: agent
    agent: Report Writer
    prompt: "Write an executive summary from: {{ steps.pull_metrics.output }}"

  - id: send_email
    type: script
    credentials:
      - service: gmail_smtp
        env:
          GMAIL_USER: username
          GMAIL_PASS: app_password
    env:
      RECIPIENT: "you@yourcompany.com"
      SUBJECT: "Weekly Report"
      REPORT_BODY: "{{ steps.write_summary.output }}"
    script: |
      #!/usr/bin/env python3
      import os, smtplib
      from email.mime.multipart import MIMEMultipart
      from email.mime.text import MIMEText
      # ... send email
```
{% endtab %}

{% tab title="Template syntax" %}
Use `{{ expression }}` to pass data between steps:

| Expression | What it returns |
|---|---|
| `{{ trigger.input.field }}` | A field from the trigger's input payload |
| `{{ steps.step_id.output }}` | The full output of a previous step |
| `{{ trigger.scheduled_at }}` | The timestamp when the schedule fired |
| `{{ expression \| default('fallback') }}` | Value with a fallback if empty |
{% endtab %}

{% tab title="Trigger types" %}
```yaml
# Manual
trigger:
  type: manual

# Schedule (cron)
trigger:
  type: schedule
  cron: "0 8 * * 1"

# Webhook
trigger:
  type: webhook
  # WorkflowFiesta generates a unique URL for this workflow

# Chat message
trigger:
  type: chat
```
{% endtab %}
{% endtabs %}

***

## Troubleshooting

<details>

<summary>Step is failing with "undefined variable"</summary>

Check that the step ID you're referencing in `{{ steps.step_id.output }}` exactly matches the `id` field of the earlier step. IDs are case-sensitive.

</details>

<details>

<summary>Schedule isn't firing</summary>

1. Check that the workflow status is set to **Active** (not Draft)
2. Verify the cron expression using [crontab.guru](https://crontab.guru)
3. Remember that cron times are in UTC — adjust for your timezone

</details>

<details>

<summary>Email step is failing with authentication error</summary>

1. Make sure you're using a Gmail **App Password**, not your regular password
2. Generate one at: Google Account → Security → 2-Step Verification → App Passwords
3. Store it as a credential in **Settings → Credentials**, not in the script

</details>

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
      <td>🧩 <strong>Add Skills to Your Agent</strong></td>
      <td>Give your agents new capabilities — email, Jira, Slack, and more.</td>
      <td><a href="../skills/add-skills-to-your-agent.md">add-skills-to-your-agent.md</a></td>
    </tr>
    <tr>
      <td>🔌 <strong>Install the Runner</strong></td>
      <td>Run workflow scripts on your own machine with full local access.</td>
      <td><a href="../runner/install-the-runner.md">install-the-runner.md</a></td>
    </tr>
    <tr>
      <td>🔑 <strong>Key Concepts</strong></td>
      <td>Review triggers, steps, environments, and credentials in depth.</td>
      <td><a href="../getting-started/key-concepts.md">key-concepts.md</a></td>
    </tr>
  </tbody>
</table>
