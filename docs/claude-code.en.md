# Using Claude Code with a Third-Party Compatible API

> Claude Code itself is free — it consumes the Anthropic API. You don't need an official subscription: point it at any Anthropic-protocol-compatible API. This guide uses [Tiantian AI](https://ai.ttshuli.com) as the example (works with any compatible provider — just change the host and key).

[中文](./claude-code.md) | English

## 1. Prerequisites

1. Register with the provider and create an API key in the console (starts with `sk-`)
2. Note the provider's **Base URL** and supported **model names**

## 2. Configure Claude Code

Create `~/.claude/settings.json` (Windows: `%USERPROFILE%\.claude\settings.json`):

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://ai.ttshuli.com",
    "ANTHROPIC_API_KEY": "sk-mt-...",
    "ANTHROPIC_MODEL": "auto",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "auto",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "auto",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "auto"
  }
}
```

- Replace `BASE_URL` with your provider's address (no `/v1` — the Anthropic protocol doesn't use it)
- Generate the key in the provider console and replace `sk-mt-...`
- Setting every model to `auto` lets the system route each task to the best model automatically

Run `claude` inside any project directory and skip the official login.

## 3. Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `Invalid API Key` | copied with spaces / wrong environment | Copy again, check both ends |
| `Connection refused` / timeout | wrong Base URL (extra `/v1` or missing `https://`) | Check provider docs |
| `model not found` | model name doesn't match the provider | Use `auto` or the documented name |
| Config change not applied | Claude Code reads config at startup | Fully quit and relaunch |

## 4. Relationship with official subscriptions

- Official subscriptions are tied to the official client; using subscription quota in third-party tools risks bans (see the OpenClaw incident)
- Compatible APIs are pay-as-you-go and work with any tool — top up a small amount first to test stability

## 5. Other tools

The same key works in OpenAI-protocol clients (Cursor / Cherry Studio / Cline, etc.) with base URL `https://ai.ttshuli.com/v1` (note the `/v1`) — see [cursor.en.md](./cursor.en.md) and [cherry-studio.en.md](./cherry-studio.en.md).

---

*Open an issue if you get stuck.*
