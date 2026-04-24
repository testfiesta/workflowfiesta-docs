# Credentials

Credentials are how WorkflowFiesta connects to external services on your behalf — securely, without ever exposing your API keys or passwords.

{% hint style="success" %}
**Credentials are encrypted and never exposed.** Once saved, your credentials are stored securely and injected into workflows at runtime. No one — including you — can read them back out of the platform.
{% endhint %}

## How credentials work

When a workflow or agent needs to connect to an external service (Intercom, Jira, Slack, Google Analytics, etc.), it uses a stored credential. You provide the credential once through a secure form, and WorkflowFiesta handles the rest automatically.

You never paste API keys into chat messages or workflow configurations. The platform opens a secure form, you fill it in, and it's encrypted and saved.

## How to add a credential

Just tell WorkflowFiesta what you want to connect:

> *"I want to connect to Intercom."*

WorkflowFiesta will:
1. Tell you exactly where to find the API key or token in that service
2. Open a secure credential form in the chat
3. You paste the value into the form — it's masked immediately
4. WorkflowFiesta saves it encrypted and confirms it's ready to use

That credential is then available to any workflow or agent in your organization.

## Credential types

{% tabs %}
{% tab title="API Keys & Tokens" %}
The most common type. A secret key provided by an external service that grants access to its API.

**Examples:** Intercom API token, Google Analytics API key, Jira API token, GitHub personal access token, OpenAI API key

WorkflowFiesta will tell you exactly where to find each key in the external service's settings.
{% endtab %}

{% tab title="Username & Password" %}
For services that use traditional login credentials — typically email delivery services or legacy systems.

**Examples:** Gmail SMTP (email + app password), Outlook SMTP

{% hint style="warning" %}
For Gmail, use an **App Password** rather than your regular account password. WorkflowFiesta will guide you through generating one.
{% endhint %}
{% endtab %}

{% tab title="OAuth" %}
For services that use OAuth — you authorize WorkflowFiesta through the service's own login screen rather than providing a key manually.

**Examples:** Google (Gmail, Calendar, Drive), GitHub, Slack, Discord, HubSpot, Salesforce, Notion, Linear, and many more.

WorkflowFiesta opens the provider's authorization screen in a new tab. You log in and approve access. No keys to copy or paste.
{% endtab %}
{% endtabs %}

## Supported integrations

WorkflowFiesta can connect to virtually any service with an API. Common integrations include:

| Category | Services |
|----------|----------|
| **Communication** | Gmail, Outlook, Slack, Discord, Microsoft Teams |
| **Project Management** | Jira, Linear, Asana, Notion, Monday |
| **Analytics** | Google Analytics, Intercom, Mixpanel |
| **Advertising** | Google Ads, Meta Ads |
| **CRM & Sales** | HubSpot, Salesforce, Pipedrive |
| **Development** | GitHub, GitLab, Bitbucket |
| **Cloud Storage** | Google Drive, Dropbox, Box |
| **AI Models** | OpenAI, Anthropic, AWS Bedrock, Ollama, and more |
| **Billing** | Stripe |
| **Documentation** | GitBook, Confluence |

If the service you need isn't listed, ask WorkflowFiesta — if it has an API, it can likely be connected.

## Managing credentials

All saved credentials are visible in **Settings → Credentials**. You can see which services are connected, delete credentials you no longer need, and add new ones at any time.

{% hint style="danger" %}
**Never paste credentials into a chat message.** Always use the secure credential form. WorkflowFiesta will automatically prompt you to use the form whenever a credential is needed.
{% endhint %}

{% content-ref url="workflows.md" %}
[Use credentials in workflows](workflows.md)
{% endcontent-ref %}
