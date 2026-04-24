# DevOps

DevOps teams manage infrastructure, deployments, monitoring, and incident response. WorkflowFiesta automates the repetitive operational work so your engineers can focus on building.

## What DevOps teams automate with WorkflowFiesta

{% tabs %}
{% tab title="Deployments" %}
**Automate your release pipeline end to end.**

- Trigger deployments from a GitHub merge or manual command
- Run pre-deployment checks and notify the team
- Monitor rollout progress and alert on failures
- Automatically roll back if health checks fail

> *"When a PR is merged to main, run the deployment pipeline, monitor for errors, and post a status update to Slack."*
{% endtab %}

{% tab title="Monitoring" %}
**Get alerted on what matters, not everything.**

- Monitor infrastructure health on a schedule
- Summarize error logs and surface the most critical issues
- Correlate alerts across multiple systems
- Escalate to the on-call engineer when thresholds are breached

> *"Every hour, check our error rate. If it exceeds 1%, page the on-call engineer and post a summary to #incidents."*
{% endtab %}

{% tab title="Incident Response" %}
**Respond faster with automated triage.**

- Create incident channels and assign roles automatically
- Pull relevant logs and metrics when an incident is declared
- Draft status page updates based on what's known
- Generate post-mortem templates after resolution

> *"When an incident is declared, create a Slack channel, pull the last hour of error logs, and draft an initial status update."*
{% endtab %}

{% tab title="Reporting" %}
**Weekly engineering health reports without manual work.**

- Track deployment frequency, lead time, and failure rate
- Summarize open PRs, blocked issues, and tech debt
- Report on infrastructure costs and anomalies
- Email the engineering digest to leadership on Fridays

> *"Every Friday, pull our deployment metrics from GitHub Actions and infrastructure costs from AWS, and email a summary to the CTO."*
{% endtab %}
{% endtabs %}

## Getting started

Tell WorkflowFiesta what DevOps process you want to automate. It will ask about your CI/CD setup, cloud provider, and alerting tools — then build the workflow.

{% hint style="info" %}
**Install the Runner** on your infrastructure if you need agents to access internal systems, private networks, or local files. [Learn more about the Runner.](../../documentation/workflowfiesta/runner.md)
{% endhint %}

{% content-ref url="../README.md" %}
[Back to Guides](../README.md)
{% endcontent-ref %}
