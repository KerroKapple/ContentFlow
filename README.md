# ContentFlow

一份素材，按平台规范生成多平台内容，并支持定时与自动发布。

## 功能

- **多平台生成**：小红书、抖音、B 站、公众号、Twitter、博客。每个平台一套独立 prompt（字数、标签、封面文案等约束），输出强制为结构化 JSON
- **品牌档案**：为不同账号设定语气与风格（专业 / 轻松 / 种草等），生成时自动注入
- **热点选题**：聚合今日头条、百度、知乎热榜作为选题参考
- **定时与发布**：APScheduler 定时任务；基于 Playwright 会话的小红书 / B 站 / Twitter 发布
- **账号与用量**：注册登录（JWT）、生成历史、用量统计
- **多模型后端**：OpenAI 兼容接口（Gemini / Qwen）与 Anthropic 可切换

## 技术栈

| 层 | 技术 |
|---|---|
| 后端 | FastAPI · SQLAlchemy 2.0 (async) · Alembic · PostgreSQL · Redis · APScheduler · Playwright |
| 前端 | Next.js 16 · React 19 · Tailwind CSS v4 · shadcn/ui |
| 部署 | Railway（`backend/railway.toml`）或自建服务器（`deploy/`） |
| CI | GitHub Actions：后端 pytest，前端 build |

## 目录结构

```
backend/    FastAPI 服务（models / routers / schemas / services / prompts）
frontend/   Next.js 管理端（生成、品牌、日历、定时、历史）
deploy/     自建服务器部署脚本
docs/       设计文档与实施计划
```

## 本地开发

```bash
# 后端
cd backend
cp .env.example .env   # 填入数据库连接与至少一个模型 API Key
uv sync
uv run uvicorn app.main:app --reload

# 测试
uv run pytest -v

# 前端
cd frontend
npm install
npm run dev
```

## 设计文档

- [总体设计](docs/superpowers/specs/2026-03-23-contentflow-design.md)
- [Phase 2 设计](docs/superpowers/specs/2026-03-23-contentflow-phase2-design.md)
