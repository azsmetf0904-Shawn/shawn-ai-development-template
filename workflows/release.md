# Workflow：發版 SOP

把功能從開發環境安全上線到 production 的流程。

---

## 發版前 checklist

### 功能確認

- [ ] 所有 Doing 的任務已移到 Done
- [ ] 主要功能流程在本地測試通過
- [ ] 已知的 P0/P1 Bug 已修復
- [ ] `TASKS.md` 沒有遺漏的 Doing 任務

### 程式碼確認

- [ ] 沒有 `console.log` 留在程式碼中（除非是刻意的 debug 工具）
- [ ] 沒有 hardcode 的測試資料或假資料
- [ ] 環境變數都設定正確（Vercel environment variables）
- [ ] 沒有未完成的 TODO comment 影響功能

### 資料庫確認（如果有 schema 異動）

- [ ] Migration 已在 staging / 測試環境跑過
- [ ] Migration 有回滾方案
- [ ] 有備份計畫（Supabase 有自動備份）

---

## 發版流程

### 1. 最後一次測試

```bash
npm start
# 手動測試以下情況：
# - 主要用戶流程（Happy Path）
# - 最近修改的功能
# - 登入 / 登出
```

### 2. Build 確認

```bash
npm run build
# 確認 build 成功，沒有 error
# 有 warning 不一定要修，但要知道是什麼
```

### 3. Commit 所有變更

```bash
git status                    # 確認沒有遺漏的檔案
git add [相關檔案]             # 不用 git add -A，指定檔案
git commit -m "feat: [版本描述]"
git push
```

### 4. Vercel Preview 確認

```bash
# Vercel 會自動建立 Preview Deployment
# 等待 Preview 部署完成（約 1-2 分鐘）
# 在 Preview URL 做最終測試
```

### 5. 部署 Production

```bash
vercel --prod
# 等待部署完成
# 確認 production URL 正常
```

### 6. 部署後確認（5-10 分鐘後）

- [ ] 首頁載入正常
- [ ] 登入功能正常
- [ ] 剛上線的新功能正常
- [ ] 沒有 Vercel runtime error

---

## 更新文件

```markdown
# CHANGELOG.md 新增一個版本
## [x.y.z] - YYYY-MM-DD

### Added
- [新功能描述]

### Fixed
- [修復的 Bug]

### Changed
- [改動的功能]
```

---

## 緊急回滾

如果 production 出問題：

```bash
# 方法一：Vercel dashboard 回滾（最快）
# 進入 Vercel 專案 → Deployments → 找到上一個好的版本 → Promote

# 方法二：git revert
git revert HEAD~1
git push
# Vercel 會自動重新部署
```

---

## 版本號規則（Semantic Versioning）

- **v1.0.0** → 大版本：不相容的 API 變更、重大架構改動
- **v1.1.0** → 小版本：新功能
- **v1.1.1** → 修補版本：Bug 修復

簡單原則：
- 修 Bug → patch（0.0.X）
- 新功能 → minor（0.X.0）
- 大改版 → major（X.0.0）
