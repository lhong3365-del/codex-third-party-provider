<div align="center">

# Codex Third-Party Provider Guide

**Complete guide for connecting OpenAI Codex to third-party relay APIs in China**

[![Stars](https://img.shields.io/github/stars/lhong3365-del/codex-third-party-provider?style=flat-square&color=yellow)](https://github.com/lhong3365-del/codex-third-party-provider/stargazers)
[![Forks](https://img.shields.io/github/forks/lhong3365-del/codex-third-party-provider?style=flat-square&color=blue)](https://github.com/lhong3365-del/codex-third-party-provider/network)
[![License](https://img.shields.io/github/license/lhong3365-del/codex-third-party-provider?style=flat-square&color=purple)](./LICENSE)

[English](./README.en.md) | **简体中文**

</div>

---

## What is this?

A guide for developers in China to use OpenAI Codex via third-party relay APIs, avoiding network restrictions and high costs.

## Quick Start

### 1. Choose a relay provider

Select a relay that supports Codex. Common options:

- **OJBK** - Stable and reliable
- **PackyAPI** - Well-documented
- **Shenma API** - Established provider

### 2. Configure config.toml

Codex config file: `~/.codex/config.toml` (Windows: `C:\Users\YourName\.codex\config.toml`)

```toml
model_provider = "ojbk"
model = "gpt-5-codex"
model_reasoning_effort = "medium"
network_access = "enabled"
disable_response_storage = true

[model_providers.ojbk]
name = "ojbk"
base_url = "https://api.ojbk.top/v1"
env_key = "OJBK_API_KEY"
wire_api = "responses"
```

### 3. Set API Key environment variable

**Windows (PowerShell):**
```powershell
[Environment]::SetEnvironmentVariable("OJBK_API_KEY", "sk-xxxxx", [EnvironmentVariableTarget]::User)
```

**macOS / Linux:**
```bash
echo 'export OJBK_API_KEY="sk-xxxxx"' >> ~/.bashrc
source ~/.bashrc
```

### 4. Test

```bash
codex
```

Type `Hello` to test if it works.

## Supported Providers

| Provider | wire_api | Notes |
|----------|----------|-------|
| OJBK | responses | Stable |
| PackyAPI | responses | Well-documented |
| Shenma API | responses / chat | Established |

## Troubleshooting

| Error | Cause | Solution |
|-------|-------|----------|
| `404 Not Found` | Wrong wire_api or base_url | Try `responses` or `chat`, check `/v1` suffix |
| `401 Unauthorized` | Env variable not loaded | Open new terminal, run `echo $VAR` |
| `TOML parse error` | Syntax error in config | Check quotes, equals, brackets |

## License

MIT License © 2026 lhong3365-del
