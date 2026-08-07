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
