---
icon: question
---

# Getting Started FAQ

{% hint style="success" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


New to WorkflowFiesta? Here are the most common questions from people just getting started.

{% hint style="info" %}
**Can't find your answer here?** Join our [Discord community](https://discord.gg/XEKxARDkNQ) — the team and community are active and happy to help.
{% endhint %}

## General

<details>

<summary>What is WorkflowFiesta?</summary>

WorkflowFiesta is a conversational AI automation platform. You build AI agents, reusable skills, and automated workflows by talking — no code, no configuration files, no technical setup required.

You describe what you want to automate. WorkflowFiesta asks clarifying questions, confirms the design, and builds it for you.

</details>

<details>

<summary>Do I need to know how to code?</summary>

No. WorkflowFiesta is designed for non-technical business users. Everything is created through conversation. You describe what you want, and the platform builds it.

If you are technical, you can go deeper — but it's never required.

</details>

<details>

<summary>What's the difference between an agent, a skill, and a workflow?</summary>

* **Agent** — An AI assistant you design for a specific purpose. It has a name, a role, and a set of instructions. You talk to it directly.
* **Skill** — A reusable building block that makes an agent's behavior consistent. Skills are shared across your entire organization.
* **Workflow** — An automated pipeline that runs on a schedule or trigger, without you being present. It can call agents, connect to external services, send emails, and more.

</details>

<details>

<summary>How do I create my first agent?</summary>

Just describe what you want the agent to do:

> _"Create an agent that helps me write marketing copy for WorkflowFiesta."_

WorkflowFiesta will ask a few questions and create the agent. You can start talking to it immediately.

See the [Quickstart guide](../../get-started/quickstart.md) for a step-by-step walkthrough.

</details>

<details>

<summary>How do I connect an external service like Jira or Slack?</summary>

Tell WorkflowFiesta which service you want to connect:

> _"I want to connect Jira."_

It will tell you exactly where to find your API key or token, open a secure form for you to paste it into, and save it encrypted. Your credentials are never exposed after that.

See [Credentials](../../documentation/credentials.md) for more detail.

</details>

<details>

<summary>Can I use my own AI model?</summary>

Yes. WorkflowFiesta supports OpenAI, Anthropic, AWS Bedrock, Google Gemini, Ollama (local models), Azure OpenAI, and any other provider with an API. You connect your own API key and choose which model each agent uses.

See [Models & Providers](../../documentation/models.md) for the full list.

</details>

<details>

<summary>What is the Runner?</summary>

The Runner is a lightweight app you install on your own computer or server. Once connected, your agents can access local files, internal systems, and private networks — things that aren't accessible from the cloud.

It's optional. You only need it if your workflows need to touch files or systems on your own machine.

See [Install the Runner](../../documentation/runner.md) for setup instructions.

</details>

<details>

<summary>Is my data secure?</summary>

Yes. Credentials are encrypted at rest and never exposed after saving. Conversation data is not used to train AI models. The Runner runs on your own infrastructure and only communicates outbound to the WorkflowFiesta platform.

</details>
