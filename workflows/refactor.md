# Workflow：重構 SOP

在不改變功能行為的前提下，改善程式碼結構的流程。

---

## 重構原則

1. **功能不變**：重構前後，用戶看到的行為完全一樣
2. **小步前進**：每次只改一件事，不要一次大改
3. **有測試保護**：重構前先確認有測試，或至少手動測試 checklist
4. **有明確理由**：不要為了「感覺更乾淨」而重構，要有具體的改善目標

---

## 什麼時候該重構？

**應該重構的情況**：
- 同一段邏輯在三個以上地方重複（Rule of Three）
- 函式超過 100 行，已經難以理解
- 加新功能時，現有架構讓實作很困難
- 發現 Bug 的根因是結構問題，不是單純的邏輯錯誤

**不應該現在重構的情況**：
- 快要發版，沒有時間驗證
- 這段程式碼很少被改到
- 只是「感覺不好看」，但沒有具體問題

---

## Step 1：明確重構目標

在開始之前，填寫這個表：

```markdown
重構對象：[檔案名稱或函式名稱]
目前的問題：[具體描述什麼讓你難以維護]
重構後的改善：[重構後會有什麼不同]
不會改變的行為：[什麼功能重構後必須保持一樣]
```

---

## Step 2：確認測試覆蓋

```bash
# 如果有測試，先跑一次確認現在是 pass 的
npm test

# 如果沒有測試，手動列出需要測試的情況：
# - [情況 1]
# - [情況 2]
```

---

## Step 3：請 Claude 分析現有程式碼

```
請分析以下程式碼的結構問題，並提出重構建議。

目前的問題（我觀察到的）：[說明]

程式碼：
[貼入程式碼]

請回應：
1. 你確認的結構問題（可能比我觀察到的更多）
2. 重構方向建議（2 個選項）
3. 建議哪個方向，理由是什麼
4. 哪些部分在重構時最容易出錯（需要特別小心）
```

---

## Step 4：小步實作

每次只做一個改動，不要一次改太多：

```bash
# 範例：先把函式提取出來
# commit 1：提取 [functionName] 函式，行為不變
git commit -m "refactor: 提取 [functionName]，行為不變"

# 確認還是正常後，再做下一步
# commit 2：重組 [moduleName] 的結構
git commit -m "refactor: 重組 [moduleName] 結構"
```

---

## Step 5：驗證行為不變

每個 commit 後都要驗證：

```bash
# 如果有測試
npm test

# 如果是手動測試，走一遍 checklist：
# - [ ] [情況 1] 正常
# - [ ] [情況 2] 正常
# - [ ] [主要流程] 正常
```

---

## Step 6：程式碼審查

用 `prompts/review.md` 請 Claude 審查重構結果，特別關注：

- 重構是否真的簡化了邏輯？
- 有沒有不小心改到行為？
- 命名是否更清楚了？

---

## 常見重構模式

### 提取重複邏輯

```javascript
// 重構前：三個地方都有同樣的計算
const aScore = tasks.filter(t => t.status === 'approved').reduce((sum, t) => sum + t.points, 0)
const bScore = tasks.filter(t => t.status === 'approved').reduce((sum, t) => sum + t.points, 0)

// 重構後：提取成函式
const calcApprovedPoints = (tasks) =>
  tasks.filter(t => t.status === 'approved').reduce((sum, t) => sum + t.points, 0)
```

### 簡化條件邏輯

```javascript
// 重構前：巢狀 if
if (user) {
  if (user.is_admin) {
    if (user.active) {
      // ...
    }
  }
}

// 重構後：Early return
if (!user || !user.is_admin || !user.active) return null
// ...
```

### 分離 UI 和業務邏輯

```javascript
// 重構前：在 component 裡直接計算
function ScoreBoard() {
  const [tasks, setTasks] = useState([])
  // 一大堆計算邏輯...

// 重構後：計算邏輯移到 lib/
// lib/scoreUtils.js
export const calcGroupRanking = (tasks, groups) => { ... }

// ScoreBoard.js
function ScoreBoard() {
  const ranking = calcGroupRanking(tasks, groups)
```
