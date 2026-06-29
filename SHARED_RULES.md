# SHARED_RULES.md — 所有 AI 共用規則

這是單一事實來源（Single Source of Truth）。
CLAUDE.md 和 AGENTS.md 引用此文件，不重複寫規則。

---

## 溝通規則

- 語言：繁體中文
- 給選項時用「A 或 B」，不用開放式問句
- 一次只問一個問題
- 簡短直接，不加廢話
- 完成後說清楚：「完成了，下一步是 A 或 B？」

## Git 規則

- commit 後自動 push，不詢問確認
- commit message 說明「為什麼」，不只是「做了什麼」
- 不用 `--no-verify` 跳過 hook
- 不 force push 任何分支
- 不 amend 已推上去的 commit

## 安全底線

- 不 hardcode API key 或 secret
- 不 console.log 敏感資料（token、password、個資）
- SQL 查詢用 parameterized query
- 永遠驗證用戶輸入（只在 system boundary 驗證）
- 不引入未在 ARCHITECTURE.md 列出的新依賴（要先說明）

## 不做的事

- 不加不必要的 comment（只在 WHY 非常不明顯時才加）
- 不建立不必要的抽象層（三行重複 > 一個不必要的 helper）
- 不加「以防萬一」的 error handling
- 不做功能需求範圍外的「順手優化」
- 不刪除資料庫資料（即使是測試資料），有疑問先問

## 必須先確認才能動的事

- 核心商業邏輯改動（計分、權限、金流）
- 資料庫 schema 異動（新增欄位、改型別、刪除）
- 環境變數新增或修改
- 外部 API credential 處理
- 任何影響超過兩個核心模組的改動
