# GeekNow 中转站配置教程

## 注册与获取 API Key

1. 访问 GeekNow 官网注册账号
2. 进入"API Keys"页面创建新 Key
3. 复制保存 Key（只显示一次）

## 配置文件示例

```toml
[model_providers.geeknow]
name = "GeekNow"
base_url = "https://api.geeknow.top/v1"
env_key = "GEEKNOW_API_KEY"
wire_api = "responses"
```

## 设置环境变量

**Windows（PowerShell）：**

```powershell
[Environment]::SetEnvironmentVariable("GEEKNOW_API_KEY", "sk-你的真实Key", [EnvironmentVariableTarget]::User)
```

**macOS / Linux：**

```bash
echo 'export GEEKNOW_API_KEY="sk-你的真实Key"' >> ~/.bashrc
source ~/.bashrc
```

## 验证配置

```bash
codex
```

输入 `Hello` 测试是否正常工作。
