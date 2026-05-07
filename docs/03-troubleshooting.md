# 故障排查

## 错误速查表

| 报错 | 原因 | 解决 |
|------|------|------|
| `404 Not Found` 或 `Endpoint not found` | `wire_api` 协议不对 | 把 `responses` 改 `chat` 试试，或反之 |
| `404` 但模型名是对的 | `base_url` 末尾少了 `/v1` | 加上 `/v1` |
| `401 Unauthorized` | 环境变量没生效 | **关掉终端开新窗口**，再 `echo $变量名` 验证 |
| `401` 但 echo 有值 | `env_key` 名字写错 | 检查 config.toml 里 `env_key` 和实际环境变量名是否完全一致 |
| `429 Too Many Requests` | 超过中转站限速 | 等几秒重试，或去后台升级套餐 |
| `Connection refused` | base_url 不通 | 用 `curl -v <base_url>` 测试网络 |
| `TOML parse error at line X` | 配置文件语法错误 | 检查引号、等号、括号是否完整 |
| `Model 'xxx' not found` | 模型名不对 | 去中转站文档查准确的模型字符串 |
| `Failed to load auth.json` | auth.json 文件存在但内容错误 | 删掉 `~/.codex/auth.json` 重启 |
| Windows 下 `codex` 卡住不响应 | 终端不兼容 | 换 Windows Terminal 或 WSL |
| 中文乱码 | 终端编码 | Windows 执行 `chcp 65001` |

---

## 排查流程

```
报错出现
    │
    ├─→ 404 ──→ 检查 wire_api 是否正确
    │            检查 base_url 末尾 /v1
    │
    ├─→ 401 ──→ 新开终端 echo $变量名 验证环境变量
    │            检查 env_key 是否和 config.toml 一致
    │
    ├─→ 429 ──→ 等几秒重试
    │            去中转站后台查余额和限速
    │
    ├─→ Connection ──→ curl -v 测试 base_url
    │                 检查网络/DNS/防火墙
    │
    └─→ TOML error ──→ 检查配置文件语法
                      去掉多余空格/引号/括号
```

---

## 调试技巧

### 查看 Codex 实际发出的请求

```bash
# 开启详细日志
RUST_LOG=debug codex
```

### 用 curl 测试中转站

```bash
curl -X POST https://api.example.com/v1/chat/completions \
  -H "Authorization: Bearer $变量名" \
  -H "Content-Type: application/json" \
  -d '{"model":"gpt-5-codex","messages":[{"role":"user","content":"hi"}]}'
```

如果 curl 也失败，那就是中转站问题，不是 Codex 配置问题。

### TOML 语法校验

把配置文件内容粘贴到 https://www.toml-lint.com/ 校验语法。

---

## 环境变量不生效？

1. **Windows 必须开新终端窗口**才能读到新设置的环境变量
2. 验证方式：
   ```powershell
   # PowerShell
   $env:你的变量名
   ```
3. 如果还是不行，尝试直接设置用户变量：
   ```powershell
   [Environment]::SetEnvironmentVariable("变量名", "值", [EnvironmentVariableTarget]::User)
   ```
4. 确认 config.toml 里的 `env_key` 和环境变量名**完全一致**（区分大小写）
