# Custom Commands

Custom commands are slash commands that let your team switch to a specific agent instantly from any conversation. Type `/marketing` and you're immediately talking to your Marketing Agent. Type `/jira` and you're in the Jira Agent.

{% hint style="success" %}
**Custom commands make your agents discoverable.** Instead of searching for an agent by name, your team types a short slash command and they're there instantly.
{% endhint %}

## What Is a Custom Command?

A custom command is a shortcut that:
1. Switches the conversation to a specific agent
2. Optionally sends an opening prompt to kick off the interaction
3. Appears in the chat autocomplete when you type `/`

## Creating a Custom Command

Ask WorkflowFiesta through conversation:

> "Create a slash command /marketing that switches to the Marketing Agent."

> "Create a /report command that triggers the weekly report workflow and says 'Generate this week's report.'"

> "Add a /support command for the Customer Support Agent with the icon 🎧."

The platform will create the command immediately. It appears in the chat autocomplete for everyone in your organization.

## Command Properties

| Property | Description | Example |
|---|---|---|
| **Command** | The slash command name (no spaces) | `marketing` |
| **Display name** | Label shown in autocomplete | `Marketing Agent` |
| **Icon** | Optional emoji | 📣 |
| **Agent** | Which agent it switches to | Marketing Agent |
| **Prompt template** | Optional opening message | "You are helping with a marketing task." |

## Using a Custom Command

Type `/` in any chat window to see all available commands. Select one or keep typing to filter:

```
/marketing    → switches to Marketing Agent
/jira         → switches to Jira Agent  
/report       → triggers the Report workflow
/support      → switches to Customer Support Agent
```

## Managing Commands

To see all commands:

> "Show me all the custom commands in our organization."

To update a command:

> "Update the /marketing command — point it to the new Brand Agent instead."

To delete a command:

> "Delete the /oldreport command."

## Best Practices

- Keep command names short and memorable: `/jira` not `/jira-ticket-creator`
- Use emoji icons to make commands visually distinct in the autocomplete
- Add a prompt template for commands that always start with the same context
- Create commands for your team's most-used agents — reduce friction to zero
