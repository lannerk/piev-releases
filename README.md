<p align="center">
  <img src="https://raw.githubusercontent.com/lannerk/piev-releases/main/assets/piev-logo-256.png" alt="PiEv" width="128">
</p>

<h1 align="center">PiEv</h1>

<p align="center">
  会自我演进的桌面 coding agent：按项目装上它需要的插件、技能、MCP 和模型，在日常使用中发现自己的不足并改进。<br>
  <sub>PiEv (Pi + Evolve) — a self-evolving desktop coding agent built on <a href="https://github.com/earendil-works/pi">Pi</a>.</sub>
</p>

<p align="center">
  <a href="https://github.com/lannerk/piev-releases/releases/latest"><img alt="release" src="https://img.shields.io/github/v/release/lannerk/piev-releases?color=0AAC13"></a>
  <a href="https://github.com/lannerk/piev-releases/releases"><img alt="downloads" src="https://img.shields.io/github/downloads/lannerk/piev-releases/total?color=3066CF"></a>
  <img alt="platforms" src="https://img.shields.io/badge/platforms-Windows%20%7C%20macOS%20%7C%20Linux-27A57F">
  <a href="EULA.md"><img alt="license" src="https://img.shields.io/badge/license-EULA-lightgrey"></a>
</p>

> 这是 PiEv 的**发行仓**：安装包、更新清单、版本说明、问题反馈都在这里。源码不公开。基于 Pi，非 Pi 官方项目。
> 出品：innocraft.ai（元枢造物）。

## 目录

- [PiEv 是什么](#piev-是什么)
- [下载](#下载)
- [安装](#安装)
- [第一次启动](#第一次启动)
- [使用教程](#使用教程)
- [Demo](#demo)
- [更新](#更新)
- [校验下载](#校验下载)
- [版本与发布日期](#版本与发布日期)
- [反馈](#反馈)
- [许可](#许可)

## PiEv 是什么

PiEv 把 [Pi](https://github.com/earendil-works/pi) 这个 coding agent 装进一个桌面应用，并在它外面加了三层：

| | |
|---|---|
| **按项目选能力** | 打开一个项目，PiEv 按项目类型自动装上它需要的扩展、skills、MCP 服务器和模型档位（T1 / T2 / T3，可在设置里改） |
| **多 agent** | 一个任务可以拆给多个子 agent 并行；Agent 树面板看得到谁在做什么 |
| **自我演进** | 回合结束后看自己哪里卡了（同一个工具连续失败、你中途打断……），提出改进提案；经你批准后把产物（扩展 / skill / 面板）热加载进来，变差了自动禁用、可回滚 |
| **一个窗口里的工作台** | 聊天、文件、改动（真 `git diff`）、终端、内置浏览器（真网页，可缩放）、预览（PDF / 图片 / Office）、ComfyUI 出图、桌面操控（白名单、每次确认）全在一个窗口 |
| **164 套界面风格** | 设置或右下角快速面板里一键换风格，透明度可调，深浅两套 |
| **插话不丢任务** | agent 跑着的时候直接打字：Enter 在下一个安全边界插进去，Shift+Enter 排到本轮之后 |
| **模型** | DeepSeek、OpenRouter、OpenAI、Anthropic、Google、xAI、Mistral、Groq、Moonshot、智谱、MiniMax 等 16 家云端 + 本机 Ollama + 自定义端点；key 只进系统钥匙串 |

## 下载

最新版在 [Releases](https://github.com/lannerk/piev-releases/releases/latest)：

| 平台 | 文件 | 说明 |
|---|---|---|
| Windows 10 / 11 x64 | `PiEv_<版本>_x64-setup.exe` | 推荐；装到用户目录，不需要管理员 |
| Windows 10 / 11 x64 | `PiEv_<版本>_x64_en-US.msi` | 企业分发 / 静默安装 |
| macOS Apple Silicon | `PiEv_<版本>_aarch64.dmg` | *跟进中* |
| macOS Intel | `PiEv_<版本>_x64.dmg` | *跟进中* |
| Linux x64 | `PiEv_<版本>_amd64.AppImage` / `.deb` | *跟进中* |

机器可读的更新清单：[`manifests/piev.json`](manifests/piev.json)（与 Release 上的 `latest.json` 同内容）。

**系统要求**：Windows 需要 [WebView2 运行时](https://developer.microsoft.com/microsoft-edge/webview2/)（Win 11 自带，Win 10 安装器会自动装）；PiEv 自带 Node 运行时，不用另外装 Node。

## 安装

### Windows

1. 下载 `PiEv_<版本>_x64-setup.exe`，双击。
2. SmartScreen 提示「Windows 已保护你的电脑」→ 「更多信息」→「仍要运行」（PiEv 目前没有买代码签名证书；安装包有 minisign 签名，见 [校验下载](#校验下载)）。
3. 一路下一步，完成后桌面和开始菜单都有 PiEv。

静默安装：`PiEv_<版本>_x64-setup.exe /S`，或 `msiexec /i PiEv_<版本>_x64_en-US.msi /qn`。

### macOS（跟进中）

打开 `.dmg`，把 PiEv 拖进「应用程序」。还没有 Apple 公证，第一次启动要在「系统设置 › 隐私与安全性」里点「仍要打开」。

### Linux（跟进中）

```bash
chmod +x PiEv_<版本>_amd64.AppImage && ./PiEv_<版本>_amd64.AppImage
# 或
sudo apt install ./PiEv_<版本>_amd64.deb
```

## 第一次启动

1. **选一个模型**：引导页列出各家；填 key（只进系统钥匙串，不落文件）。本机有 Ollama 的话选「本地」，PiEv 会探测 `127.0.0.1:11434`。
2. **打开一个项目**：选目录；PiEv 识别项目类型并装上对应能力，能力面板里能看到装了什么、为什么。
3. **说第一句话**：左边聊天框打字，agent 要写文件、跑命令时会按你设的权限先问。

不想先配 key：引导页有「稍后」，可以先看界面与风格。

## 使用教程

### 窗口布局

```
┌ 标题栏：项目 · 分支 · 模式（AI / IDE / Git） · 搜索 · 通知 · 设置 ───────────────┐
│ 侧栏      │ 聊天 / 编辑器                     │ 右栏：文件 · 改动 · 浏览器 · 预览 … │
│ 任务列表  │                                   │                                     │
│           ├───────────────────────────────────┤                                     │
│           │ 终端 · 预览（可铺满）              │                                     │
└───────────┴───────────────────────────────────┴─────────────────────────────────────┘
                                                              ┊ 右下角：快速设置（风格 / 外观 / 透明度）
```

### 聊天

| 操作 | 作用 |
|---|---|
| Enter（agent 空闲） | 发送 |
| Enter（agent 运行中） | **插话**：在下一个安全边界交给 agent；正在跑的工具会被停掉，任务不丢 |
| Shift+Enter（运行中） | 排到本轮结束之后 |
| Alt+Enter | 换行 |
| Ctrl+Enter | 中断当前并立刻发送 |
| Esc | 中断 |
| Ctrl+K | 命令面板 |
| `/piev …` | PiEv 自己的命令（`/piev ledger status`、`/piev-evolve …`、`/piev-report`） |

排队的消息可以编辑、删除、调整顺序。每条回复的代码块悬停有复制按钮；固定头上可以把选中的对话导出成 Markdown 或长图。

### 权限

设置 › 访问限制：读写范围、命令审批（每次问 / 自动 / 关）、网站黑白名单、桌面操控白名单（默认关）。有一层任何设置都放不开的硬拒绝（`rm -rf /`、格式化、`sudo bash -c` 套娃这类）。

### 面板

- **文件**：项目树，双击打开编辑器；二进制只显示信息，用系统默认程序打开。
- **改动**：IDE 页签 = 真 `git status` / `git diff`；AI 任务页签 = 这个任务改了什么的快照。
- **浏览器**：真网页（原生 WebView），可缩放 40–150%，快捷项可编辑；agent 可以在你授权的站点上操作。
- **预览**：PDF（内置阅读器）、图片、Office 文件卡片。
- **终端**：项目根目录下的 shell，可铺满。
- **ComfyUI**：设置里填 ComfyUI 地址后，聊天里能直接出图。
- **能力 / 演进收件箱 / 观察记录 / Agent 树**：PiEv 给自己装了什么、提了什么改进、看到了什么、谁在干活。

### 风格

设置 › 风格，或右下角快速设置：164 套，按家族（扁平 / 描边 / 质感 / 立体 / 发光 / 柔影 / 玻璃 / 像素）排列，搜索可用中文；透明风格有透明度滑条，0 = 完全透明、100 = 不透明；深浅外观各自记忆。

### 演进

设置 › 演进：三档（关 / 每次确认 / 自动）。PiEv 只改自己的产物层（扩展、skills、面板），不改主程序；主程序的缺陷与能力缺口走「报告问题」（`/piev-report`）投到本仓库的 Issues。

### 数据在哪

| 什么 | 在哪 |
|---|---|
| 设置、任务、台账 | `%APPDATA%\com.piev.desktop\`（macOS `~/Library/Application Support/com.piev.desktop/`，Linux `~/.local/share/com.piev.desktop/`） |
| 模型 key | 系统钥匙串（Windows 凭据管理器 / macOS Keychain / Linux Secret Service） |
| Pi 自己的配置 | `~/.pi/agent/` |
| 导出 | 应用数据目录下 `exports/` |

## Demo

<p align="center">
  <img src="https://raw.githubusercontent.com/lannerk/piev-releases/main/assets/demo-styles.png" alt="设置 › 风格：164 套" width="760">
</p>

一个典型回合：

```
你：  把 README 里的错别字改掉，顺便跑一下测试
PiEv： [read README.md] → [edit README.md ×3] → 要运行 `npm test`，允许？  [允许一次] [本会话允许] [拒绝]
你：  （agent 跑测试时直接打字）测试别跑 e2e 那组        ← Enter = 插话，在下一个安全边界生效
PiEv： 改为 `npm test -- --ignore e2e` … 3 处错别字已改，单元测试 42/42 通过。
```

## 更新

- **设置 › 更新 › 主程序**：显示「当前版本 · 发布日期」与「最新版本 · 发布日期」，一键「下载并安装」——先验签名再安装，Windows 装完自动重启。
- 启动时会在后台查一次（可在设置里关），有新版只在通知区提示一条。
- 更新只认本仓库的 `latest.json` 和编进程序里的公钥，不接受别的地址；签名不过就不装，旧版原地不动。
- Pi 核心的升级是另一个按钮（设置 › 更新 › 核心升级），升级前会先跑兼容测试，不过就不切换。

## 校验下载

每个 Release 带 `SHA256SUMS.txt`，每个安装包带 `.sig`（[minisign](https://jedisct1.github.io/minisign/) 格式，Tauri 签名）。公钥在 [`keys/piev.pub`](keys/piev.pub)：

```powershell
Get-FileHash .\PiEv_0.1.0_x64-setup.exe          # 对照 SHA256SUMS.txt
minisign -Vm .\PiEv_0.1.0_x64-setup.exe -x .\PiEv_0.1.0_x64-setup.exe.sig -p .\keys\piev.pub
```

## 版本与发布日期

- 第一个对外版本是 **0.1.0**，之后每版只加末位，正式版才是 1.0.0。
- 每个版本都有发布日期，关于页和 `latest.json` 的 `pub_date` 都能看到。
- 已发布的版本**不覆盖、不删除**；有问题就发下一版。变更写在各版本的 Release 说明里。

## 反馈

- bug、建议：开 [Issue](https://github.com/lannerk/piev-releases/issues)，附版本（关于页）和复现步骤；**别贴 key、项目内容或含本机路径的截图**。应用内「报告问题」会自动脱敏后投到这里。
- 安全问题请不要开公开 Issue，发到仓库 About 里留的邮箱。

## 许可

PiEv 按 [EULA](EULA.md) 分发，可免费下载使用，不包含源码授权。Pi 本身是其作者的开源项目，许可见 Pi 仓库。
