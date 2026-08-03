# Milktea Agents Army for Codex

給 Codex 使用的繁體中文 AI 開發協作 Skills。

你不需要記住全部 15 個 Skills。平常只要依照目前情況選擇入口，後續流程會載入需要的內部 Skills。

## 四個主要入口

| 你的情況 | 使用 Skill | 產出 |
|---|---|---|
| 開始新專案或新增功能 | `$milktea-skills-grill-me` | 需求、架構、Spec、Tickets 與執行交接 |
| 評估或整理既有混亂專案 | `$milktea-skills-brownfield-refactor-planner` | 先產生架構報告；你決定繼續後才產生重構 Spec、Tickets 與執行交接 |
| 評估想法能不能做 | `$milktea-skills-check-feasibility` | 可行性、成本、時間與風險報告 |
| 更換目前 Task 的開發與審查角色 | `$milktea-skills-set-agent-roles` | 本 Task 的 Developer 與雙 Reviewer 設定 |

`improve-codebase-architecture` 是 Brownfield Planner 內部使用的架構報告產生器。`implement` 與 `brownfield-refactor-implement` 由 Planner 產生的交接內容啟動，不需要平常自己呼叫。

### Brownfield 流程

```text
混亂或需要評估的舊專案
  ↓
Brownfield Refactor Planner
  ↓
HTML 架構報告
  ├─ 只需要報告 → 到此結束
  └─ 決定重構 → 目標架構 → Spec → Tickets → 執行交接
```

Spec 與 Tickets 預設寫入 `docs/work/`，不需要 GitHub、Commit 或 Push。Tickets 核准後，Codex Desktop 會在使用者授權時建立新的執行 Task。

## 安裝

Windows：

```powershell
codex plugin marketplace add D:\workstationD\milktea-agents-army-codex
codex plugin add milktea-agents-army-codex@milktea-agents-army-codex
```

安裝或更新後，請開新 Task，讓 Codex 重新載入 Skills。

## 結構

```text
milktea-agents-army-codex/  # Codex 發行包
├── .agents/plugins/        # Repo-local Marketplace 設定
│   └── marketplace.json  # Codex Marketplace 定義
├── plugins/                # 可安裝的 Plugin 集合
│   └── milktea-agents-army-codex/  # 實際 Plugin
│       ├── .codex-plugin/           # Codex Plugin 設定
│       │   └── plugin.json  # Codex Plugin 定義
│       └── skills/          # 15 個繁體中文 Skills
└── README.md             # 使用說明
```
