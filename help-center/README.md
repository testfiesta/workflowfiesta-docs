---
icon: house-chimney-medical
---

# Help Center Home

Find answers to common questions, troubleshoot issues, and get your workflows running smoothly.

{% hint style="info" %}
**Can't find what you need?** [Join the Discord](https://discord.gg/XEKxARDkNQ) — the community and team are active there.
{% endhint %}

***

## Browse by Topic

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>🚀 <strong>Getting Started FAQ</strong></td><td>Common questions from new users</td><td><a href="faq/getting-started.md">getting-started.md</a></td></tr><tr><td>⚙️ <strong>Troubleshooting Workflows</strong></td><td>Workflow not running? Start here.</td><td><a href="troubleshooting/workflows.md">workflows.md</a></td></tr><tr><td>🖥️ <strong>Troubleshooting the Runner</strong></td><td>Runner not connecting or going offline</td><td><a href="troubleshooting/runner.md">runner.md</a></td></tr><tr><td>🔑 <strong>Troubleshooting Credentials</strong></td><td>API key errors and authentication issues</td><td><a href="troubleshooting/credentials.md">credentials.md</a></td></tr><tr><td>🤖 <strong>Troubleshooting Models</strong></td><td>Model errors, rate limits, and provider issues</td><td><a href="troubleshooting/models.md">models.md</a></td></tr><tr><td>💳 <strong>Billing &#x26; Account</strong></td><td>Plans, invoices, and account settings</td><td><a href="account/billing.md">billing.md</a></td></tr><tr><td>👥 <strong>Team &#x26; Permissions</strong></td><td>Invite team members and manage roles</td><td><a href="account/team-permissions.md">team-permissions.md</a></td></tr></tbody></table>

***

## Quick Answers

<details>

<summary>How do I create my first agent?</summary>

Go to **Agents** in the left sidebar → click **New Agent** → give it a name and a system prompt → click **Save**. Your agent is live immediately. See the [Quickstart](../documentation/getting-started/quickstart.md) for a full walkthrough.

</details>

<details>

<summary>What is the Runner and do I need it?</summary>

The Runner is a lightweight binary you install on your own machine. It lets WorkflowFiesta run scripts directly on your computer — reading local files, accessing internal systems, and using local tools. You don't need it to get started. You need it if you want to access files or systems that aren't on the public internet.

</details>

<details>

<summary>Can I use my own OpenAI or Anthropic API key?</summary>

Yes. Go to **Settings → Models** and add your API key. WorkflowFiesta supports OpenAI, Anthropic, and AWS Bedrock. You can switch models at any time — you're never locked in.

</details>

<details>

<summary>How do I invite my team?</summary>

Go to **Settings → Team** → click **Invite Member** → enter their email. They'll receive an invitation to join your organization. See [Team & Permissions](account/team-permissions.md) for role details.

</details>

<details>

<summary>Where are my credentials stored?</summary>

Credentials are encrypted at rest and never exposed in logs or chat. They're stored in WorkflowFiesta's credential store and injected into workflow steps at runtime via environment variables. You can manage them at **Settings → Credentials**.

</details>
