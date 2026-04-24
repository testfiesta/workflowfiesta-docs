---
icon: computer
---

# Runner

The WorkflowFiesta Runner connects your local machine or server to the platform. Once installed, agents can read your local files, access internal databases, and run scripts on your own hardware.

{% hint style="info" %}
**The Runner is optional.** Most workflows run entirely in the cloud. You only need the Runner if you want agents to access files or systems on your local machine or private network.
{% endhint %}

***

## What the Runner enables

<table data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td>📁 <strong>Local File Access</strong></td><td>Agents can read and write files on your machine — documents, spreadsheets, code repositories, config files.</td></tr><tr><td>🗄️ <strong>Internal Databases</strong></td><td>Query databases that aren't exposed to the internet — Postgres, MySQL, SQLite, internal APIs.</td></tr><tr><td>🔧 <strong>Local Tools</strong></td><td>Run any tool installed on your machine — Python scripts, CLI tools, custom executables.</td></tr><tr><td>🔒 <strong>Private Network Access</strong></td><td>Access services behind your firewall or VPN without exposing them to the internet.</td></tr></tbody></table>

***

## How it works

The Runner connects **outbound** to WorkflowFiesta's servers over HTTPS. No inbound ports. No firewall changes. No VPN configuration.

```
Your Machine                    WorkflowFiesta
     │                               │
     │  ── outbound HTTPS ──►        │
     │  ◄── receives job ──          │
     │  runs script locally          │
     │  ── sends output ──►          │
     │                               │
```

When a workflow step targets your Runner, WorkflowFiesta sends the script to the Runner, the Runner executes it natively on your OS, and the output is returned to the workflow.

***

## Installation

{% tabs %}
{% tab title="macOS" %}
#### macOS (Apple Silicon or Intel)

**Step 1 — Download the Runner**

```bash
# Apple Silicon (M1/M2/M3)
curl -L https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-darwin-arm64 -o wff-runner

# Intel Mac
curl -L https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-darwin-amd64 -o wff-runner

chmod +x wff-runner
```

**Step 2 — Get your registration code**

1. Go to **Settings → Runners** in WorkflowFiesta
2. Click **Add Runner**
3. Give it a name (e.g. `my-macbook`)
4. Copy the registration code

**Step 3 — Register and start**

```bash
./wff-runner --code YOUR_REGISTRATION_CODE
```

The Runner will connect and show as **Online** in Settings → Runners.

{% hint style="success" %}
To keep the Runner running after you close the terminal, add it to your login items or run it as a background service.
{% endhint %}
{% endtab %}

{% tab title="Linux" %}
#### Linux (headless or desktop)

**Step 1 — Download the Runner**

```bash
# Headless / server
curl -L https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-linux-amd64 -o wff-runner
chmod +x wff-runner

# Desktop GUI app
curl -L https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-linux-amd64-gui -o wff-runner-gui
chmod +x wff-runner-gui
```

**Step 2 — Get your registration code**

1. Go to **Settings → Runners** in WorkflowFiesta
2. Click **Add Runner**, give it a name, copy the code

**Step 3 — Register and start**

```bash
./wff-runner --code YOUR_REGISTRATION_CODE
```

**Run as a systemd service (recommended for servers):**

```bash
# Create service file
sudo tee /etc/systemd/system/wff-runner.service > /dev/null << EOF
[Unit]
Description=WorkflowFiesta Runner
After=network.target

[Service]
ExecStart=/path/to/wff-runner --code YOUR_REGISTRATION_CODE
Restart=always
User=$USER

[Install]
WantedBy=multi-user.target
EOF

# Enable and start
sudo systemctl enable wff-runner
sudo systemctl start wff-runner
sudo systemctl status wff-runner
```
{% endtab %}

{% tab title="Windows" %}
#### Windows

**Option 1 — GUI Desktop App (recommended)**

1. Download: [workflowfiesta-runner-windows-amd64-gui.exe](https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-windows-amd64-gui.exe)
2. Run the `.exe`
3. Go to **Settings → Runners** in WorkflowFiesta, click **Add Runner**, copy the code
4. Paste the registration code into the app
5. Click **Connect**

**Option 2 — Headless (PowerShell)**

```powershell
# Download
Invoke-WebRequest -Uri "https://github.com/ss-libs/workflowfiesta-runner/releases/latest/download/workflowfiesta-runner-windows-amd64.exe" -OutFile "wff-runner.exe"

# Register and start
.\wff-runner.exe --code YOUR_REGISTRATION_CODE
```
{% endtab %}
{% endtabs %}

***

## Verify the connection

After starting the Runner, go to **Settings → Runners** in WorkflowFiesta. Your runner should show as **Online** or **Idle**.

{% hint style="warning" %}
If the runner shows as **Offline** or **Pending**:

1. Check that the Runner process is still running on your machine
2. Verify your machine has outbound internet access on port 443
3. Check that the registration code hasn't expired (codes are valid for 60 minutes)
{% endhint %}

***

## Use the Runner in a workflow

To run a workflow step on your Runner, attach it to an Environment and reference that environment in your workflow step.

**Step 1 — Create an environment for your Runner**

1. Go to **Settings → Environments → New Environment**
2. Name it (e.g. `My Mac`)
3. Under **Runners**, select your runner
4. Save

**Step 2 — Reference the environment in your workflow**

```yaml
steps:
  - id: read_local_files
    type: script
    environment: My Mac    # name of the environment with your runner attached
    script: |
      ls ~/Documents/reports/
      cat ~/Documents/reports/latest.csv
```

The script runs natively on your machine with full access to your filesystem.

***

## Security

{% hint style="danger" %}
**The Runner executes scripts with the permissions of the user account it runs under.** Only connect runners to WorkflowFiesta organizations you control. Never run the Runner as root or Administrator unless you have a specific reason.
{% endhint %}

**What the Runner can access:**

* Files and directories accessible to the running user
* Network resources accessible from the machine
* Any tool or executable installed on the machine

**What WorkflowFiesta cannot do:**

* Access your machine without a workflow step explicitly targeting your Runner
* Read files that aren't accessible to the Runner's user account
* Execute code outside of workflow step invocations

***

## Troubleshooting

<details>

<summary>Runner shows as Offline immediately after connecting</summary>

This usually means the Runner process exited. Check:

1. Is the terminal/process still running?
2. Are there any error messages in the Runner output?
3. Does your machine have stable internet access?

</details>

<details>

<summary>Workflow step fails with "runner not available"</summary>

1. Verify the runner is Online in Settings → Runners
2. Check that the environment is correctly configured with the runner attached
3. Check that the workflow step references the correct environment name

</details>

<details>

<summary>Script can't find a local file</summary>

The Runner executes scripts from the user's home directory by default. Use absolute paths or `~/` to reference files:

```bash
cat ~/Documents/myfile.csv          # ✅ works
cat /Users/yourname/Documents/myfile.csv  # ✅ works
cat Documents/myfile.csv            # ⚠️ may not work — relative path
```

</details>

***

## What to read next

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>⚙️ <strong>Build Your First Workflow</strong></td><td>Use your Runner in a workflow step to access local files and systems.</td><td><a href="/broken/pages/rLfM8h3XRBsPDW5iRAIc">Broken link</a></td></tr><tr><td>🧩 <strong>Add Skills to Your Agent</strong></td><td>Give your agents new capabilities that run on your Runner.</td><td><a href="/broken/pages/cE4i4Xok4YQTVRxGz2RR">Broken link</a></td></tr><tr><td>🔑 <strong>Key Concepts</strong></td><td>Review environments, runners, and how they fit into the platform.</td><td><a href="/broken/pages/NTG9K8RkGRICSNDTJpqN">Broken link</a></td></tr></tbody></table>
