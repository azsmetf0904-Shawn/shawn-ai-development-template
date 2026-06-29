# Shawn Core — 使用說明

這個目錄是 **Shawn Core**：Shawn 的 AI 協作人格核心與決策規則庫。

## 這是什麼

不是自傳，不是履歷。
是 AI 需要了解的一切，讓每次對話都能從正確的起點開始。

## AI 使用方式

1. **每次新對話開始時**，先讀 `identity.md` + `communication.md`
2. **做決策或規劃前**，讀 `decision.md` + `workflow.md`
3. **商業相關問題**，讀 `business.md`
4. **Shawn 卡住或在走老路時**，參考 `blindspots.md`

不需要每次全讀，按需載入。

## 標記說明

每個結論都標示可信度：

| 標記 | 意義 |
|------|------|
| `[Fact]` | 直接陳述或確認的事實 |
| `[Inference]` | 從行為模式推導，高可信度 |
| `[Hypothesis]` | 假設，需要更多觀察驗證 |

## 更新規則

- 版本更新記在 `changelog.md`
- 發現新的行為模式 → 先加 `[Hypothesis]`，觀察一段時間後升格
- `[Fact]` 被推翻 → 直接修改，在 changelog 記錄原因
- 不要刪除 `[Inference]` 和 `[Hypothesis]`，改為加刪除線並說明

## 同步機制

```
shawn-ai-development-template/memory/  ← 官方版本（此處）
        ↓ 穩定後手動同步
~/.claude/projects/memory/             ← 本機執行版，Claude Code 自動讀取
```
