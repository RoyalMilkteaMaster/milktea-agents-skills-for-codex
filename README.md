# Milktea Agents Army for Codex

這是皇家奶茶大師給 Claude Code 使用的 AI 開發協作 Skills。

你會用到的技能只有四個。
平常你只需要依照你的需求使用技能或是輸入範本。  
後續需要的規劃、實作、測試與 Review Skills 都會由流程接手。

## 先選你現在要做的事

```text
你現在想做什麼？
│
├─ 開始新專案，或替正常的專案新增功能
│  └─ grill-me
│
├─ 想先看懂混亂的舊專案，再決定是否要重構
│  └─ brownfield-refactor-planner
│
├─ 還不確定一個想法能不能做、值不值得做
│  └─ check-feasibility
│
└─ 想更換目前執行 Task 的 Developer 或 Reviewer
   └─ set-agent-roles
```

| 你的情況 | 使用 Skill | 產出 | 會修改程式嗎？ |
|---|---|---|---|
| 新專案或新增功能 | `grill-me` | 需求、架構、Spec、Tickets 與執行交接 | 不會 |
| 評估或整理既有混亂專案 | `brownfield-refactor-planner` | 先產生架構報告；你決定繼續後才產生重構 Spec、Tickets 與執行交接 | 不會 |
| 評估想法能不能做 | `check-feasibility` | 可行性、成本、時間與風險報告 | 不會 |
| 更換目前 Task 的開發與審查角色 | `set-agent-roles` | 本 Task 的 Developer 與雙 Reviewer 設定 | 不會 |

`implement` 不需要自己記指令。Grill Me 或 Brownfield Planner 完成後，會產生一段完整交接內容；Codex Desktop 可以在你授權後建立新的執行 Task，也可以把交接內容貼到新的 Codex Task。

## 奶茶流怎麼運作

### 新專案或新增功能

```text
想法
  ↓
Grill Me
  ↓
確認需求 → 確認架構 → 寫 Spec → 拆 Tickets
  ↓
產生執行交接內容
  ↓
建立新的 Codex Task
  ↓
Implement → Developer 實作 → Reviewer A + Reviewer B 獨立審查
```

### 整理既有專案

```text
混亂或需要重構的舊專案
  ↓
Brownfield Refactor Planner
  ↓
內部呼叫 Architecture Auditor
  ↓
HTML 架構報告
  ├─ 只需要報告 → 到此結束
  └─ 決定重構
       ↓
     確認目標架構 → 重構 Spec → Tickets
       ↓
     產生執行交接內容
       ↓
     建立新的 Codex Task 執行重構
```

## 四個主要入口

### 1. 開始新專案或新增功能

使用 `$milktea-skills-grill-me`。

它會依序跟你確認需求與架構，再寫成 Spec、拆成 Tickets。它只負責規劃，不會在同一個 Task 直接寫程式。

如果舊專案已經明顯混亂，先使用 Brownfield Planner，不要一邊整理舊架構、一邊規劃新功能。

<details>
<summary>可直接複製的用法</summary>

```text
我要開發一個＿＿＿＿專案／新增＿＿＿＿功能。

目前已知需求：
- ＿＿＿＿
- ＿＿＿＿

請使用：
$milktea-skills-grill-me

先跟我確認需求與架構，再產生 Spec、Tickets 和執行交接。現在不要直接寫程式。
```

</details>

### 2. 整理或重構既有專案

使用 `$milktea-skills-brownfield-refactor-planner`。

適合架構混亂、重複程式增加、舊功能殘留，或你還不確定這個專案是否值得重構。

它會先呼叫內部的架構健檢 Skill，用唯讀方式盤點現況並產生 HTML 報告。你可以拿到報告就結束；只有明確選擇繼續，才會確認目標架構、產生重構 Spec 與 Tickets。整個 Planner 不會直接修改或刪除程式。

<details>
<summary>可直接複製的用法</summary>

```text
我的專案已經開發一段時間，現在有以下問題：
- ＿＿＿＿
- ＿＿＿＿

必須保留的功能：
- ＿＿＿＿

請使用：
$milktea-skills-brownfield-refactor-planner

先盤點現況、架構、資料流與清理風險，產生 HTML 架構報告讓我判斷。等我決定繼續後，才產生重構 Spec 與 Tickets。現在不要直接修改或刪除程式。
```

</details>

### 3. 先確認想法能不能做

使用 `$milktea-skills-check-feasibility`。

適合在投入開發前，先確認技術能力、外部依賴、成本、時間、風險與成功機率。它只產生評估報告，不會自動開始規劃或實作。

<details>
<summary>可直接複製的用法</summary>

```text
我想做＿＿＿＿，但還不確定是否可行或值得投入。

我的環境與限制：
- ＿＿＿＿
- ＿＿＿＿

請使用：
$milktea-skills-check-feasibility

查證後評估技術可行性、成本、時間、主要風險與最小驗證方式。不要修改程式。
```

</details>

### 4. 更換 Developer 與 Reviewer

使用 `$milktea-skills-set-agent-roles`。

只有想改變預設分工時才需要。它只設定目前 Task 的 Developer、Reviewer A 與 Reviewer B，不會開始派工，也不會影響其他 Task。

請在實際執行 Tickets 的 Task 中使用，並在下一張 Ticket 尚未派發前完成設定。

<details>
<summary>可直接複製的用法</summary>

```text
請使用：
$milktea-skills-set-agent-roles

幫我設定目前 Task 的 Developer、Reviewer A 與 Reviewer B。只設定角色，先不要開始派工。
```

</details>

## 其他 Skills

`improve-codebase-architecture` 是 Brownfield Planner 內部使用的架構報告產生器；`implement` 與 `brownfield-refactor-implement` 由規劃完成後的交接內容啟動。其餘 Skills 負責需求確認、架構設計、Spec、Tickets、TDD、Debug、Code Review 與 Git 衝突處理，由流程或執行 Agent 按需載入。

一般使用者不需要逐一呼叫，也不需要記住名稱。

## 快速開始

此 Repository 為 Public，不需要先登入 GitHub。請先安裝 [Codex CLI](https://learn.chatgpt.com/docs/codex/cli)（`codex`）。

請選擇實際要使用 Codex 的環境，並在同一個環境完成以下所有步驟。

如果 `codex login status` 已顯示登入成功，可以略過登入命令。

### Windows（新手推薦）

在 PowerShell 執行：

```powershell
codex login
codex login status

codex plugin marketplace add RoyalMilkteaMaster/milktea-agents-army-codex
codex plugin add milktea-agents-army-codex@milktea-agents-army-codex
codex plugin list
```

### Linux／WSL（長期開發者推薦）

在 Linux／WSL Terminal 執行：

```bash
codex login
codex login status

codex plugin marketplace add RoyalMilkteaMaster/milktea-agents-army-codex
codex plugin add milktea-agents-army-codex@milktea-agents-army-codex
codex plugin list
```

Windows 與 WSL 是兩個獨立環境。在 Windows 完成的 Codex 登入與 Plugin 安裝，不會自動套用到 WSL；反之亦然。

Plugin 安裝完成後，請開啟新的 Codex Task。Milktea Skills 將套用至該使用者在此環境中的所有專案，不需要 Clone Repository、不需要設定專案路徑，也不需要再次安裝。

## 多 Agent 協作（推薦）

Milktea Skills 支援 Developer、Reviewer A 與 Reviewer B 等多個 Agent 協作。只使用 Codex 也能執行；若同時使用不同 AI CLI，通常能獲得更好的交叉驗證，並降低單一模型的盲點。

建議先選定 **Windows** 或 **Linux／WSL**，再把要使用的 AI CLI 全部安裝並登入在同一個環境。不要把 Codex 裝在 Windows、Claude Code 或 Antigravity CLI 裝在 WSL，因為目前執行工作流的 Terminal 只能使用該環境中可找到的 CLI。

若已安裝 [Claude Code](https://code.claude.com/docs/en/overview) 與 [Antigravity CLI](https://antigravity.google/docs/cli-getting-started)，請在剛才同一個 Terminal 執行：

```shell
# Claude Code
claude auth login
claude auth status

# Antigravity CLI
agy
```

Antigravity CLI 沒有另外的 `auth login` 指令。第一次執行 `agy` 時會開啟 Google 登入流程；完成後可在 Antigravity CLI 輸入 `/exit` 回到 Terminal。

如果電腦上有兩種以上的 AI CLI，建議全部登入。工作流只會使用目前環境中實際可用的 CLI。

完成後，在新的 Codex Task 中使用 Plugin Skill：

```text
$milktea-skills-grill-me
```

Plugin 安裝後，即可在該環境的所有專案使用，並完整保留工作流需要的相依 Skills。
