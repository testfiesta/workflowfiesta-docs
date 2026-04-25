---
icon: square-question
---

# Troubleshooting the Runner

{% hint style="warning" %}
**WorkflowFiesta agents are fully self-aware.** They know the platform, its capabilities, and can take most actions for you directly. If you have a question, the fastest answer is always to ask the agent itself — just type it in the chat.
{% endhint %}


Common issues with the WorkflowFiesta Runner and how to fix them.

***

## Runner shows as Offline or Never Connected

**Cause:** The runner process isn't running, or it can't reach WorkflowFiesta's servers.

**Fix:**

1. Confirm the runner process is running:
   ```bash
   # macOS / Linux
   ps aux | grep wff-runner
   ```

2. Check outbound HTTPS (port 443) is not blocked:
   ```bash
   curl -I https://app.workflowfiesta.com
   # Should return HTTP 200 or 301
   ```

3. If the registration code has expired (codes are valid 60 minutes by default):
   - Go to **Settings → Runners**
   - Delete the pending runner
   - Click **Add Runner** to generate a new code
   - Re-register with the new code

4. Try running the runner with verbose output:
   ```bash
   ./wff-runner --code YOUR_CODE --verbose
   ```

{% hint style="warning" %}
A runner that was registered but never started shows as **Pending**. A runner that was connected but has stopped sending heartbeats shows as **Offline**. Both are fixed by starting the runner process.
{% endhint %}

***

## Runner connects then immediately disconnects

**Cause:** Network instability, sleep/hibernate settings, or the process is being killed.

**Fix:**

1. **Laptop users:** Disable sleep when plugged in, or use a server/desktop machine for production runners.

2. **Run as a system service** so it restarts automatically:

   ```bash
   # Linux — systemd
   sudo tee /etc/systemd/system/wff-runner.service > /dev/null << EOF
   [Unit]
   Description=WorkflowFiesta Runner
   After=network.target

   [Service]
   ExecStart=/usr/local/bin/wff-runner --code YOUR_CODE
   Restart=always
   RestartSec=5

   [Install]
   WantedBy=multi-user.target
   EOF

   sudo systemctl enable wff-runner
   sudo systemctl start wff-runner
   ```

3. Check for process managers (Docker, supervisord) that might be killing the process.

***

## Workflow step fails when targeting runner environment

**Cause:** The script references a tool, file, or path that doesn't exist on the runner machine.

**Fix:**

1. Verify the tool exists on the runner machine:
   ```bash
   which python3
   which node
   which git
   ```

2. Check file paths — paths in runner scripts are relative to the runner machine's filesystem, not the cloud:
   ```python
   # ✅ Correct — absolute path on runner machine
   with open("/Users/isaac/Documents/data.csv") as f:
       ...

   # ❌ Wrong — this path doesn't exist on the runner machine
   with open("/workspace/data.csv") as f:
       ...
   ```

3. Run the script manually on the runner machine to reproduce the error before debugging in the workflow.

***

## Multiple runners — jobs going to wrong runner

**Cause:** Runner selection strategy sending jobs to an unexpected runner.

**Fix:**

1. Go to **Settings → Environments**
2. Check which runners are attached to the environment
3. Adjust the **Runner Selection** strategy:
   - `first_available` — uses the first online runner (default)
   - `round_robin` — distributes evenly
   - `random` — picks randomly

4. If you need a specific runner for a specific workflow, create a dedicated environment with only that runner attached.

***

## Permission denied errors in scripts

**Cause:** The runner is running as a user without permission to access the file or directory.

**Fix:**

1. Check what user the runner is running as:
   ```bash
   ps aux | grep wff-runner
   ```

2. Ensure that user has read/write access to the paths the script needs:
   ```bash
   ls -la /path/to/file
   chmod 644 /path/to/file   # if you own it
   ```

3. If running as a system service, check the `User=` setting in the systemd unit file.

***

## Still stuck?

[Join the Discord](https://discord.gg/XEKxARDkNQ) and post in `#support` with:
- Your OS and architecture
- The runner version (`./wff-runner --version`)
- The error message or behavior you're seeing
