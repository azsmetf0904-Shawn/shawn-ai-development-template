# AGENTS.md — Coding Agent 工作規範

這份文件是給 Codex、Cursor、GitHub Copilot Workspace 等 coding agent 的工作指令。
請在開始任何任務前先完整讀取此文件。

## 專案概述

> **TODO**：複製模板後請填寫
>
> - 專案名稱：___
> - 核心功能：___
> - 技術棧：___
> - 進入點：___（例如：`src/App.js`、`app/page.tsx`）

## Coding Agent 職責範圍

你（coding agent）負責：
- 撰寫、修改、重構程式碼
- 修復 Bug
- 補充測試
- 依照規格實作功能

你**不負責**：
- 架構決策（交給 Claude / Shawn）
- 商業需求拆解（交給 Claude / Shawn）
- 資料庫 schema 設計（先討論再實作）

## 工作流程

### 開始任務前
1. 讀取 `TASKS.md` 確認當前任務是什麼
2. 讀取 `docs/ARCHITECTURE.md` 了解技術架構
3. 讀取 `docs/PRODUCT.md` 了解商業邏輯
4. 如果任務描述不夠清楚，停下來問，不要假設

### 執行任務中
1. 只改動與任務相關的檔案
2. 不要順手「順便優化」無關的程式碼
3. 遇到核心商業邏輯的改動，標記出來請求確認
4. 發現 Bug 或風險，立刻記錄到 `TASKS.md` 的 Bugs 區塊

### 完成任務後
1. 更新 `TASKS.md`，將任務從 Doing 移至 Done
2. 確認所有測試通過（如果專案有測試）
3. 用清楚的 commit message 提交（說明「為什麼」）

## 程式碼規範

### 命名
- 變數、函式名稱要清楚表達「是什麼」
- 布林值用 `is_`、`has_`、`can_` 開頭
- 函式用動詞開頭（`fetch_`, `create_`, `update_`, `delete_`）

### 結構
- 優先編輯現有檔案，不隨意建立新檔
- 不引入未在 `docs/ARCHITECTURE.md` 中提到的新依賴
- 如果需要新依賴，先說明原因

### 安全
- 永遠驗證用戶輸入
- 不在前端暴露 secret / API key
- SQL 查詢用 parameterized query，不用字串拼接
- 不 console.log 敏感資料

### 測試
- 新功能需有對應的基本測試
- 修 Bug 需新增防止迴歸的測試
- 測試要測行為，不測實作細節

## 禁止事項

- **禁止**修改 `docs/DECISIONS.md` 裡已記錄的架構決策
- **禁止**改動核心商業邏輯（計分、權限、金流）而不先說明
- **禁止**刪除資料庫資料（即使是測試資料）
- **禁止**使用 `--no-verify` 跳過 git hook
- **禁止**force push 任何分支

## 遇到以下情況請停止並回報

- 任務要求改動兩個以上核心模組
- 任務描述與現有程式碼邏輯衝突
- 需要新增 DB migration
- 需要修改環境變數
- 任務涉及外部 API 的 credential 處理

## Git Commit 格式

```
<type>(<scope>): <summary>

<optional body: 說明為什麼，不是說明做了什麼>
```

Type 選項：
- `feat`：新功能
- `fix`：修 Bug
- `refactor`：重構（不改功能）
- `test`：補測試
- `docs`：文件
- `chore`：建置、設定

範例：
```
fix(auth): 修正 session 過期後沒有自動重導向的問題

用戶在 token 過期時直接看到空白頁面，改為導回登入頁。
```

## 技術棧參考

> **TODO**：填入此專案的技術棧

| 層次 | 技術 |
|------|------|
| Frontend | React / Next.js |
| Auth | Supabase Auth |
| Database | PostgreSQL（via Supabase）|
| Storage | Supabase Storage |
| 部署 | Vercel / Zeabur |
| 自動化 | n8n |
