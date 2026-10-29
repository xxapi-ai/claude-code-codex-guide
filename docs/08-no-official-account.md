# Claude / ChatGPT 官方账号注册不了、被停用？用 API 不需要官方账号

如果你卡在 Claude 或 ChatGPT 官方账号的注册、付款或停用上，另一种用法是走 API：在 xxapi（[https://xxapi.ai](https://xxapi.ai)）注册账号并创建 API 密钥（API Key），把地址和密钥填进 Claude Code、Codex 等工具，工具就按 API 方式调用模型，不需要登录 Anthropic 或 OpenAI 的官方账号。xxapi 充值支持支付宝、微信，按用量扣费。

下面分开说清两件事：官方账号为什么会遇到限制，API 方式在机制上有什么不同。

## 1. 官方账号为什么会遇到限制

官方账号受官方的地区和付款条件约束，这些条件写在官方公开的政策里：

- Anthropic 的 [Supported Regions Policy](https://www.anthropic.com/supported-countries) 写明，Claude.ai、Claude Code、API 等产品只在列出的国家和地区提供，未列出的地区都不支持。
- OpenAI 的 API 也有 [支持的国家和地区列表](https://developers.openai.com/api/docs/supported-countries)。
- 订阅和 API 充值通常需要官方接受的付款方式，例如官方支持地区发行的银行卡。

不满足这些条件时，常见的情况是注册不了、付款失败，或者账号被官方限制、停用。具体以官方的政策和通知为准，本文不提供、也不建议任何绕开官方检测的方法。

## 2. API 方式有什么不同

Claude Code、Codex 这类工具本来就支持“自定义地址 + 密钥”的接入方式，官方文档里叫网关（Gateway）或自定义服务商：

| | 官方账号登录 | 通过 xxapi 的 API 方式 |
| --- | --- | --- |
| 登录什么 | Anthropic / OpenAI 官方账号 | 不登录官方账号，工具里填 xxapi 的地址和 API 密钥 |
| 怎么付钱 | 官方订阅或官方 API 充值 | 在 xxapi 钱包充值，支付宝、微信、Stripe |
| 怎么计费 | 按官方套餐或官方 API 价 | 按用量从 xxapi 余额扣，价格见 [模型广场](https://xxapi.ai/pricing) |
| 工具里怎么配 | 工具自带的官方登录 | Claude Code 用 `ANTHROPIC_BASE_URL` 和 `ANTHROPIC_AUTH_TOKEN`；Codex 用 `config.toml` 的自定义服务商 |

接入地址：

```text
Claude Code 等 Anthropic 接口：https://xxapi.ai
Codex 等 OpenAI 兼容接口：  https://xxapi.ai/v1
```

具体怎么填，见 [Claude Code 教程](02-claude-code.md) 和 [Codex CLI 教程](03-codex-cli.md)。Claude Code 里配置好之后，旧的官方登录记录可以保留，当前填的网关凭据会优先使用。

## 3. 边界：哪些事 API 方式做不到

- **官方账号专属功能不会因为填了 API 密钥就能用**，例如 Claude 桌面版的远程、云端功能，ChatGPT 网页版、手机端和云端任务。API 方式只影响你在本机工具里发出的模型请求。
- **xxapi 不是 Anthropic 或 OpenAI 官方**，也不代表官方的服务承诺。使用 xxapi 需要遵守 [xxapi 用户协议](https://xxapi.ai/user-agreement)。
- **API 密钥就是付款凭证**：谁拿到密钥，谁就能用你的余额。不要把密钥发进群聊或提交到代码仓库，截图要遮住。

## 4. 开始使用

1. 在 [https://xxapi.ai/sign-up](https://xxapi.ai/sign-up) 注册。
2. 按 [注册与创建密钥](01-register-and-api-key.md) 创建密钥并充值。
3. 按你用的工具选一篇教程配置。

完整图文教程：[https://docs.xxapi.ai/getting-started](https://docs.xxapi.ai/getting-started)

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
