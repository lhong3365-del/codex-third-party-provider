# 常见问题 FAQ

## 配置相关

<details>
<summary><b>Q：Codex 和 ChatGPT 桌面版有什么区别？</b></summary>

ChatGPT 桌面版是聊天产品，需要你复制粘贴代码。Codex CLI 是 Agent 产品，能直接读写你电脑上的文件、运行命令。
</details>

<details>
<summary><b>Q：用第三方中转会被 OpenAI 封号吗？</b></summary>

第三方中转用的是中转站自己的官方账号池，封号风险在中转站那边，不影响你。但你的对话内容会经过中转站服务器，敏感数据慎用。
</details>

<details>
<summary><b>Q：`disable_response_storage = true` 是什么意思？为什么要开？</b></summary>

OpenAI 的 Responses API 默认会在服务端保存对话历史。如果你用第三方中转，中转站可能没启用这个特性，开启会导致请求失败。设为 `true` 让 Codex 客户端自己管理历史。
</details>

<details>
<summary><b>Q：能不能同时配置多个中转站，按需切换？</b></summary>

能。在 config.toml 里定义多个 `[model_providers.xxx]`，然后用 `[profiles.xxx]` 切换不同供应商。
</details>

---

## 使用相关

<details>
<summary><b>Q：Windows 上必须用 WSL 吗？</b></summary>

不必须，但推荐。原生 Windows 部分功能（沙箱、文件权限、shell 集成）有限制。
</details>

<details>
<summary><b>Q：能用本地模型吗（Ollama / vLLM）？</b></summary>

可以。把 `base_url` 指向 `http://localhost:11434/v1`，`env_key` 随便填一个不存在的，`requires_openai_auth = false`。
</details>

<details>
<summary><b>Q：reasoning_effort 调高了模型变慢，怎么办？</b></summary>

`high` 会让模型多想几轮，速度慢但效果好。日常用 `medium`，复杂任务用 `high`，简单查询用 `low`。
</details>

<details>
<summary><b>Q：模型回复经常被截断怎么办？</b></summary>

设置 `model_context_window` 为模型支持的最大值，并设置 `model_auto_compact_token_limit` 让 Codex 自动压缩历史。
</details>

---

## 中转站相关

<details>
<summary><b>Q：中转站会跑路吗？</b></summary>

任何第三方服务都有风险。建议先小额测试，确认稳定后再增加充值金额。
</details>

<details>
<summary><b>Q：哪个中转站最稳定？</b></summary>

没有绝对答案。稳定性会随时间变化。建议多注册几个，做备用。
</details>

<details>
<summary><b>Q：可以自己搭建中转吗？</b></summary>

可以。如果你有海外服务器，可以用开源项目如 `adryfish/recodex` 自建。
</details>
