# Claude Code / Cursor in China: compatible API setup

> Official subscriptions lock you to their client; overseas cards are painful; direct connections drop. Point your tools at any **OpenAI / Anthropic compatible** endpoint and pay per token.
> Examples use [天天AI](https://ai.ttshuli.com): sign up, pay-as-you-go tokens, usage visible. Hermes (hosted agent) is optional on the same account.

English | [中文](./README.md)

## What this repo is

Working setup guides (Claude Code / Cursor / Cherry Studio), not a product brochure. Swap the host and key if you use another compatible provider.

- Dashboard: https://ai.ttshuli.com
- Token plans: https://ai.ttshuli.com/plans.html
- Claude Code walkthrough: https://ai.ttshuli.com/articles/claude-code-install.en.html
- Trial codes: join **QQ group 833984139** (codes are handed out in the group, not pasted here)

## 30-second cheat sheet

| Client | Base URL | Model |
|---|---|---|
| Claude Code (Anthropic protocol) | `https://ai.ttshuli.com` (**no** `/v1`) | `auto` |
| Cursor / Cherry Studio / Cline (OpenAI protocol) | `https://ai.ttshuli.com/v1` (**with** `/v1`) | `auto` |
| API Key | from the dashboard, looks like `sk-mt-...` | |

## Claude Code

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

Save, `cd` into a project, run `claude`, skip the official login. Full steps + error table: [docs/claude-code.en.md](./docs/claude-code.en.md).

## Cursor

Settings → Models → API key, Override OpenAI Base URL `https://ai.ttshuli.com/v1`, model `auto`. See [docs/cursor.en.md](./docs/cursor.en.md).

## Cherry Studio

Settings → Model Services → add an OpenAI-compatible provider, API Host `https://ai.ttshuli.com`, then add models. See [docs/cherry-studio.en.md](./docs/cherry-studio.en.md).

## Pitfalls we actually hit

- Prefer transparent per-token billing over “unlimited monthly”
- Top up a little, soak for a couple of days, then add more
- Prices below cost usually mean stolen/shared subscriptions
- Do not append `/v1` on Anthropic clients; do not omit `/v1` on OpenAI clients

## Hermes panel (optional)

Same account, hosted instance: persona / skills / MCP / Feishu. **It spends the same token balance.** Not the focus of this repo.

## FAQ

**Q: Official subscription required?**  
No. Compatible API + the config above. You can register from mainland China.

**Q: Redeem codes?**  
QQ group 833984139, then Dashboard → Recharge → redeem.

**Q: Support?**  
Issues here, QQ group 833984139, or angelababy88@proton.me

---

*Tutorials, not ads. If a step is wrong, open an issue.*
