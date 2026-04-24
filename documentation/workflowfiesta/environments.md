# Environments

An environment defines where your workflow scripts run — the container image, environment variables, and which runner (if any) to use.

{% hint style="info" %}
Most users never need to configure environments manually. WorkflowFiesta sets up a default environment automatically. You only need to customize this if you need a specific runtime, custom dependencies, or want scripts to run on your local machine.
{% endhint %}

## What Is an Environment?

When a workflow runs a script step, it needs somewhere to execute. That somewhere is an environment. An environment specifies:

| Property | What it controls |
|---|---|
| **Docker image** | The base runtime (Python, Node.js, Debian, etc.) |
| **Environment variables** | Values injected into every script that runs here |
| **Runner** | Whether scripts run in the cloud or on your local machine |
| **Runner selection** | If multiple runners are attached, how to pick one |

## Default Environment

WorkflowFiesta provides a default cloud environment with:
- Debian Linux base image
- Python 3, Node.js, curl, git, jq, AWS CLI pre-installed
- Outbound internet access
- No local file access

This is sufficient for most workflows that call external APIs, process data, or send notifications.

## Creating a Custom Environment

Ask WorkflowFiesta through conversation:

> "Create an environment that uses Python 3.11 and has my database connection string available."

> "Set up an environment that runs scripts on my local machine."

The platform will ask what you need and configure it.

## Attaching a Runner

To run scripts on your local machine instead of in the cloud, attach your Runner to an environment:

> "Attach my local runner to the default environment."

Once attached, any workflow step using that environment will execute on your machine.

See [Runner](runner.md) for how to install and connect a runner.

## Environment Variables

Environment variables are injected into every script that runs in the environment. Use them for:
- Database connection strings
- API base URLs
- Configuration values that change between environments

{% hint style="danger" %}
**Do not store secrets as environment variables.** Use [Credentials](credentials.md) instead. Credentials are encrypted. Environment variables are not.
{% endhint %}
