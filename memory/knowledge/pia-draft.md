# pia-draft.md — Personal Intelligence Architecture 設計草稿

**狀態**：[Hypothesis] 待驗證，SIS v0.1.1 穩定後再推進
**建立**：2026-06-29
**觸發條件**：不要因為這份文件存在就開始建 repo。先讓 SIS 跑一個月。

---

## 核心定位

SIS 是 PIA 的第一個 Reference Implementation。

```
PIA（Framework，方法論）
    │
    ├── SIS（Shawn's implementation）← 目前在做
    ├── Alice OS
    └── Company OS
```

類比：Linux 是 Kernel，Ubuntu 是 Distribution。
PIA 是 Kernel，SIS 是第一個 Distribution。

---

## 為什麼不是 AI Operating System，而是 AI Governance System

OS 只是其中一部分。真正值錢的是：

> **這套系統如何確保所有 AI 做出一致、可驗證、符合你價值觀的決策。**

---

## 六層架構

```
Constitution Layer（治理）
    ↓
Identity Engine
Decision Engine
Knowledge Engine
Execution Engine
    ↓
Validation Layer（驗證系統沒壞）
    ↓
Infrastructure（Claude / Codex / n8n / GitHub...）
    ↓
Products（TeamStar / paopao / VegeNova...）
```

**Constitution Layer**（SIS 目前已有）：
- Principles / Guardrails / Blindspots / Review Protocol / Evolution Protocol

**Validation Layer**（SIS 目前沒有，這是 PIA 新增的）：
- Scenario Tests：給定情境，驗證 AI 回應是否符合預期
- Consistency Tests：跨 session 行為是否一致
- Regression Tests：更新後有沒有壞掉舊行為

---

## 七個設計原則

1. **Evidence First** — 所有結論要有 Evidence，Hypothesis → Validation → Fact
2. **Governance over Intelligence** — AI 再聰明，必須受到治理，否則會漂移
3. **Memory ≠ Identity** — Memory 是 Evidence，Identity 是人格，不要混淆
4. **Decision before Action** — 先問怎麼決策，再做事
5. **Build > Perfect** — 先做出可用版本
6. **Platform Neutral** — Claude / GPT / Gemini 都可以用，不綁定單一工具
7. **Evolution without Drift** — 允許進化，但要能偵測漂移

---

## 閉環數據流

```
Evidence → Review → Constitution → Identity → Decision
    ↑                                               ↓
Results ← Products ← Infrastructure ← Execution ←─┘
```

---

## Validation Layer 場景範例（最重要的新增）

```
場景：Shawn 開始研究一個新 AI 工具
預期：系統問「它完成哪一個產品？」

場景：Shawn 連續三天沒有推進當前任務
預期：系統問「是遇到阻礙，還是在走 blindspot #1？」

場景：有人建議重構整個架構
預期：系統問「這讓 30 天內有什麼東西可以上線？」
```

這些場景就是 SIS 的健康指標。如果 Validation 全部 PASS，代表 SIS 正常運作。

---

## 未來 Repo 結構（到時候才建）

```
pia/
├── README.md
├── ARCHITECTURE.md
├── constitution/
├── identity/
├── decision/
├── knowledge/
├── execution/
├── validation/        ← Scenarios + Tests
├── products/
└── infrastructure/
```

---

## 與 SIS 的關係

| | SIS | PIA |
|---|---|---|
| 定位 | 個人實作 | 通用框架 |
| 現況 | v0.1.1，已在運作 | 草稿，未建 repo |
| 下一步 | 跑 Validation，穩定一個月 | 等 SIS 驗證完再說 |

**PIA 什麼時候才建 repo？**
→ SIS 在三個不同的真實工作情境下都通過 Validation，且沒有重大漂移。
