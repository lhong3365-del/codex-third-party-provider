<div align="center">

# Codex 第三方中转站接入指南

**国内开发者接入 OpenAI Codex 的完整配置教程：选择中转站 → 配置 config.toml → 设置 API Key → 验证运行**

[![Stars](https://img.shields.io/github/stars/lhong3365-del/codex-third-party-provider?style=flat-square&color=yellow)](https://github.com/lhong3365-del/codex-third-party-provider/stargazers)
[![Forks](https://img.shields.io/github/forks/lhong3365-del/codex-third-party-provider?style=flat-square&color=blue)](https://github.com/lhong3365-del/codex-third-party-provider/network)
[![License](https://img.shields.io/github/license/lhong3365-del/codex-third-party-provider?style=flat-square&color=purple)](./LICENSE)

[English](./README.en.md) | **简体中文**

</div>

---

## 📖 这是什么

这是一份**Codex 第三方中转站接入教程**，帮助国内开发者绕过网络限制、低成本使用 OpenAI Codex。

## 📖 核心问题

| 问题 | 官方方案 | 本教程方案 |
|------|---------|-----------|
| 网络限制 | 需要魔法上网 | 无需魔法 |
| 价格 | 官方订阅价格 | 中转站价格更低 |
| 配置难度 | 全英文文档 | 中文详细教程 |

## 🚀 快速开始

### 第一步：选择中转站

选择一个支持 Codex 的第三方中转站。

> ⚠️ **风险提示**：中转站存在跑路、断供、调价风险，**充值前务必小额测试**。

### 第二步：配置 config.toml

Codex 配置文件位于 `~/.codex/config.toml`（Windows 在 `C:\Users\你的用户名\.codex\config.toml`）。

**创建配置目录和文件：**

```powershell
# Windows PowerShell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.codex"
New-Item -ItemType File -Force -Path "$env:USERPROFILE\.codex\config.toml"
```

**写入配置（参考 [config-examples/config.toml](./config-examples/config.toml)）：**

```toml
# ============================================
# Codex CLI 配置文件
# 文件路径: ~/.codex/config.toml
# ============================================

# ---- 顶层配置：默认使用哪个模型和供应商 ----
model_provider = "ojbk"                  # 必须和下面 [model_providers.ojbk] 的 ojbk 一致
model = "gpt-5-codex"                      # 中转站支持的模型名
model_reasoning_effort = "medium"           # 推理强度: low / medium / high
network_access = "enabled"                  # 允许 codex 访问网络
disable_response_storage = true             # ⭐ 关键：禁用 OpenAI 端会话存储

# ---- 第三方供应商定义 ----
[model_providers.ojbk]
name = "GeekNow"
base_url = "https://api.ojbk.top/v1"    # ⭐ 中转站给的 API 地址
env_key = "GEEKNOW_API_KEY"                 # ⭐ 环境变量的名字，不是 Key 本身
wire_api = "responses"                      # responses 或 chat，看中转站支持哪个

# ---- 可选：Profile 多模型配置 ----
[profiles.text]
model = "gpt-5-codex"                      # 文本模型
model_provider = "ojbk"
model_reasoning_effort = "medium"

[profiles.image]
model = "gpt-image-2"                      # 图像模型
model_provider = "ojbk"
model_reasoning_effort = "minimal"
```

### 第三步：设置 API Key 环境变量

**Windows（PowerShell）：**

```powershell
# 把 sk-xxxxx 换成你的真实 Key
[Environment]::SetEnvironmentVariable("GEEKNOW_API_KEY", "sk-xxxxx", [EnvironmentVariableTarget]::User)

# 验证（必须开新窗口才能读到）
$env:GEEKNOW_API_KEY
```

**macOS / Linux：**

```bash
echo 'export GEEKNOW_API_KEY="sk-xxxxx"' >> ~/.bashrc
source ~/.bashrc
```

### 第四步：启动验证

```bash
# 关闭当前终端，重新开一个新窗口
codex

# 或者用某个 profile
codex --profile text
```

进入交互界面后，输入一句简单的 `Hello`，如果模型有回应就成功了。

## 📋 配置字段说明

### 顶层字段

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `model` | string | `gpt-5-codex` | 默认使用的模型名 |
| `model_provider` | string | `openai` | 供应商名，对应 `[model_providers.xxx]` 的 xxx |
| `model_reasoning_effort` | string | `medium` | 推理强度，可选 `low` / `medium` / `high` / `xhigh` |
| `network_access` | string | `disabled` | `enabled` 时允许 Codex 访问网络 |
| `disable_response_storage` | bool | `false` | 第三方中转**强烈建议设为 `true`** |

### `[model_providers.xxx]` 字段

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `name` | string | 否 | 显示名称 |
| `base_url` | string | **是** | API 端点地址，末尾通常带 `/v1` |
| `env_key` | string | 是 | 环境变量名 |
| `wire_api` | string | 是 | 协议：`responses`（新）或 `chat`（旧） |

## ⚠️ 常见报错

| 报错 | 原因 | 解决 |
|------|------|------|
| `404 Not Found` | `wire_api` 协议不对或 `base_url` 错误 | 切换 `responses`/`chat`，检查 `/v1` 后缀 |
| `401 Unauthorized` | 环境变量没生效 | 关掉终端开新窗口，`echo $GEEKNOW_API_KEY` 验证 |
| `TOML parse error` | 配置文件语法错误 | 检查引号、等号、括号是否完整 |

## ❓ FAQ

<details>
<summary><b>Q：中转站会跑路吗？</b></summary>

任何第三方服务都有风险。建议先小额测试，确认稳定后再增加充值金额。
</details>

<details>
<summary><b>Q：可以用多个中转站吗？</b></summary>

可以。在 config.toml 里定义多个 `[model_providers.xxx]`，然后用 `[profiles.xxx]` 切换。
</details>

<details>
<summary><b>Q：为什么要有 `disable_response_storage = true`？</b></summary>

OpenAI 的 Responses API 默认会在服务端保存对话历史。第三方中转可能不支持这个特性，开启会导致请求失败。
</details>

## 🤝 贡献

欢迎补充新的中转站配置示例！提交 PR 或提 Issue。

## 📄 License

[MIT License](./LICENSE) © 2026 lhong3365-del

---

<div align="center">

**如果这份指南帮到了你，请点一个 ⭐ Star**

[⬆ 回到顶部](#codex-第三方中转站接入指南)

</div>
