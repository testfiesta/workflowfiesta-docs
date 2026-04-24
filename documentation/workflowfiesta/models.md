# Models & Providers

WorkflowFiesta is model-agnostic. You can connect any AI model from any provider — and switch between them at any time without rebuilding your agents or workflows.

{% hint style="success" %}
**No lock-in.** Your agents, skills, and workflows are independent of the model powering them. Swap providers in seconds.
{% endhint %}

## Supported providers

WorkflowFiesta works with every major AI model provider, including:

| Provider | Models |
|----------|--------|
| **Anthropic** | Claude 3.5 Sonnet, Claude 3 Opus, Claude 3 Haiku, and all Claude variants |
| **OpenAI** | GPT-4o, GPT-4 Turbo, GPT-3.5 Turbo, o1, o1-mini, and all GPT variants |
| **AWS Bedrock** | All Bedrock-hosted models including Llama, Mistral, Titan, and more |
| **Google** | Gemini Pro, Gemini Flash, Gemini Ultra |
| **Ollama** | Any locally-hosted model via Ollama (Llama 3, Mistral, Phi, Gemma, etc.) |
| **Azure OpenAI** | All Azure-hosted OpenAI models |
| **Any other provider** | If it has an API, WorkflowFiesta can connect to it |

## How to connect a model

Tell WorkflowFiesta which provider you want to connect:

> *"I want to connect my OpenAI API key."*

WorkflowFiesta will:
1. Open a secure credential form
2. You paste your API key — it's encrypted immediately
3. The model is available to all your agents

You can connect multiple providers simultaneously and choose which model each agent uses.

## Choosing a model for an agent

Each agent can be configured to use a specific model. When creating or editing an agent, just tell WorkflowFiesta which model you want it to use:

> *"Use Claude 3.5 Sonnet for this agent."*
> *"Switch the report agent to GPT-4o."*

## Bring your own model (BYOM)

If your organization has its own model infrastructure — whether self-hosted, fine-tuned, or accessed through a private endpoint — WorkflowFiesta can connect to it. Just provide the API endpoint and credentials.

## Why model flexibility matters

Different models have different strengths. You might use:
- A fast, cost-efficient model for high-volume tasks like email triage
- A more capable model for complex reasoning like strategy analysis
- A locally-hosted model for sensitive data that shouldn't leave your network

WorkflowFiesta lets you match the right model to the right task — and change your mind whenever you need to.

{% content-ref url="agents.md" %}
[Configure models on agents](agents.md)
{% endcontent-ref %}

{% content-ref url="credentials.md" %}
[Connect your API keys](credentials.md)
{% endcontent-ref %}
