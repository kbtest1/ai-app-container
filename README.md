# ai-app-container

A minimal Slack app built with [Bolt for JavaScript](https://tools.slack.dev/bolt-js/), running in Socket Mode.

## Requirements

- Node.js 18+
- A Slack app with Socket Mode enabled

## Setup

```bash
npm install
```

Set the following environment variables:

- `SLACK_BOT_TOKEN` — bot user OAuth token (`xoxb-…`)
- `SLACK_SIGNING_SECRET` — app signing secret
- `SLACK_APP_TOKEN` — app-level token with `connections:write` (`xapp-…`)
- `PORT` — optional, defaults to `3000`

## Run

```bash
npm start
```

You should see `⚡️ Bolt app is running!` once the app connects.

## Behavior

The app listens for messages containing `hello` and replies by greeting the sender.

## Reference: Oz integrations quickstart (summary)

Summary of Warp's [Integrations quickstart](https://docs.warp.dev/agent-platform/cloud-agents/integrations/quickstart) doc, which covers triggering Oz cloud agents from Slack (~15 minutes to set up). The same steps apply to Linear — substitute `linear` for `slack`.

### What it does

Oz integrations let you trigger cloud agents from tools your team already uses. Once Slack is connected, anyone can tag `@Oz` in a message or thread to kick off a cloud agent that runs the task and posts results back in-thread.

### Prerequisites

- **Eligible plan** — a Warp team on Build, Max, or Business with at least 20 credits available.
- **An Oz cloud environment** — agents run inside a configured environment containing repos and dependencies. Create one via the Cloud Agents Quickstart or `/create-environment` in Warp.
- **GitHub authorization** — Warp needs repo access to clone code and open PRs; you authorize the Warp GitHub app on first use.

### 1. Connect the Slack integration

Easiest path is the Oz web app: go to [oz.warp.dev/integrations](https://oz.warp.dev/integrations), click **Slack**, then follow the guided flow to pick an environment and authorize Oz in your Slack workspace. All members of your Warp team can then use it.

Via the Oz CLI instead:

```bash
oz integration create slack --environment <ENV_ID>
```

Find `<ENV_ID>` with `oz environment list` or in the Oz web app. The command opens a browser to authorize the Oz app. Add a default prompt applied to every run from this integration with `--prompt`:

```bash
oz integration create slack \
  --environment <ENV_ID> \
  --prompt "Always open a draft PR and request review from the team-leads group."
```

### 2. Tag @Oz in Slack

In any channel or thread, tag `@Oz` with a task, e.g. *"@Oz scan the authentication module for security issues and summarize what you find"*. Oz acknowledges immediately, starts a cloud agent run, and posts progress updates in the thread. Tagging `@Oz` inside an existing thread automatically picks up the full thread history as context, so there's no need to repeat background.

### 3. Watch the run

- **Session link** — Oz posts a link in the thread that opens a live terminal view where you can watch in real time or add follow-up instructions.
- **[oz.warp.dev/runs](https://oz.warp.dev/runs)** — the full run transcript: status, commands executed, files changed, and agent output.

When the task finishes, Oz posts a summary back to the original Slack thread.

### Next steps

- Use a **skill** as the integration's base prompt for consistent, reusable instructions across runs.
- Trigger agents programmatically with the Warp **API & SDK**.
- See the full Slack reference for identity mapping, team access, monitoring, troubleshooting, and uninstall instructions.
