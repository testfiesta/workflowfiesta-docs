---
icon: key
---

# Credentials

Credentials are API keys, passwords, and tokens that your agents and workflows use to connect to external services. WorkflowFiesta stores them encrypted — they are never exposed in chat, logs, or workflow definitions.

{% hint style="danger" %}
**Never paste API keys or passwords into the chat.** Always use the secure credential form the platform provides. This keeps your secrets out of conversation logs permanently.
{% endhint %}

## How Credentials Work

When an agent or workflow needs to connect to an external service — Jira, Gmail, Slack, Google Analytics — it needs credentials to authenticate. WorkflowFiesta handles this through a secure form flow:

{% stepper %}
{% step %}
### You describe what you want to connect
"I want my agent to be able to send emails via Gmail."
{% endstep %}
{% step %}
### The platform tells you what it needs
"I'll need your Gmail address and an App Password. Go to Google Account → Security → 2-Step Verification → App Passwords. Generate one for WorkflowFiesta. When you're ready, I'll open a secure form."
{% endstep %}
{% step %}
### A secure form opens in the UI
You enter your credentials into the form. The values are masked as you type. They are encrypted before being stored.
{% endstep %}
{% step %}
### The credential is saved and referenced
The credential is stored with a name (e.g. "gmail_smtp"). Your agent or workflow references it by name — the actual value is never visible again.
{% endstep %}
{% endstepper %}

## Adding Credentials

You can add credentials through conversation:

> "I want to connect to Intercom. Walk me through it."

> "Add Jira credentials so my agent can create tickets."

> "I need to connect to Stripe — help me set that up."

The platform will guide you through finding the right API key or token for each service and open the secure form at the right moment.

## OAuth Connections

For services that use OAuth (Google, GitHub, Slack, Discord, HubSpot, and others), WorkflowFiesta uses a browser-based OAuth flow instead of a form:

> "Connect my Google account so my agent can read my Gmail."

The platform opens the provider's consent screen in a new browser tab. You log in and grant permission. The access token is stored automatically — you never see or handle it directly.

**Supported OAuth providers include:**
Google · Microsoft · GitHub · GitLab · Slack · Discord · Atlassian (Jira/Confluence) · Notion · Linear · HubSpot · Salesforce · Zoom · Stripe · Airtable · and more.

## Credential Security

| Property | Detail |
|---|---|
| **Encryption** | All credentials are encrypted at rest |
| **Scope** | Credentials are org-wide — available to all agents and workflows in your org |
| **Visibility** | Values are never shown after saving — not in chat, not in logs, not in the UI |
| **Injection** | In workflows, credentials are injected as environment variables at runtime |
| **Rotation** | You can update a credential at any time by saving a new value under the same name |

## Using Credentials in Workflows

In workflow YAML, credentials are referenced by service name. The actual values are injected at runtime:

```yaml
steps:
  - id: send_email
    type: script
    credentials:
      - service: gmail_smtp
        env:
          GMAIL_USER: username
          GMAIL_PASS: app_password
    script: |
      python3 send_report.py
```

Alternatively, all org credentials are auto-injected as environment variables using the pattern `CREDENTIAL_{SERVICE}_{FIELD}`:

```python
import os
gmail_user = os.environ['CREDENTIAL_GMAIL_SMTP_USERNAME']
gmail_pass = os.environ['CREDENTIAL_GMAIL_SMTP_APP_PASSWORD']
```

{% hint style="info" %}
You never need to hardcode credentials. The platform handles injection automatically. If you see a credential value in a script, it should be replaced with an environment variable reference.
{% endhint %}

## Managing Credentials

All stored credentials are listed in **Settings → Credentials**. From there you can:
- See which credentials exist (names and services only — values are never shown)
- Delete credentials you no longer need
- Add new credentials

To update a credential (e.g. rotate an API key):

> "Update the Jira credentials — I have a new API token."

The platform will open a new secure form. The old value is replaced.

## Frequently Asked Questions

<details>
<summary>Can I see my stored credential values?</summary>
No. Once a credential is saved, its value is never shown again — not in the UI, not in chat, not in logs. This is by design. If you need to verify a credential, test it by running an agent or workflow that uses it.
</details>

<details>
<summary>What if my API key expires or is rotated?</summary>
Update the credential through conversation: "Update my Jira API token — I have a new one." The platform opens a secure form and replaces the old value. All agents and workflows using that credential will automatically use the new value.
</details>

<details>
<summary>Are credentials shared across my whole organization?</summary>
Yes. Credentials are org-wide. Any agent or workflow in your organization can use any stored credential. This means you only need to store a credential once, even if multiple agents use it.
</details>
