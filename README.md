# Hermes — 一键部署的 24 小时在线 AI 私人助理

> 服务器全托管、开通即送 Token，**加 QQ 群领兑换券，最低 29 元兑换 Hermes 7 天使用权限**。

[English](./README.en.md) | 中文

## Hermes 是什么

不是一个冷冰冰的 API，而是一个**帮你把活干完的智能体**：

- 你说目标，它拆步骤、出初稿、改到能交差
- 写文章 · 写小说 · 写代码 · 毕业设计 · 做 PPT · 整理文档，样样精通
- 人设、模型、技能、插件（MCP）全部可配置，越用越贴你的习惯
- 支持飞书接入，任务丢进群里就能干

## 为什么叫「一键部署」

| 你以为要做的 | 实际上 |
|---|---|
| 买服务器、装环境、配模型 | **不用**，Hermes 是托管实例，服务器由平台提供 |
| 充值、估算 Token 成本 | **开通即送 Token**，套餐内含大额使用额度 |
| 写 prompt、调参数 | **零配置**，控制台选好人设和模型，直接开聊 |

深夜赶工、周末加班，你的助理 24 小时在线。

## 🎁 兑换码活动

1. 加入 QQ 群：**833984139**
2. 群内领取兑换券（**最低 29 元**档）
3. 控制台输入兑换码 → 立刻解锁 **Hermes 7 天使用权限**
4. 满意再续，不满意到期即止，零沉没成本

咨询也可以邮件联系：angelababy88@proton.me

## 想自己写代码？同账户还有 Token API

同一账户提供兼容 OpenAI / Anthropic 协议的 API，Cursor、Claude Code、Cherry Studio 换个配置就能跑。

以 Claude Code 为例，新建 `~/.claude/settings.json`，粘贴整段（密钥在控制台生成，替换 `sk-mt-...`）：

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

保存后进入项目目录跑 `claude` 即可，模型全指到 `auto`，系统自动选最优。OpenAI 协议客户端（Cursor / Cherry Studio 等）Base URL 填 `https://ai.ttshuli.com/v1`，其余照旧。保姆级教程：https://ai.ttshuli.com/articles/claude-code-install.html

## 链接

- 控制台 / 开通 Hermes：https://ai.ttshuli.com
- Token 套餐：https://ai.ttshuli.com/plans.html

---

*有问题开 issue，或加 QQ 群 833984139 直接聊。*
