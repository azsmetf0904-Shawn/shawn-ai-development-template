# review_protocol.md — Sprint 後審查清單

每個 Sprint 結束後，AI 應主動執行這份審查，並把重要變更記錄到 `governance/changelog.md`。

## 1. 目標對齊

- 本 Sprint 完成的工作，是否對應一個明確產品目標？
- 是否違反 Shawn Rule No.1，因工具興奮而偏離原目標？
- 是否符合 Build > Perfect，已經產出可驗證版本，而不是只做規劃或架構？

## 2. 商業與產品

- 新增功能是否解決真實用戶問題？
- 是否改動到計分邏輯、角色權限、付費方案等 Shawn 應親自決策的商業規則？
- 是否有「技術上很酷但用戶感受不到」的工作混入 Sprint？

## 3. 技術與維護

- 是否有新增 workflow、edge function、自動化或排程？如果有，監控與錯誤回報是否清楚？
- 是否有新增長期維護成本？誰會確認它正常運作？
- 是否有必要更新 `TASKS.md`、`DECISIONS.md`、README 或相關操作文件？

## 4. 盲點檢查

- 是否出現工具跳躍循環？
- 是否架構先於產品？
- 是否因多專案並行讓當前 Sprint 失焦？
- 是否低估維護成本？
- 是否因完美主義延後出貨？

## 5. 記憶更新

- 是否觀察到新的 `[Hypothesis]`？
- 是否有 `[Hypothesis]` 可以升格為 `[Inference]` 或 `[Fact]`？
- 是否有既有 `[Fact]` 被推翻，需要修正並記錄原因？
- 是否需要更新 `governance/changelog.md`？
