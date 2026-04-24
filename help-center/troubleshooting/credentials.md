---
icon: square-question
---

# Troubleshooting Credentials

{% hint style="info" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


Credential issues are the most common cause of workflow failures. Here's how to diagnose and fix them.

## Adding credentials

<details>

<summary>I don't know where to find my API key</summary>

Tell WorkflowFiesta which service you're trying to connect and it will give you exact instructions:

> _"Where do I find my Intercom API key?"_

For common services:

* **Intercom** — Settings → Developers → Developer Hub → Authentication → Access Token
* **Jira** — Account Settings → Security → API tokens → Create API token
* **GitHub** — Settings → Developer settings → Personal access tokens → Tokens (classic)
* **Google Analytics** — Google Cloud Console → APIs & Services → Credentials
* **Slack** — api.slack.com → Your Apps → OAuth & Permissions → Bot Token

</details>

<details>

<summary>The credential form isn't appearing</summary>

The secure credential form appears in the chat when WorkflowFiesta needs a credential. If it's not appearing:

1. Make sure you're asking WorkflowFiesta to connect a specific named service (e.g., "connect Jira" not just "add a credential")
2. Try refreshing the page and asking again
3. Check that your browser isn't blocking pop-ups or modals

</details>

## Credential errors in workflows

<details>

<summary>A workflow fails with "credential invalid" or "unauthorized"</summary>

This means the stored credential is no longer valid. API keys can expire, be rotated, or be revoked by the external service.

**Fix:**

1. Go to **Settings → Credentials**
2. Find the credential for the failing service
3. Delete it
4. Ask WorkflowFiesta to re-add it: _"I need to reconnect my Jira credential."_

</details>

<details>

<summary>My OAuth connection stopped working</summary>

OAuth tokens expire and need to be refreshed. WorkflowFiesta handles token refresh automatically for most OAuth providers, but sometimes the refresh token itself expires (usually after 6 months of inactivity).

**Fix:** Reconnect the OAuth service. Tell WorkflowFiesta:

> _"My Google connection isn't working — can you reconnect it?"_

It will open the OAuth authorization screen and you'll re-approve access.

</details>

<details>

<summary>The credential works when I test it but fails in the workflow</summary>

This usually means the credential has the right access for some actions but not others. For example, a GitHub token with only `read` scope will fail when a workflow tries to create a PR.

**Fix:** Check the permission scopes on your credential in the external service and ensure they match what the workflow needs. WorkflowFiesta will tell you which scopes are required when you ask it to connect a service.

</details>

## Security

<details>

<summary>Can I see my stored credentials?</summary>

No. Credentials are encrypted after saving and cannot be read back — not by you, not by the WorkflowFiesta team. This is by design. If you need to update a credential, delete it and re-add it.

</details>

<details>

<summary>I accidentally pasted a credential into the chat</summary>

WorkflowFiesta automatically detects credentials pasted into chat and sanitizes the message immediately. The value is masked in the conversation log. However, you should still rotate the credential in the external service as a precaution.

</details>

{% hint style="info" %}
**Still stuck?** Ask WorkflowFiesta directly — describe which service is failing and it will diagnose the issue. Or join the [Discord community](https://discord.gg/XEKxARDkNQ).
{% endhint %}
