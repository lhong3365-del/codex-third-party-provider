# 其他中转站配置示例

> ⚠️ **风险提示**：以下中转站信息来自社区收集，充值前请自行验证。

---

## PackyAPI

```toml
[model_providers.packyapi]
name = "PackyAPI"
base_url = "https://api.packyapi.com/v1"
env_key = "PACKYAPI_API_KEY"
wire_api = "responses"
```

**环境变量设置：**
```powershell
[Environment]::SetEnvironmentVariable("PACKYAPI_API_KEY", "sk-你的Key", [EnvironmentVariableTarget]::User)
```

---

## 神马 API

```toml
[model_providers.shenma]
name = "神马API"
base_url = "https://api.shenma.com/v1"
env_key = "SHENMA_API_KEY"
wire_api = "responses"
```

**环境变量设置：**
```powershell
[Environment]::SetEnvironmentVariable("SHENMA_API_KEY", "sk-你的Key", [EnvironmentVariableTarget]::User)
```

---

## AICodeMirror

```toml
[model_providers.aicodemirror]
name = "AICodeMirror"
base_url = "https://api.aicodemirror.com/v1"
env_key = "AICODEMIRROR_API_KEY"
wire_api = "responses"
```

---

## 多中转站切换配置

如果你有多个中转站，可以通过 profiles 快速切换：

```toml
# 默认使用 OJBK
model_provider = "ojbk"
model = "gpt-5-codex"
model_reasoning_effort = "medium"
network_access = "enabled"
disable_response_storage = true

# OJBK 配置
[model_providers.ojbk]
name = "ojbk"
base_url = "https://api.ojbk.top/v1"
env_key = "OJBK_API_KEY"
wire_api = "responses"

# PackyAPI 配置
[model_providers.packyapi]
name = "PackyAPI"
base_url = "https://api.packyapi.com/v1"
env_key = "PACKYAPI_API_KEY"
wire_api = "responses"

# 神马 API 配置
[model_providers.shenma]
name = "神马API"
base_url = "https://api.shenma.com/v1"
env_key = "SHENMA_API_KEY"
wire_api = "responses"

# Profile 切换
[profiles.ojbk]
model_provider = "ojbk"
model = "gpt-5-codex"
model_reasoning_effort = "high"

[profiles.packy]
model_provider = "packyapi"
model = "gpt-5-codex"
model_reasoning_effort = "medium"

[profiles.shenma]
model_provider = "shenma"
model = "gpt-5-codex"
model_reasoning_effort = "medium"
```

**使用方式：**
```bash
# 使用 OJBK
codex --profile ojbk

# 切换到 PackyAPI
codex --profile packy

# 切换到神马
codex --profile shenma
```

---

## 自建中转方案

如果你有海外服务器，可以考虑自建：

| 项目 | 适用场景 | 链接 |
|------|---------|------|
| `adryfish/recodex` | Codex 单产品代理 | [GitHub](https://github.com/adryfish/recodex) |
| `Wei-Shaw/sub2api` | Claude / Codex / Gemini 一站式 | [GitHub](https://github.com/Wei-Shaw/sub2api) |

**自建配置示例：**
```toml
[model_providers.self]
name = "自建中转"
base_url = "https://你的域名.com/v1"
env_key = "SELF_API_KEY"
wire_api = "responses"
requires_openai_auth = false
```
