---
icon: openai
---

# Models & Providers

WorkflowFiesta is model-agnostic. You connect your own AI model API keys and choose which model powers each agent. Switch models at any time without rebuilding anything.

{% hint style="success" %}
**Bring your own model.** WorkflowFiesta never locks you into one AI provider. Connect OpenAI, Anthropic, AWS Bedrock, or any supported provider — and switch between them freely.
{% endhint %}

## Supported Providers

| Provider        | Models                                           |
| --------------- | ------------------------------------------------ |
| **Anthropic**   | Claude 3.5 Sonnet, Claude 3 Opus, Claude 3 Haiku |
| **OpenAI**      | GPT-4o, GPT-4 Turbo, GPT-3.5 Turbo               |
| **AWS Bedrock** | Claude via Bedrock, Llama, Titan, and others     |
| **Ollama**      | Any locally-hosted model                         |

## Connecting a Model Provider

Ask WorkflowFiesta through conversation:

> "I want to connect my OpenAI API key."

> "Set up Anthropic as my model provider."

> "Connect AWS Bedrock using my IAM credentials."

The platform will open a secure form to collect your API key or credentials. They are encrypted and stored — never visible again after saving.

## Setting a Model for an Agent

Each agent can use a different model:

> "Set the Research Agent to use Claude 3.5 Sonnet."

> "Switch the Code Review Agent to GPT-4o."

> "Use the cheapest available model for the Email Formatter Agent."

## Default Model

If no model is specified for an agent, it uses the organization's default model. Set the default through conversation:

> "Set Claude 3.5 Sonnet as the default model for all agents."

## Model Selection Tips

| Use case                          | Recommended model               |
| --------------------------------- | ------------------------------- |
| Complex reasoning, long documents | Claude 3.5 Sonnet or GPT-4o     |
| Fast, high-volume tasks           | Claude 3 Haiku or GPT-3.5 Turbo |
| Code generation and review        | GPT-4o or Claude 3.5 Sonnet     |
| Cost-sensitive workflows          | Claude 3 Haiku                  |

## Temperature

Temperature controls how creative vs. precise an agent's responses are. Set it when creating or updating an agent:

* **0.0–0.3** — Precise, consistent, factual (good for data extraction, classification)
* **0.4–0.7** — Balanced (good for most tasks)
* **0.8–1.5** — Creative, varied (good for brainstorming, copywriting)

> "Set the Creative Writing Agent's temperature to 1.2."

> "Make the Data Extraction Agent more precise — set temperature to 0.1."
