# changelog.md — Shawn Core 版本記錄

記錄 Shawn Core 的重要更新，包括：
- 新增的 Fact / Inference / Hypothesis
- 被推翻或修正的舊記錄
- 重要的行為模式升格（Hypothesis → Inference → Fact）

---

## v0.1.0 — 2026-06-29（初版）

### 建立

- `identity.md`：基本定位、能力輪廓、思維風格
- `values.md`：工作觀、Shawn Rule No.1、30 天工具封凍
- `decision.md`：決策風格、AI 給建議的正確格式
- `communication.md`：溝通偏好、讓我有/沒有能量的事
- `workflow.md`：AI 團隊分工、開發流程、多專案管理
- `business.md`：商業背景、專案優先順序、TeamStar 策略
- `blindspots.md`：5 個已知盲點，含 AI 應對建議

### 背景

這是第一版 Shawn Core，從以下來源提煉：
1. 過去與 Claude 的對話（存在 `~/.claude/projects/memory/`）
2. Shawn 在 2026-06-29 的自述（工具跳躍循環、AI 團隊願景）
3. SIS_CORE.md 原版（整合並重構）

### 待驗證的 Hypothesis

以下標記為 `[Hypothesis]` 的結論，需要更多觀察才能升格：
- `identity.md`：設計 AI 團隊可能是最大天賦
- `values.md`：低估維護現有系統的時間成本
- `workflow.md`：工作節奏不是朝九晚五，而是集中爆發
- `business.md`：對 AI API 費用敏感度高
- `blindspots.md #4`：低估維護成本
- `blindspots.md #5`：完美主義 vs 出貨速度矛盾

---

## 更新模板

```markdown
## vX.Y.Z — YYYY-MM-DD

### 新增
- `檔案名.md`：[新增的 Fact / Inference / Hypothesis]

### 修正
- `檔案名.md`：~~舊內容~~
  修正為：[新內容]
  原因：[為什麼這個記錄是錯的]

### 升格
- `blindspots.md #X`：[Hypothesis] 升格為 [Inference]
  根據：[觀察到什麼行為]
```
