# ARCHITECTURE.md — 技術架構文件

> 這份文件描述整個系統的技術架構，AI 在實作前必須讀懂這份文件。

---

## 系統概覽

**架構類型**：___（例如：React SPA + Supabase BaaS、Next.js Full Stack、FastAPI + React）

**部署架構圖**：

```
用戶瀏覽器
    │
    ▼
[Vercel / Zeabur]          ← 靜態資源 / SSR
    │
    ├──► [Supabase]         ← Auth + PostgreSQL + Storage
    │        │
    │        └──► [Edge Functions]  ← Server-side 邏輯
    │
    └──► [n8n]              ← 自動化流程（LINE 推播、排程任務）
```

---

## 技術棧

| 層次 | 技術 | 版本 | 說明 |
|------|------|------|------|
| Frontend | ___ | ___ | ___ |
| Routing | ___ | ___ | ___ |
| Auth | Supabase Auth | ___ | email/password + 自定義 |
| Database | PostgreSQL（Supabase）| ___ | ___ |
| Storage | Supabase Storage | ___ | ___ |
| 部署 | Vercel / Zeabur | ___ | ___ |
| 自動化 | n8n | ___ | ___ |

---

## 目錄結構

```
src/
  ├── App.js / App.tsx        # 路由定義、auth guard
  ├── context/
  │   └── AuthContext.js      # 全域 auth 狀態
  ├── lib/
  │   └── supabase.js         # 所有 Supabase 呼叫集中於此
  ├── components/
  │   ├── Layout.js           # 共用 layout（導覽列、選單）
  │   └── UI.js               # 共用 UI 元件
  ├── pages/
  │   ├── public/             # 不需登入的頁面
  │   ├── member/             # 一般用戶頁面
  │   └── admin/              # 管理員頁面
  └── styles/
      └── global.css          # CSS 變數 + utility class
```

---

## 資料庫 Schema

### 主要表格

| 表格 | 說明 | 重要欄位 |
|------|------|----------|
| `users` / `members` | 用戶資料 | `id`, `role`, `created_at` |
| ___ | ___ | ___ |

### 關係圖

```
users
  │
  ├──► user_actions (1:N)
  └──► groups (N:1)
```

### 重要 View

| View 名稱 | 說明 | 注意事項 |
|-----------|------|----------|
| `user_scores` | 積分彙總 | 不能直接 INSERT/UPDATE |

---

## 認證流程

| 角色 | 登入方式 | 儲存位置 |
|------|----------|----------|
| 管理員 | Supabase Auth（email/password）| Supabase session |
| 一般用戶 | ___ | ___ |

`useAuth()` 回傳：`{ session, user, loading }`
- `session` 有值 → 管理員
- `user` 有值 → 一般用戶

---

## 環境變數

| 變數名稱 | 用途 | 必填 |
|----------|------|------|
| `REACT_APP_SUPABASE_URL` | Supabase 專案 URL | 是 |
| `REACT_APP_SUPABASE_ANON_KEY` | Supabase 匿名 Key | 是 |
| ___ | ___ | ___ |

---

## API 設計原則

- 所有 Supabase 呼叫集中在 `lib/supabase.js`，頁面元件不直接 import `supabase`
- Edge Functions 透過 `fetch` 直接呼叫，不走 supabase-js
- 所有 query 預設加 limit 避免資料量過大

---

## 效能考量

- 大量資料查詢必須分頁（`range()`）
- 避免在 render 函式中做 Supabase 查詢，使用 `useEffect`
- 靜態資源透過 CDN（Vercel / Supabase Storage）提供

---

## 安全設計

- Supabase RLS（Row Level Security）對所有用戶資料表啟用
- API Key 只存在環境變數，不 hardcode 在程式碼
- 用戶輸入在 server-side 驗證（Edge Function 或 Supabase Policy）

---

## 已知技術債

| 項目 | 說明 | 優先度 |
|------|------|--------|
| ___ | ___ | 低 / 中 / 高 |

---

## 架構決策歷史

詳細內容見 `docs/DECISIONS.md`。

| 日期 | 決策摘要 |
|------|----------|
| ___ | ___ |
