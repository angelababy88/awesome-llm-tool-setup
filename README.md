# mytoken

大模型 Token 代理中转 SaaS：对外兼容 **OpenAI** 与 **Anthropic**，对内渠道路由、计费；提供用户控制台与管理后台。

## 技术栈

- API：Python 3.12 + Sanic
- 网关 / 前端：OpenResty（用户控制台 + 管理后台静态页 + 反代 API）
- 数据：MySQL 8 + Redis；**手写 SQL（asyncmy 连接池）**，无 ORM
- 上游 HTTP：httpx 长生命周期连接池
- 前端：多页原生 HTML + 本地 Bootstrap + 原生 JS（无 TypeScript / Vite）
  - 用户控制台（PC）：`front/` → `/`
  - 用户控制台（手机 WAP）：`front-wap/` → `/m/`（两端 UA 互跳）
  - 管理后台：`admin/` → `/admin/`

## 快速开始（本地 API 开发）

```bash
cp .env.example .env
cd deploy && docker compose up -d mysql redis
cd ..
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements-dev.txt

# 建表 + 管理员种子
PYTHONPATH=. python -m server.bootstrap

# 仅 API（不含静态页）
# 对外（含宿主机/LAN）请用单进程、勿加 --dev：auto-reload 易与残留进程抢绑 :8000，导致 curl 52 Empty reply
PYTHONPATH=. sanic server.app:app --host 0.0.0.0 --port 8000 --single-process
# 仅本机热重载开发可加 --dev；启动前先清空端口：fuser -k 8000/tcp
```

健康检查：`curl http://127.0.0.1:8000/healthz` → `{"status":"ok"}`  
默认管理员由 bootstrap 用 `.env` 的 `ADMIN_USERNAME` / `ADMIN_PASSWORD` 写入数据库（示例 `admin` / `admin123`）；之后登录与改密只认库里的 `is_admin` 用户。

用户控制台与管理后台请用下方 Docker 全栈（OpenResty 托管 `front/`、`admin/`）。

## 对外协议

| 协议 | 路径 | 鉴权 |
|------|------|------|
| OpenAI | `POST /v1/chat/completions` | `Authorization: Bearer <sk-mt-...>` |
| OpenAI | `GET /v1/models` | 可选 |
| Anthropic | `POST /v1/messages` | `x-api-key: <sk-mt-...>` |

终端用户**只指定 `model`**。运营在管理后台「模型」页配置：该模型对应的上游地址、密钥与计价；每个模型一条有效接入。底层表对用户和管理文案都不叫「渠道」。

```bash
curl http://127.0.0.1:8000/v1/chat/completions \
  -H "Authorization: Bearer sk-mt-..." \
  -H "Content-Type: application/json" \
  -d '{"model":"gpt-4o-mini","messages":[{"role":"user","content":"hi"}]}'
```

### 用户控制台

公开落地页：`/`（手机自动跳 `/m/`）。登录后控制台：`/overview.html`（WAP：`/m/overview.html`）。  
公开教程（SEO 静态页）：`/articles/`（WAP：`/m/articles/`）；源稿在 `content/articles/*.md`，改完后执行 `python scripts/build_articles.py` 再提交生成的 HTML。  
用户 API：`/api/user/*`，响应 `{code,message,data}`；鉴权 `Authorization: Bearer <user-token>`（与管理端 token 隔离，PC/WAP 共用）。  
充值：可创建待支付订单；管理员仍可在后台手工加款。

### 管理后台

仪表盘 / 用户 / 模型 / 调用日志。  
管理 API：`/api/admin/*`，响应 `{code,message,data}`，分页 `page` + `page_size`。

## 目录结构

```
server/            # 服务端包根（Sanic API + 领域逻辑）
  app.py           # Sanic 入口
  bootstrap.py     # 建表与种子
  blueprints/      # HTTP 路由（含 user_api / admin_api）
  services/        # 代理流水线等
  auth/            # 密码、API Key
  billing/         # 预扣 / 结算
  channels/        # 路由与熔断
  infra/           # 配置、连接池、schema.sql
  proto/           # Canonical + OpenAI/Anthropic codec
  providers/       # 上游适配器
front/             # 用户控制台 PC（OpenResty → /）
front-wap/         # 用户控制台手机端（OpenResty → /m/）
content/articles/  # SEO 教程 MD 源稿（build → front/articles + front-wap/articles）
admin/             # 管理后台（OpenResty → /admin/）
deploy/
  Dockerfile       # API 镜像
  docker-compose.yml
  openresty/nginx.conf
tests/
```

## Docker（API + OpenResty）

```bash
cp .env.example .env
cd deploy && docker compose up -d --build
```

- 入口：OpenResty（`:80` / `:443`）
  - `/` → 公开落地页；其余用户页同属 `front/`（概览 `/overview.html`）
  - `/admin/*` → 管理后台静态页
  - `/v1/*`、`/api/*`、`/healthz` 等 → 反代到内部 `api:8000`
- 公开站 / 控制台：https://ai.ttshuli.com/ 、https://ai.ttshuli.com/overview.html （或 `/login.html`）
- 管理后台：https://ai.ttshuli.com/admin/login.html
- 对外 Base URL：OpenAI `https://<域名>/v1`，Anthropic `https://<域名>`（与控制台同域，靠路径分流）
- API 容器不对外暴露端口，只走 OpenResty
