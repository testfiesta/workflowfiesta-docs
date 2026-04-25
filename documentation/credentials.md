---
icon: key
---

# Credentials

{% hint style="success" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


Credentials are the API keys, passwords, and tokens that WorkflowFiesta uses to connect to your external tools and services — things like your CRM, email provider, analytics platform, or any third-party API.

They are stored encrypted and never exposed. Once saved, a credential is referenced by name — no one ever sees the actual value again, including you.

{% hint style="danger" %}
**Never paste credentials into a chat message.** WorkflowFiesta will always open a secure form to collect sensitive values. If you are ever asked to type a key or password directly into a conversation, do not do it.
{% endhint %}

## How credentials work

When you ask WorkflowFiesta to connect to a new tool, it will guide you through the process:

1. **You describe the connection** — "I want to connect to Intercom"
2. **WorkflowFiesta tells you what it needs** — "I will need your Intercom API key. You can find it in your Intercom settings under Developer Hub → Authentication."
3. **A secure form appears in the chat** — you enter the value directly into the form
4. **The credential is saved and encrypted** — WorkflowFiesta confirms it is stored
5. **Your agents and workflows can now use it** — referenced by name, never by value

You never need to manage this manually. WorkflowFiesta handles the entire process through conversation.

## OAuth connections

For services that support OAuth — like Google, GitHub, Slack, HubSpot, and others — WorkflowFiesta opens the provider's own login screen in your browser. You authorize the connection there, and WorkflowFiesta stores the token securely. You never handle a token directly.

Supported OAuth providers include Google, Microsoft, GitHub, GitLab, Slack, Discord, Notion, Linear, HubSpot, Salesforce, Stripe, Airtable, Intercom, Zendesk, and more.

## Security

{% tabs %}
{% tab title="Encryption" %}
All credentials are encrypted at rest using industry-standard encryption. The raw value is never stored in plain text and is never logged.
{% endtab %}

{% tab title="Access" %}
Credentials are scoped to your organization. Only agents and workflows within your org can use them — and only when explicitly authorized to do so.
{% endtab %}

{% tab title="Exposure" %}
Credential values are never shown in chat, never included in logs, and never visible after the initial save. If a credential needs to be rotated, you save a new value and the old one is replaced.
{% endtab %}
{% endtabs %}

## Managing credentials

All saved credentials are listed in **Settings → Credentials**. From there you can:

* See which services are connected
* Add new credentials
* Rotate or replace existing ones
* Delete credentials that are no longer needed

You can also ask WorkflowFiesta directly: _"What credentials do I have saved?"_ or _"Connect my SendGrid account"_ — and it will handle everything through conversation.

## Common integrations

| Service      | What it enables                                                           |
| ------------ | ------------------------------------------------------------------------- |
| **Google**   | Gmail, Google Analytics, Google Ads, Google Drive, Calendar               |
| **GitHub**   | Read repos, manage PRs, trigger Actions, push code                        |
| **Jira**     | Create and update tickets, query sprints, manage boards                   |
| **Slack**    | Send messages, read channels, post summaries                              |
| **HubSpot**  | Read and write CRM contacts, deals, and companies                         |
| **Intercom** | Pull user data, send messages, read conversations                         |
| **Stripe**   | Read billing data, subscriptions, and invoices                            |
| **SendGrid** | Send transactional and marketing email                                    |
| **Any API**  | If a service has an API and issues keys, WorkflowFiesta can connect to it |
