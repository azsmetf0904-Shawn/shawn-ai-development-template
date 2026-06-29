# Shawn AI Development Template

這是 Shawn 的標準 AI 開發模板，適用於所有新專案的快速啟動。

## 這個模板是什麼

一套可複製的專案規範框架，讓 Claude Code、Codex、Cursor 等 AI 工具能立即理解你的專案背景、協作方式與決策風格，不必每次重新說明。

## 適合什麼專案

- Web SPA（React / Next.js）
- 後端 API（FastAPI / Express / Supabase Edge Functions）
- 自動化流程（n8n workflow）
- 全端 SaaS（Supabase + Vercel / Zeabur）
- 任何需要 AI pair programming 的個人或小團隊專案

## 目錄說明

| 路徑 | 用途 |
|------|------|
| `CLAUDE.md` | Claude Code 專案工作規範 |
| `AGENTS.md` | Codex / Cursor 等 coding agent 規範 |
| `SIS_CORE.md` | Shawn 個人 AI 協作偏好與決策風格 |
| `TASKS.md` | 任務看板（Backlog / Doing / Done / Bugs / Decisions）|
| `docs/PRODUCT.md` | 產品需求文件模板 |
| `docs/ARCHITECTURE.md` | 技術架構文件模板 |
| `docs/DECISIONS.md` | 架構決策紀錄（ADR）|
| `docs/CHANGELOG.md` | 版本更新紀錄 |
| `prompts/` | 可複製使用的 AI prompt 集合 |
| `workflows/` | 功能開發、修 bug、發版、重構 SOP |

## 如何使用這個模板

### 方式一：複製整個模板

```bash
cp -r shawn-ai-development-template/ my-new-project/
cd my-new-project/
# 修改 README.md、PRODUCT.md、ARCHITECTURE.md 填入專案細節
```

### 方式二：從 GitHub Template 建立

1. 將此 repo 推上 GitHub，設定為 Template Repository
2. 新專案時點「Use this template」
3. Clone 後修改各 `.md` 文件填入專案細節

### 方式三：只複製需要的 prompt / workflow

進入 `prompts/` 或 `workflows/` 直接取用對應的 `.md` 貼入 AI 對話。

## 第一次使用 checklist

- [ ] 複製模板到新專案目錄
- [ ] 更新 `README.md`（專案名稱、描述）
- [ ] 填寫 `docs/PRODUCT.md`（商業目標、用戶、功能列表）
- [ ] 填寫 `docs/ARCHITECTURE.md`（技術棧、DB 結構）
- [ ] 請 Claude 讀取 `CLAUDE.md` + `SIS_CORE.md` 後開始工作
- [ ] 所有決策寫入 `docs/DECISIONS.md`
- [ ] 任務進度更新到 `TASKS.md`

## 核心原則

1. **Build > Perfect**：先做出可用版本，再優化
2. **先建立模型，再回答**：不理解需求不動手
3. **商業邏輯優先**：程式服務於業務，不反過來
4. **不動核心規則**：未確認前不修改核心商業邏輯
5. **主動指出問題**：AI 必須說出風險，不只附和

## 技術棧預設

- Frontend：React / Next.js App Router
- Backend：Supabase（Auth + PostgreSQL + Storage + Edge Functions）
- 自動化：n8n
- 部署：Vercel / Zeabur
- AI 工具：Claude Code、Codex、Cursor
