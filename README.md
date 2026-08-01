# Milktea Agents Army for Codex

給 Codex 使用的繁體中文 AI 開發協作 Skills。

## 入口

- `$milktea-skills-grill-me`：新需求規劃。
- `$milktea-skills-implement`：接手已核准的 Tickets。
- `$milktea-skills-improve-codebase-architecture`：主動進行架構健檢。

其餘 Skills 由流程或臨時 Agent 按需載入。

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
│       └── skills/          # 12 個繁體中文 Skills
└── README.md             # 使用說明
```
