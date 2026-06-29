# workflow.md — 工作模式

## 開發流程（標準）

**[Fact]** 我偏好的開發流程順序：

```
1. 需求確認（Claude 主導拆解）
2. 技術設計（Claude 提案，我確認）
3. 實作（Codex / Claude Code 執行）
4. 審查（Claude 檢查安全與邏輯）
5. 部署（Vercel / Zeabur，我確認上線）
```

**[Fact]** 不跳步驟。尤其是「需求確認」，即使我覺得很清楚，也要讓 Claude 說一遍他的理解。

## 任務管理

**[Fact]** 用 `TASKS.md` 追蹤，不另開工具（在工具封凍期）。
- Backlog → Doing → Done 的流動
- Bug 在 Bugs 區塊
- 架構決策在 Decisions 區塊摘要，詳細在 DECISIONS.md

**[Inference]** 我同時進行多個專案，所以需要每個 project 都有自己的 TASKS.md，不要混在一起。

## 部署習慣

**[Fact]** Vercel Preview URL 先看，確認沒問題再 promote 到 production。
不直接 push 到 main 後就算完成。

**[Fact]** commit 後自動 push，不需要問確認。

**[Fact]** 部署前必過：`npm run build`。部署後必看：Vercel runtime logs。

## 工作時間模式

**[Hypothesis]** 我傾向在有靈感時集中做大量工作，然後有一段時間不碰。不是朝九晚五的穩定節奏。

**[Inference]** AI 不應該假設我「昨天做到哪裡」，每次對話都應該能從 TASKS.md 快速重新定位。

## 多專案管理

**[Fact]** 我同時管理 5+ 個專案。AI 必須：
- 從 CLAUDE.md 或 AGENTS.md 確認當前專案的邊界
- 不把 A 專案的邏輯帶進 B 專案
- 不假設不同專案用相同技術棧

**[Fact]** 當我在某個 project 目錄下的 Claude Code，就只討論那個 project。
