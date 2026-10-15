# Claude Code 接入第三方兼容 API 完全指南

> Claude Code 本体免费，吃的是 Anthropic API。没有官方订阅也能用：把请求指向任何「Anthropic 协议兼容」的 API 即可。本文以 [天天AI](https://ai.ttshuli.com) 为例（其他兼容服务同理，只换域名和 key）。

[English](./claude-code.en.md) | 中文

## 1. 前置准备

1. 在服务提供方注册账号，控制台生成 API Key（形如 `sk-` 开头）
2. 确认服务方给出的 **Base URL** 和支持的**模型名**

## 2. 配置 Claude Code

新建 `~/.claude/settings.json`（Windows 在 `%USERPROFILE%\.claude\settings.json`），整段粘贴：

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

- `BASE_URL` 换成你的服务方地址（不要自己加 `/v1`，Anthropic 协议不加）
- 密钥在控制台生成，替换 `sk-mt-...`
- 模型全填 `auto`：系统自动路由到当前任务最优模型，不用手动挑

进入任意项目目录运行 `claude`，跳过官方登录即可开聊。

## 3. 常见报错速查

| 现象 | 原因 | 解法 |
|---|---|---|
| `Invalid API Key` | key 复制带了空格 / 用错环境 | 重新复制，检查首尾 |
| `Connection refused` / 超时 | Base URL 写错（多了 `/v1` 或漏了 `https://`） | 对照服务方文档 |
| `model not found` | 模型名与供应商不一致 | 改成 `auto` 或文档里的名字 |
| 配置改了不生效 | Claude Code 启动时读一次配置 | 完全退出重开 |

## 4. 和官方订阅的关系

- 官方订阅绑定官方客户端，第三方工具用订阅额度有封号风险（参见 OpenClaw 被踢事件）
- 兼容 API 按量计费，任何工具都能接，重度使用前先小额充值测稳定性

## 5. 其他工具怎么接

同一套 key，OpenAI 协议客户端（Cursor / Cherry Studio / Cline 等）Base URL 填 `https://ai.ttshuli.com/v1`（注意带 `/v1`），见 [cursor.md](./cursor.md) 和 [cherry-studio.md](./cherry-studio.md)。

---

*有问题开 issue，或参考[图文教程](https://ai.ttshuli.com/articles/claude-code-install.html)。*
