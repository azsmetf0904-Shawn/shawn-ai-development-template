# AGENTS.md — Coding Agent 工作規範

> 溝通、Git、安全底線詳見 `SHARED_RULES.md`，本文件只寫 Codex / Cursor 專屬行為。

## 專案概述

> **TODO**：複製模板後請填寫
>
> - 專案名稱：___
> - 核心功能：___
> - 技術棧：___
> - 進入點：___（例：`src/App.js`、`app/page.tsx`）

---

## Setup（必讀，每次開始前執行）

```bash
# 安裝依賴
npm install

# 啟動開發環境
npm run dev

# 確認測試通過
npm test
```

> 如果上面任何一步失敗，立刻停止並回報，不要繼續。

## Before Submitting（每次 commit 前必做）

```bash
# 確認 build 成功
npm run build

# 確認測試通過
npm test

# 有 lint 的話
npm run lint
```

> 如果 build 或 test 失敗，修好再 commit，不要跳過。

---

## Repository Structure

```
SHARED_RULES.md      ← 所有 AI 共用規則（先讀）
CLAUDE.md            ← Claude Code 專屬規範
AGENTS.md            ← Coding Agent 專屬規範（你在這）
TASKS.md             ← 任務看板，開始前讀，完成後更新
docs/ARCHITECTURE.md ← 技術架構，實作前必讀
docs/PRODUCT.md      ← 商業邏輯，不確定需求時讀
docs/DECISIONS.md    ← 已決定的架構，不要推翻
```

---

## Coding Agent 職責範圍

**你負責**：寫程式、修 Bug、補測試、重構

**你不負責**：架構決策、需求拆解、DB schema 設計（這些先討論再實作）

---

## 工作流程

### 開始任務前
1. 讀 `TASKS.md` 確認當前任務
2. 讀 `docs/ARCHITECTURE.md` 了解技術邊界
3. 任務描述不清楚 → 停下來問，不要假設

### 執行任務中
1. 只改動與任務相關的檔案
2. 發現 Bug → 記錄到 `TASKS.md` Bugs 區塊再繼續
3. 核心邏輯改動 → 先標記出來，請求確認

### 完成任務後
1. `TASKS.md` 任務從 Doing → Done
2. Before Submitting checklist 全過
3. commit（說明為什麼，不只說做了什麼）

---

## 禁止事項

| 禁止 | 原因 |
|------|------|
| 修改 `docs/DECISIONS.md` 裡已記錄的決策 | 決策不應被 agent 推翻 |
| 改動核心商業邏輯檔案（詳見 CLAUDE.md 填入的路徑）| 改錯影響所有用戶 |
| 沒有 WHERE 條件的 DELETE | 毀滅性操作 |
| force push | 覆蓋他人工作 |
| 引入 ARCHITECTURE.md 未列出的新依賴 | 未評估風險 |

---

## 遇到以下情況請停止並回報

- 需要 DB migration
- 需要修改環境變數
- 任務涉及超過兩個核心模組
- 測試 / build 失敗且無法自行解決

---

## Commit 格式

```
<type>(<scope>): <summary>

<optional body: 說明為什麼>
```

Types: `feat` / `fix` / `refactor` / `test` / `docs` / `chore`

範例：
```
fix(auth): session 過期後改為導回登入頁，不再顯示空白頁面
```
