# 快速开始

## 环境要求

| 项目 | 最低要求 | 推荐 |
|------|---------|------|
| Node.js | 22.0 | 22 LTS 或更新 |
| 操作系统 | Win 10 / macOS 11 / Ubuntu 20.04 | Win 11 / macOS 14 / Ubuntu 22.04 |
| 内存 | 4 GB | 8 GB+ |

## 安装 Codex CLI

### Windows

```powershell
# 1. 检查 Node 版本（必须 ≥ 22）
node --version

# 如果版本太低，去 https://nodejs.org/zh-cn 下载安装

# 2. 全局安装 Codex
npm install -g @openai/codex

# 3. 验证安装
codex --version
```

### macOS

```bash
# 推荐用 Homebrew
brew install node@22
npm install -g @openai/codex
```

### Linux

```bash
# Ubuntu / Debian
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt install -y nodejs
npm install -g @openai/codex
```

## 配置流程

### 1. 创建配置文件

```powershell
# Windows PowerShell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.codex"
New-Item -ItemType File -Force -Path "$env:USERPROFILE\.codex\config.toml"
```

### 2. 写入配置

参考 [config-examples/config.toml](../config-examples/config.toml) 编写配置。

### 3. 设置 API Key

```powershell
# Windows
[Environment]::SetEnvironmentVariable("你的变量名", "sk-你的真实Key", [EnvironmentVariableTarget]::User)
```

### 4. 启动验证

```bash
# 必须开新终端窗口
codex
```

输入 `Hello` 测试，如果模型回复就成功了。

## 常见安装问题

**Q：`npm install -g` 报权限错误？**

```bash
# Linux/Mac 不要用 sudo，改用：
mkdir -p ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
npm install -g @openai/codex
```

**Q：Windows 提示 "无法加载文件 codex.ps1"？**

```powershell
# 管理员身份运行 PowerShell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```
