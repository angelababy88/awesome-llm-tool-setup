# Hermes — Your 24/7 AI Assistant, Deployed in One Click

> Fully hosted, tokens included on signup. **Join the QQ group to grab a redeem voucher — starting at ¥29 (~$4) for 7 days of Hermes access.**
> Claude Code / Cursor / Cherry Studio without an official subscription or overseas payment — sign up and go; an OpenAI / Anthropic compatible token API is bundled with the same account.

English | [中文](./README.md)

## What is Hermes?

Not a bare API — a **hands-on agent that gets work done**:

- State your goal; it breaks it down, drafts, and iterates until it's deliverable
- Writing · fiction · coding · coursework · slides · document cleanup — it covers them all
- Fully configurable: persona, model, skills, plugins (MCP) — it adapts to how you work
- Feishu (Lark) integration: drop tasks into a group chat and it gets on with it

## Why "one-click deployment"?

| What you'd expect to do | Reality |
|---|---|
| Rent a server, set up the env, configure models | **Not needed** — Hermes is a hosted instance; the server side is handled for you |
| Top up and estimate token costs | **Tokens included** — plans come with a generous usage allowance |
| Craft prompts and tune parameters | **Zero config** — pick a persona and model in the dashboard, and start talking |

Late-night deadlines, weekend crunch — your assistant is online 24/7.

## 🎁 Redeem-code campaign

1. Join the QQ group: **833984139**
2. Claim a voucher in the group (**starts at ¥29**, roughly $4)
3. Enter the redeem code in the dashboard → unlock **7 days of Hermes access**
4. Subscribe only if you like it — no sunk cost

Questions? Email angelababy88@proton.me

## Prefer to code against an API?

The same account also gives you an OpenAI / Anthropic compatible API — point Cursor, Claude Code, or Cherry Studio at a new config and go.

Claude Code example — create `~/.claude/settings.json` and paste (generate your key in the dashboard, replace `sk-mt-...`):

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://ai.ttshuli.com",
    "ANTHROPIC_API_KEY": "sk-mt-...",
    "ANTHROPIC_MODEL": "auto",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "auto",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "auto",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "auto",
    "ANTHROPIC_DEFAULT_FABLE_MODEL": "auto"
  }
}
```

Save, `cd` into your project, and run `claude`. All models point to `auto` so the system picks the best one. For OpenAI-protocol clients (Cursor / Cherry Studio etc.), use base URL `https://ai.ttshuli.com/v1`. Full walkthrough: https://ai.ttshuli.com/articles/claude-code-install.en.html

## FAQ

**Q: Does Claude Code require an official subscription or browser login?**
No. Write `~/.claude/settings.json` (see config above) pointing at a compatible API and skip the official login entirely.

**Q: How do I switch Cursor to a different API provider?**
Settings → Models → enter your API key, set Override OpenAI Base URL to `https://ai.ttshuli.com/v1`, pick model `auto`.

**Q: And Cherry Studio?**
Settings → Model Services → add an OpenAI-compatible provider with host `https://ai.ttshuli.com`, then add models manually.

**Q: Do I need my own server for Hermes?**
No. Hermes is a hosted instance — one click to deploy, server environment and starter tokens all included.

**Q: How do redeem codes work?**
Join QQ group 833984139 to claim a voucher (from ¥29), enter the code in the dashboard, and unlock 7 days of Hermes access instantly.

## In-depth tutorials (docs/)

- [Claude Code with a third-party compatible API](./docs/claude-code.en.md) ([中文](./docs/claude-code.md)) — setup, troubleshooting, and the subscription trade-off

## Links

- Dashboard / Get Hermes: https://ai.ttshuli.com
- Token plans: https://ai.ttshuli.com/plans.html

---

*Open an issue, or join QQ group 833984139 to chat directly.*
