---
icon: square-question
---

# Troubleshooting Workflows

{% hint style="info" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


Having trouble with a workflow? Here are the most common issues and how to fix them.

## Workflow isn't triggering

<details>

<summary>My scheduled workflow didn't run at the expected time</summary>

**Check the workflow status first.** A workflow must be set to **Active** to run on a schedule. If it's in **Draft** status, it won't trigger automatically.

To check: open the workflow in the **Workflows** tab and confirm the status shows Active.

**Check the timezone.** Schedules run in UTC by default. If you set a workflow to run at "9am" and it's running at the wrong time, confirm whether the schedule was set in your local timezone or UTC.

**Ask WorkflowFiesta to check it:**

> _"Why didn't my weekly report workflow run this morning?"_

</details>

<details>

<summary>My webhook-triggered workflow isn't firing</summary>

**Confirm the webhook URL is correct.** Copy the webhook URL from the workflow settings and paste it into the external service again — a single character difference will cause it to fail silently.

**Check that the external service is actually sending the event.** Most services (GitHub, Stripe, HubSpot) have a webhook delivery log where you can see whether the event was sent and what response it received.

**Check for authentication.** Some webhook sources require a secret token to be included in the request. If your workflow expects a token and the sender isn't including it, the request will be rejected.

</details>

## Workflow runs but produces wrong output

<details>

<summary>An agent step returned an unexpected result</summary>

Open the run log for the workflow (in the **Workflows** tab → select the run) and look at the output of each step. The run log shows exactly what each agent received as input and what it returned.

If the agent's output looks wrong, the issue is usually in the prompt or the input data — not the workflow itself. Try talking to the agent directly with the same input to debug it in isolation.

</details>

<details>

<summary>A step says it succeeded but nothing happened</summary>

Some integrations (email sends, Slack messages, Jira ticket creation) succeed from the workflow's perspective even if the downstream action had an issue. Check:

* **Email:** Check your sent folder and spam. Verify the recipient address is correct.
* **Jira:** Check that the credential used has permission to create issues in the target project.
* **Slack:** Confirm the bot has been invited to the channel it's posting to.

</details>

## Workflow fails with an error

<details>

<summary>A step failed — how do I find out why?</summary>

Open the **Workflows** tab, find the failed run, and click into it. Each step shows its status, and failed steps show the error message. The error message usually tells you exactly what went wrong.

Common errors:

* **Credential expired or invalid** — the API key for a connected service has been rotated or revoked. Re-add the credential.
* **Rate limit exceeded** — the external service rejected the request because too many calls were made. The workflow will succeed if you run it again after a short wait.
* **Timeout** — a step took too long to complete. This can happen with large data pulls. Ask WorkflowFiesta to break the step into smaller chunks.

</details>

<details>

<summary>The workflow keeps failing on the same step</summary>

If a specific step fails consistently, it's usually one of three things:

1. **Invalid credential** — the API key or token for that service is expired or incorrect. Go to **Settings → Credentials**, delete the old credential, and re-add it.
2. **Permission issue** — the credential doesn't have the right permissions for the action being taken. Check the service's permission settings.
3. **Data issue** — the input to that step is malformed or missing. Check the output of the previous step in the run log.

</details>

{% hint style="info" %}
**Still stuck?** Describe the issue in the chat and WorkflowFiesta will diagnose it for you. Or join the [Discord community](https://discord.gg/XEKxARDkNQ) for help from the team.
{% endhint %}
