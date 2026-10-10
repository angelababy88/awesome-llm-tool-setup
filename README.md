# 把 Cursor / Claude Code / Cherry Studio 接到 OpenAI·Anthropic 兼容 API 的踩坑笔记

> 国内部署中转、协议双兼容（OpenAI / Anthropic）、注册拿 Key 改 Base URL 即用。
> 本文以 [天天AI](https://ai.ttshuli.com) 为例，任何兼容协议的服务同理。

## 为什么需要中转

直接用官方 API 的常见问题：网络不通、支付不便、不同工具各管一套 Key。
协议兼容的中转只做一件事：**客户端不用改，换个 Base URL 就能跑**。

## 三步接入（通用）

1. **注册拿 Key** —— 在控制台注册，生成 API Key。
2. **改 Base URL** —— OpenAI 系填 `https://ai.ttshuli.com/v1`；Anthropic 系填 `https://ai.ttshuli.com`。
3. **指定模型** —— 按控制台模型列表填 `model`，客户端里只需要选名字。

## 各工具配置速查

### Cherry Studio
设置 → 模型服务 → 添加 OpenAI 兼容供应商：
- API Host：`https://ai.ttshuli.com`
- API Key：控制台生成的 Key
- 模型：手动添加控制台列表里的模型名

### Claude Code
环境变量方式接入：
```bash
export ANTHROPIC_BASE_URL=https://ai.ttshuli.com
export ANTHROPIC_AUTH_KEY=sk-你的Key
claude
```

### Cursor
Settings → Models：
- OpenAI API Key 填控制台 Key
- Override OpenAI Base URL：`https://ai.ttshuli.com/v1`
- 勾选模型后 Verify

### Cline / Kilo Code / OpenCode
凡是「自定义 OpenAI / Anthropic Base URL」的客户端：
- Base URL：`https://ai.ttshuli.com/v1`（OpenAI 协议）
- API Key：控制台生成
- Model：控制台模型列表任选

## 常见坑

| 现象 | 原因 | 处理 |
|---|---|---|
| 401 | Key 填错或前面带空格 | 重新复制，注意别带 `Bearer` 前缀 |
| 404 | Base URL 少了 `/v1` | OpenAI 协议必须带 `/v1`，Anthropic 协议不带 |
| 模型不存在 | `model` 名字手打 | 一律从控制台模型列表复制 |
| 计费不动 | 客户端缓存 | 看控制台「用量明细」为准 |

## 进阶：不只是 API

同账户下还有 **Hermes 智能体面板**：可托管一个 24 小时在线的助理实例，配人设、技能、飞书接入，适合「丢任务给它干」而不是「自己写 prompt 调 API」的用法。控制台按需开通即可。

## 链接

- 控制台 / 注册：https://ai.ttshuli.com
- 接入文档（站内有完整版）：https://ai.ttshuli.com/docs.html

---

*觉得有用就点个 Star，配置有坑欢迎 issue 交流。*
