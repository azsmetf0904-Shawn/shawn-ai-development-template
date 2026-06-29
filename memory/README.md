# Shawn Core — 使用說明

這個目錄是 **Shawn Core**：Shawn 的 AI 協作人格核心與決策規則庫。

## 這是什麼

不是自傳，不是履歷。
是 AI 需要了解的一切，讓每次對話都能從正確的起點開始。

## AI 使用方式

1. **每次新對話開始時**，先讀 `identity/identity.md` + `identity/communication.md`
2. **做決策或規劃前**，讀 `governance/constitution.md` + `decision/decision.md` + `execution/workflow.md`
3. **商業相關問題**，讀 `knowledge/business.md`
4. **Shawn 卡住或在走老路時**，參考 `governance/blindspots.md`
5. **每個 Sprint 結束後**，依 `governance/review_protocol.md` 審查，必要時更新 `governance/changelog.md`

不需要每次全讀，按需載入。

## 目錄結構

```text
memory/
├── governance/
│   ├── constitution.md      # 核心 policy、Shawn Rule No.1、AI 協作治理
│   ├── blindspots.md        # 已知盲點與高風險模式
│   ├── review_protocol.md   # Sprint 後 AI 審查清單
│   └── changelog.md         # Shawn Core 版本記錄
├── identity/
│   ├── identity.md          # Shawn 的身份、能力輪廓、思維風格
│   ├── values.md            # 個人時間與精力價值觀
│   └── communication.md     # 溝通偏好
├── decision/
│   └── decision.md          # 決策風格與建議格式
├── execution/
│   └── workflow.md          # 開發 SOP、任務管理、部署習慣
├── knowledge/
│   └── business.md          # 商業背景與產品策略
└── README.md
```

## 標記說明

每個結論都標示可信度：

| 標記 | 意義 |
|------|------|
| `[Fact]` | 直接陳述或確認的事實 |
| `[Inference]` | 從行為模式推導，高可信度 |
| `[Hypothesis]` | 假設，需要更多觀察驗證 |

## 更新規則

- 版本更新記在 `governance/changelog.md`
- 發現新的行為模式 → 先加 `[Hypothesis]`，觀察一段時間後升格
- `[Fact]` 被推翻 → 直接修改，在 changelog 記錄原因
- 不要刪除 `[Inference]` 和 `[Hypothesis]`，改為加刪除線並說明

## 同步機制

```
shawn-ai-development-template/memory/  ← 官方版本（此處）
        ↓ 穩定後手動同步
~/.claude/projects/memory/             ← 本機執行版，Claude Code 自動讀取
```
