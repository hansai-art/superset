<div align="center">

<img width="full" alt="Superset" src="apps/marketing/public/images/readme-hero.png" />

### 給 AI 代理人的程式碼編輯器

[![GitHub stars](https://img.shields.io/github/stars/superset-sh/superset?style=flat&logo=github)](https://github.com/superset-sh/superset/stargazers)
[![GitHub release](https://img.shields.io/github/v/release/superset-sh/superset?style=flat&logo=github)](https://github.com/superset-sh/superset/releases)
[![License](https://img.shields.io/github/license/superset-sh/superset?style=flat)](LICENSE.md)
[![Twitter](https://img.shields.io/badge/@superset__sh-555?logo=x)](https://x.com/superset_sh)
[![Discord](https://img.shields.io/badge/Discord-555?logo=discord)](https://discord.gg/cZeD9WYcV7)

<br />

可同時編排多個 Claude Code、Codex 等代理人平行工作。<br />
相容任何 CLI 代理人，並為本機 worktree 開發流程打造。

<br />

[**下載 macOS 版本**](https://github.com/superset-sh/superset/releases/latest) &nbsp;&bull;&nbsp; [文件](https://docs.superset.sh) &nbsp;&bull;&nbsp; [更新日誌](https://github.com/superset-sh/superset/releases) &nbsp;&bull;&nbsp; [Discord](https://discord.gg/cZeD9WYcV7)

<br />


</div>

## 不用切換上下文，也能讓開發速度提升 10 倍

Superset 讓你在「隔離的 git worktree」中同時驅動多個 CLI 程式代理人，並內建終端機、差異檢視、快速回編輯器等流程。

就算你是新手，也可以把它理解成：

- 一個代理人 = 一位幫你寫程式的助手
- 一個 worktree = 一個獨立工作桌，不會互相打架
- Superset = 你管理所有助手的控制台

你可以做到：

- **同時跑多個代理人**，不用一直切來切去
- **每個任務各自隔離**，避免改壞彼此的檔案
- **在同一個地方監控狀態**，代理人需要你時會通知
- **用內建 diff 快速審查與微調**，減少來回開關工具
- **一鍵把任務工作區交給編輯器或終端機**，延續你的原本習慣

等待更少，交付更多。

## 功能特色

| 功能 | 說明 |
|:--------|:------------|
| **平行執行（Parallel Execution）** | 在同一台機器同時跑 10 個以上代理人 |
| **Worktree 隔離（Worktree Isolation）** | 每個任務都有獨立分支與工作目錄 |
| **代理人監控（Agent Monitoring）** | 追蹤任務狀態，修改完成時可即時得知 |
| **內建差異檢視（Built-in Diff Viewer）** | 不離開 App 也能檢查、編修代理人的變更 |
| **工作區預設（Workspace Presets）** | 自動化環境初始化、安裝依賴等步驟 |
| **通用相容（Universal Compatibility）** | 任何能在終端機運作的 CLI 代理人都可使用 |
| **快速切換上下文（Quick Context Switching）** | 任務需要你時再進去處理，不被流程綁住 |
| **IDE 整合（IDE Integration）** | 一鍵在你慣用編輯器打開該工作區 |

## 支援的代理人

Superset 支援任何「CLI 型」程式代理人，包含：

| 代理人 | 狀態 |
|:------|:-------|
| [Amp Code](https://ampcode.com/) | 完整支援 |
| [Claude Code](https://github.com/anthropics/claude-code) | 完整支援 |
| [OpenAI Codex CLI](https://github.com/openai/codex) | 完整支援 |
| [Cursor Agent](https://docs.cursor.com/agent) | 完整支援 |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | 完整支援 |
| [GitHub Copilot](https://github.com/features/copilot) | 完整支援 |
| [OpenCode](https://github.com/opencode-ai/opencode) | 完整支援 |
| [Pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) | 完整支援 |
| 其他 CLI 代理人 | 多半可運作 |

一句話：只要它能在終端機跑，就能在 Superset 跑。

## 執行需求

| 需求項目 | 說明 |
|:------------|:--------|
| **作業系統** | macOS（Windows/Linux 尚未完整測試） |
| **Runtime** | [Bun](https://bun.sh/) v1.0+ |
| **版本控制** | Git 2.20+ |
| **GitHub CLI** | [gh](https://cli.github.com/) |
| **Caddy** | [caddy](https://caddyserver.com/docs/install)（開發伺服器需要） |

## 快速開始

### 方式一：直接下載（最推薦新手）

**[下載 Superset for macOS](https://github.com/superset-sh/superset/releases/latest)**

### 方式二：從原始碼建置（給想客製化或貢獻程式碼的人）

<details>
<summary>點我展開建置步驟</summary>

**1. 複製專案原始碼（clone）**

```bash
git clone https://github.com/superset-sh/superset.git
cd superset
```

**2. 設定環境變數**（二選一）

方案 A：完整設定（正式開發建議）
```bash
cp .env.example .env
# 開啟 .env 並填入對應值
```

方案 B：略過環境驗證（只想快速本機試跑）
```bash
cp .env.example .env
echo 'SKIP_ENV_VALIDATION=1' >> .env
```

**3. 設定 Caddy**（給 Electric SQL stream 的反向代理）

```bash
# 安裝 caddy：macOS 可用 brew install caddy
# 其他平台請看官方文件：https://caddyserver.com/docs/install
cp Caddyfile.example Caddyfile

# 若不執行這一步，Chromium 可能拒絕 https://localhost:* 憑證（ERR_CERT_AUTHORITY_INVALID）
# 這一步會要求一次 sudo 權限
caddy trust
```

**4. 安裝依賴並啟動開發模式**

```bash
bun install
bun run dev
```

**5. 建置桌面版 App**

```bash
bun run build
open apps/desktop/release
```

</details>

## 鍵盤快捷鍵

所有快捷鍵都可在 **Settings > Keyboard Shortcuts**（`⌘/`）客製化。更多內容可看[完整文件](https://docs.superset.sh/keyboard-shortcuts)。

### 工作區切換

| 快捷鍵 | 動作 |
|:---------|:-------|
| `⌘1-9` | 切換到第 1～9 個工作區 |
| `⌘⌥↑/↓` | 上一個／下一個工作區 |
| `⌘N` | 新增工作區 |
| `⌘⇧N` | 快速建立工作區 |
| `⌘⇧O` | 開啟專案 |

### 終端機

| 快捷鍵 | 動作 |
|:---------|:-------|
| `⌘T` | 新分頁 |
| `⌘W` | 關閉窗格／終端機 |
| `⌘D` | 向右分割 |
| `⌘⇧D` | 向下分割 |
| `⌘K` | 清空終端機 |
| `⌘F` | 在終端機中搜尋 |
| `⌘⌥←/→` | 上一個／下一個分頁 |
| `Ctrl+1-9` | 開啟第 1～9 個預設 |

### 版面配置

| 快捷鍵 | 動作 |
|:---------|:-------|
| `⌘B` | 顯示／隱藏工作區側欄 |
| `⌘L` | 顯示／隱藏變更面板 |
| `⌘O` | 用外部 App 開啟 |
| `⌘⇧C` | 複製路徑 |

## 設定檔（Configuration）

你可以在 `.superset/config.json` 設定建立／刪除工作區時要自動做的事情。詳見[完整文件](https://docs.superset.sh/setup-teardown-scripts)。

```json
{
  "setup": ["./.superset/setup.sh"],
  "teardown": ["./.superset/teardown.sh"]
}
```

| 選項 | 型別 | 說明 |
|:-------|:-----|:------------|
| `setup` | `string[]` | 建立工作區時執行的指令 |
| `teardown` | `string[]` | 刪除工作區時執行的指令 |

### setup 腳本範例

```bash
#!/bin/bash
# .superset/setup.sh

# 複製環境變數
cp ../.env .env

# 安裝依賴
bun install

# 其他初始化工作
echo "Workspace ready!"
```

腳本可以使用以下環境變數：
- `SUPERSET_WORKSPACE_NAME` — 工作區名稱
- `SUPERSET_ROOT_PATH` — 主專案路徑

## Mastra 依賴說明

本專案直接使用官方發布的 `mastracode` 與 `@mastra/*` 套件。除非有專案內特定阻礙，否則請避免加入自製 tarball 覆寫。

## 技術堆疊

<p>
  <a href="https://www.electronjs.org/"><img src="https://img.shields.io/badge/Electron-191970?logo=Electron&logoColor=white" alt="Electron" /></a>
  <a href="https://reactjs.org/"><img src="https://img.shields.io/badge/React-%2320232a.svg?logo=react&logoColor=%2361DAFB" alt="React" /></a>
  <a href="https://tailwindcss.com/"><img src="https://img.shields.io/badge/Tailwindcss-%2338B2AC.svg?logo=tailwind-css&logoColor=white" alt="TailwindCSS" /></a>
  <a href="https://bun.sh/"><img src="https://img.shields.io/badge/Bun-000000?logo=bun&logoColor=white" alt="Bun" /></a>
  <a href="https://turbo.build/"><img src="https://img.shields.io/badge/Turborepo-EF4444?logo=turborepo&logoColor=white" alt="Turborepo" /></a>
  <a href="https://vitejs.dev/"><img src="https://img.shields.io/badge/Vite-%23646CFF.svg?logo=vite&logoColor=white" alt="Vite" /></a>
  <a href="https://biomejs.dev/"><img src="https://img.shields.io/badge/Biome-339AF0?logo=biome&logoColor=white" alt="Biome" /></a>
  <a href="https://orm.drizzle.team/"><img src="https://img.shields.io/badge/Drizzle%20ORM-FFE873?logo=drizzle&logoColor=black" alt="Drizzle ORM" /></a>
  <a href="https://neon.tech/"><img src="https://img.shields.io/badge/Neon-00E9CA?logo=neon&logoColor=white" alt="Neon" /></a>
  <a href="https://trpc.io/"><img src="https://img.shields.io/badge/tRPC-2596BE?logo=trpc&logoColor=white" alt="tRPC" /></a>
</p>

## 預設重視隱私

- **Source Available**：完整原始碼依 Elastic License 2.0（ELv2）公開於 GitHub。
- **Explicit Connections**：你可以自行決定要連哪些代理人、模型供應商與整合服務。

## 如何貢獻

歡迎貢獻！如果你有能讓 Superset 更好的想法：

1. Fork 此倉庫
2. 建立功能分支（`git checkout -b feature/amazing-feature`）
3. 提交修改（`git commit -m 'Add amazing feature'`）
4. 推送分支（`git push origin feature/amazing-feature`）
5. 開啟 Pull Request

你也可以在 [issues](https://github.com/superset-sh/superset/issues) 回報 bug 或提出功能建議。

更多細節請看 [CONTRIBUTING.md](CONTRIBUTING.md)。

<a href="https://github.com/superset-sh/superset/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=superset-sh/superset" />
</a>

## 社群

加入 Superset 社群，取得協助、分享回饋並和其他使用者交流：

- **[Discord](https://discord.gg/cZeD9WYcV7)** — 與團隊和社群即時聊天
- **[Twitter](https://x.com/superset_sh)** — 追蹤最新更新與公告
- **[GitHub Issues](https://github.com/superset-sh/superset/issues)** — 回報問題與提出功能需求
- **[GitHub Discussions](https://github.com/superset-sh/superset/discussions)** — 發問、交流想法與用法
