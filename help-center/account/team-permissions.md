# Team & Permissions

## Roles

WorkflowFiesta has three roles. Every member of your organization is assigned one.

| Role | What they can do |
|------|-----------------|
| **Admin** | Full access — create, edit, and delete all resources. Manage team members, billing, and org settings. |
| **Member** | Create and use agents, skills, and workflows. Cannot manage team members or billing. |
| **Viewer** | Read-only access — can view agents, workflows, and run history but cannot create or modify anything. |

## Inviting team members

To invite someone to your organization:

1. Go to **Settings → Team**
2. Click **Invite member**
3. Enter their email address and select their role
4. They'll receive an email invitation with a link to join

Or ask WorkflowFiesta:
> *"Invite sarah@company.com as a Member."*

## Changing a member's role

Admins can change any member's role at any time from **Settings → Team**. Select the member and choose a new role from the dropdown.

## Removing a member

To remove someone from your organization, go to **Settings → Team**, find the member, and click **Remove**. Their access is revoked immediately.

{% hint style="warning" %}
Removing a member does not delete the agents, workflows, or credentials they created. Those resources remain in the organization and are accessible to other Admins.
{% endhint %}

## Org-wide resources

All agents, skills, workflows, and credentials in WorkflowFiesta are **org-wide** — they are shared across your entire organization, not owned by individual users. Any Member or Admin can use any agent or workflow.

This means:
- Skills built by one team member are available to everyone
- Workflows created by one person can be triggered by anyone with access
- Credentials are shared — you don't need to re-add the same API key for each user

## Spend limits per user

Admins can set AI spend limits for individual users to control costs. To set a limit:
> *"Set a monthly AI spend limit of $20 for john@company.com."*

See [Billing & Plans](billing.md) for more on spend limits.

{% hint style="info" %}
**Need a custom permission structure?** Enterprise plans support advanced access controls. Contact us via the [Discord community](https://discord.gg/XEKxARDkNQ) or **Settings → Help**.
{% endhint %}
