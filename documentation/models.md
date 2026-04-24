---
icon: openai
---

# Models & Providers

{% hint style="info" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


WorkflowFiesta is model-agnostic. You can connect any AI model from any provider — and switch between them at any time, for any agent, without rebuilding anything.

{% hint style="success" %}
**No lock-in.** If a provider raises prices, releases a better model, or you simply want to try something new, you swap it in through conversation. Your agents, skills, and workflows stay exactly as they are.
{% endhint %}

## How it works

Each agent in WorkflowFiesta runs on a model you choose. You can assign different models to different agents — your coding agent might use one model, your writing agent another, your analytics agent a third.

To connect a model or switch providers, just tell WorkflowFiesta:

> _"Switch my marketing agent to GPT-4o"_ _"Connect my Anthropic API key"_ _"Use Claude Sonnet for all new agents by default"_

WorkflowFiesta will guide you through adding credentials for that provider if needed, then apply the change.

## Supported providers

{% tabs %}
{% tab title="Anthropic" %}
**Models:** Claude Opus, Claude Sonnet, Claude Haiku

Strong at reasoning, writing, and following complex instructions. Excellent for content pipelines, analysis, and multi-step tasks.
{% endtab %}

{% tab title="OpenAI" %}
**Models:** GPT-4o, GPT-4 Turbo, GPT-3.5 Turbo, o1, o3

Industry-standard models with broad capability. Strong at code, structured output, and tool use.
{% endtab %}

{% tab title="AWS Bedrock" %}
**Models:** Claude (via Bedrock), Llama, Titan, Mistral, and others

Run models inside your own AWS infrastructure. Preferred for teams with data residency or compliance requirements.
{% endtab %}

{% tab title="Ollama" %}
**Models:** Llama 3, Mistral, Gemma, Phi, and any model you pull locally

Run models entirely on your own hardware. No data leaves your machine. Ideal for sensitive workloads or air-gapped environments.
{% endtab %}

{% tab title="Google" %}
**Models:** Gemini Pro, Gemini Flash, Gemini Ultra

Google's latest generation models. Strong at multimodal tasks and long-context reasoning.
{% endtab %}

{% tab title="Any provider" %}
If a model provider offers an API, WorkflowFiesta can connect to it. This includes Azure OpenAI, Mistral AI, Cohere, Together AI, Groq, and any other provider with a compatible API endpoint.

Ask WorkflowFiesta: _"Can you connect to \[provider]?"_ and it will walk you through the setup.
{% endtab %}
{% endtabs %}

## Bring your own API key

WorkflowFiesta does not mark up model costs. You connect your own API keys directly to the providers you use. You pay the provider directly at their published rates — WorkflowFiesta charges for the platform, not for model tokens.

To add a model API key:

1. Tell WorkflowFiesta which provider you want to connect
2. A secure form will appear — enter your API key
3. Choose which agents or workflows should use that provider
4. Done — your agents now run on your own model budget

## Choosing a model

| Need                               | Recommended                                     |
| ---------------------------------- | ----------------------------------------------- |
| Best reasoning and writing quality | Claude Opus or GPT-4o                           |
| Fast, high-volume tasks            | Claude Haiku or GPT-3.5 Turbo                   |
| Code generation and tool use       | GPT-4o or Claude Sonnet                         |
| Data privacy / on-premise          | Ollama (local) or AWS Bedrock                   |
| Long documents and context         | Gemini Pro or Claude Sonnet                     |
| Cost-sensitive workloads           | Claude Haiku, Gemini Flash, or Llama via Ollama |

## Managing models

All connected model providers are listed in **Settings → Models**. From there you can see which providers are active, which agents use which models, and add or remove providers at any time.
