---
icon: square-question
---

# Troubleshooting Models

{% hint style="success" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


Issues connecting or using AI model providers? Here's how to fix the most common problems.

## Connecting a model provider

<details>

<summary>I added my API key but the model isn't available</summary>

After adding a model API key, you may need to specify which model you want an agent to use. Tell WorkflowFiesta:

> _"Set my agent to use GPT-4o."_ _"Use Claude 3.5 Sonnet for this agent."_

If the model still isn't available, verify the API key has the correct permissions in the provider's dashboard.

</details>

<details>

<summary>Where do I find my API key for each provider?</summary>

| Provider          | Where to find your API key                              |
| ----------------- | ------------------------------------------------------- |
| **OpenAI**        | platform.openai.com → API keys                          |
| **Anthropic**     | console.anthropic.com → API Keys                        |
| **AWS Bedrock**   | AWS Console → IAM → Access keys                         |
| **Google Gemini** | Google AI Studio → Get API key                          |
| **Azure OpenAI**  | Azure Portal → Your OpenAI resource → Keys and Endpoint |
| **Ollama**        | No key needed — just the local endpoint URL             |

</details>

## Model errors during runs

<details>

<summary>I'm getting "rate limit exceeded" errors</summary>

Rate limits are set by the model provider, not WorkflowFiesta. Each provider has different limits based on your plan tier.

**Short-term fix:** Wait a few minutes and retry. Most rate limits reset within 60 seconds to a few minutes.

**Long-term fix:** Upgrade your plan with the provider, or distribute load across multiple providers. WorkflowFiesta supports connecting multiple providers simultaneously.

</details>

<details>

<summary>The model is returning low-quality or unexpected responses</summary>

This is usually an agent configuration issue, not a model issue. The model responds to what it's given — if the output is wrong, the instructions or context are likely the cause.

Try:

1. Ask WorkflowFiesta to review the agent's system prompt: _"Review my agent's instructions and suggest improvements."_
2. Test with a different model to see if the issue is model-specific
3. Add more specific instructions to the agent about the format or style of response you want

</details>

<details>

<summary>My Ollama (local) model isn't connecting</summary>

Ollama runs on your local machine and requires the Runner to be installed and connected. Without the Runner, WorkflowFiesta can't reach your local Ollama instance.

**Steps:**

1. Ensure the Runner is installed and showing as Connected in **Settings → Runners**
2. Ensure Ollama is running locally (`ollama serve`)
3. Tell WorkflowFiesta the Ollama endpoint: typically `http://localhost:11434`

See [Install the Runner](../../documentation/runner.md) for Runner setup.

</details>

## Costs and usage

<details>

<summary>How do I control AI spending?</summary>

WorkflowFiesta lets you set spend limits at the org, user, workflow, or agent level. When a limit is reached, runs are paused until the period resets or the limit is raised.

To set a limit, tell WorkflowFiesta:

> _"Set a monthly spend limit of $50 for my org."_ _"Limit the report workflow to $10 per month."_

You can also view a cost breakdown by model, workflow, agent, or user in the platform.

</details>

{% hint style="info" %}
**Still stuck?** Ask WorkflowFiesta directly or join the [Discord community](https://discord.gg/XEKxARDkNQ).
{% endhint %}
