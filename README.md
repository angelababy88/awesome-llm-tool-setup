# 国内用 Claude Code / Cursor：兼容 API 接入指南

> 官方订阅绑死客户端、海外卡难开、直连不稳定——把请求指到兼容 **OpenAI / Anthropic** 协议的服务即可按量用。
> 本文以 [天天AI](https://ai.ttshuli.com) 为例：注册即用、Token 按量计费、明细可查。同账户可选 Hermes 托管面板，需要再开。

[English](./README.en.md) | 中文

## 这仓库是干什么的

一组**真能跑通**的接入教程（Claude Code / Cursor / Cherry Studio），不是产品说明书。示例服务用天天AI，换别家兼容接口只改域名和 Key。

- 控制台：https://ai.ttshuli.com
- Token 套餐：https://ai.ttshuli.com/plans.html
- Claude Code 图文：https://ai.ttshuli.com/articles/claude-code-install.html
- 体验码：加 **QQ 群 833984139** 领（群里发，不在 README 里贴码）

## 30 秒对照

| 客户端 | Base URL | 模型 |
|---|---|---|
| Claude Code（Anthropic 协议） | `https://ai.ttshuli.com`（**不要**加 `/v1`） | `auto` |
| Cursor / Cherry Studio / Cline（OpenAI 协议） | `https://ai.ttshuli.com/v1`（**必须**带 `/v1`） | `auto` |
| API Key | 控制台生成，形如 `sk-mt-...` | |

## Claude Code

新建 `~/.claude/settings.json`（Windows：`%USERPROFILE%\.claude\settings.json`）：

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

保存后进项目目录跑 `claude`，跳过官方登录即可。完整步骤与报错表见 [docs/claude-code.md](./docs/claude-code.md)。

## Cursor

Settings → Models → 填 API Key，Override OpenAI Base URL 填 `https://ai.ttshuli.com/v1`，模型选 `auto`。详见 [docs/cursor.md](./docs/cursor.md)。

## Cherry Studio

设置 → 模型服务 → 添加 OpenAI 兼容供应商：API Host `https://ai.ttshuli.com`，再手动加模型。详见 [docs/cherry-studio.md](./docs/cherry-studio.md)。

## 避坑（踩过才写）

- 计费要透明：能看 Token 明细、按量扣的，比「包月无限」靠谱
- 先小额充值，跑两三天看成功率和延迟，再加码
- 别贪成本以下的超低价（多半是订阅号硬跑，会翻车）
- Anthropic 客户端不要自己给 Base URL 加 `/v1`；OpenAI 客户端漏了 `/v1` 会 404

## 同账户的 Hermes 面板（可选）

不想自己配客户端时，可以在控制台开通托管实例：人设 / 技能 / MCP / 飞书。**额度走同一份 Token**，不是另一套余额。需要再看控制台「Hermes」，不是本仓库重点。

## FAQ

**Q：一定要官方订阅吗？**  
不用。兼容 API + 上面配置即可，国内可直接注册。

**Q：兑换码怎么用？**  
加 QQ 群 833984139 领体验码，官网「充值 → 兑换码充值」输入即到余额。

**Q：出问题找谁？**  
本仓库 issue，或 QQ 群 833984139，或 angelababy88@proton.me

---

*Tutorials, not ads. If a step is wrong, open an issue.*
