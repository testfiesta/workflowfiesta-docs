---
icon: computer
---

# Runner

{% hint style="info" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


The WorkflowFiesta Runner is a lightweight app you install on your computer or server. Once connected, your agents can access local files, internal databases, and systems behind your firewall.

{% hint style="info" %}
**The Runner is optional.** You only need it if you want agents to work with files or systems on your local machine or internal network.
{% endhint %}

## What the Runner Enables

| Capability                | Example                                         |
| ------------------------- | ----------------------------------------------- |
| Read local files          | "Summarize all the PDFs in my Downloads folder" |
| Write local files         | "Save this report to my Desktop"                |
| Access internal databases | "Query our internal Postgres database"          |
| Run local scripts         | "Run the analytics script in my git repo"       |
| Work behind a firewall    | Access systems on your company network          |

## How It Works

The Runner connects outbound over HTTPS. No inbound ports, no firewall changes needed.

## Installing the Runner

Ask WorkflowFiesta through conversation:

> "I want to install a runner on my laptop."

The platform will ask what you want to name it, generate a registration code, and give you a one-click setup link.

{% tabs %}
{% tab title="macOS" %}
1. Download the Runner from the WorkflowFiesta releases page
2. Open the app and paste your registration code
3. Click **Connect**
{% endtab %}

{% tab title="Linux" %}
```bash
curl -L https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-linux-amd64 -o wf-runner
chmod +x wf-runner
./wf-runner --code YOUR_REGISTRATION_CODE
```
{% endtab %}

{% tab title="Windows" %}
1. Download the Runner `.exe` from the WorkflowFiesta releases page
2. Run the installer and paste your registration code
{% endtab %}
{% endtabs %}

## Security

{% hint style="warning" %}
**The Runner executes code on your machine.** Only connect runners to WorkflowFiesta organizations you control.
{% endhint %}

* Connects outbound only — no inbound ports opened
* All communication encrypted over HTTPS
* Registration codes are one-time tokens

## Troubleshooting

<details>

<summary>My runner shows as offline</summary>

The runner process may have stopped. Restart the Runner app. On Linux, run \`systemctl restart workflowfiesta-runner\`.

</details>

<details>

<summary>I need a new registration code</summary>

Ask WorkflowFiesta: "Generate a new runner registration code." The old code is revoked and a new one issued immediately.

</details>
