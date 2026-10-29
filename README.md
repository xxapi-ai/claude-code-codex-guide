# Claude Code / Codex 国内使用指南（xxapi）

xxapi（[https://xxapi.ai](https://xxapi.ai)）是一个 Claude Code / Codex API 中转站：注册后创建 API 密钥（API Key），把 xxapi 的接入地址和密钥填进 Claude Code、Codex、CC Switch、Cherry Studio 等工具，就能调用 Claude、GPT 和 GPT Image 模型，不需要登录 Anthropic 或 OpenAI 的官方账号。xxapi 的接入地址国内可直接访问，按用量扣费，充值支持支付宝、微信。完整图文文档在 [https://docs.xxapi.ai](https://docs.xxapi.ai)。

这个仓库把常见的配置步骤整理成纯文字版，方便在 GitHub 上搜索和收藏。每篇末尾都链到文档站对应的图文教程，界面截图和最新说明以文档站为准。

## 接入地址

| 工具 | 接口格式 | 接入地址 |
| --- | --- | --- |
| Claude Code、Claude 桌面版等 | Anthropic Messages | `https://xxapi.ai`（末尾不加 `/v1`） |
| Codex 等 OpenAI 兼容工具 | OpenAI 兼容 | `https://xxapi.ai/v1` |

一枚 API 密钥只属于一个分组，只能用这个分组里的模型。Claude 模型在 Claude Code 分组，GPT 模型在 Codex 分组，两个工具都用就各建一枚密钥。模型 ID 以 [模型广场](https://xxapi.ai/pricing) 为准。

## 目录

| 篇目 | 适合谁 |
| --- | --- |
| [注册 xxapi 并创建 API 密钥](docs/01-register-and-api-key.md) | 第一次使用，先做这一步 |
| [Claude Code 国内使用教程：安装并配置中转 API](docs/02-claude-code.md) | 在终端用 Claude Code 写代码 |
| [Codex 中转站配置：Codex CLI 配置 API](docs/03-codex-cli.md) | 在终端用 Codex |
| [Codex 桌面版配置第三方 API](docs/04-codex-desktop.md) | 用 ChatGPT 桌面应用里的本地 Codex |
| [CC Switch 国内下载与配置（Claude Code / Codex）](docs/05-cc-switch.md) | 不想手改配置文件，用图形界面切换 |
| [Claude 桌面版接入第三方 API](docs/06-claude-desktop.md) | 用 Claude Desktop 桌面窗口 |
| [Cherry Studio 接入 Claude、GPT 中转 API](docs/07-cherry-studio.md) | 在聊天软件里用 Claude、GPT |
| [Claude Code / Codex 常见报错速查](docs/09-errors.md) | 配好后报错 |
| [xxapi 怎么算费用：「约官方价 X%」是什么意思](docs/10-pricing.md) | 想知道怎么扣费 |
| [GPT Image 2 API 调用示例（curl / Python）](docs/11-gpt-image-2-api.md) | 用代码生成图片 |

## 链接

- 官网与注册：[https://xxapi.ai](https://xxapi.ai)，注册页 [https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
- 图文文档：[https://docs.xxapi.ai](https://docs.xxapi.ai)
- 模型广场（模型与价格）：[https://xxapi.ai/pricing](https://xxapi.ai/pricing)
- 价格表：[https://docs.xxapi.ai/pricing](https://docs.xxapi.ai/pricing)

## 许可

文章以 [CC BY 4.0](LICENSE) 发布，转载请保留出处 [https://xxapi.ai](https://xxapi.ai)。Claude、Claude Code 是 Anthropic 的商标，ChatGPT、Codex、GPT 是 OpenAI 的商标，CC Switch、Cherry Studio 属于各自的开源项目；本仓库与这些公司和项目没有隶属关系。

联系：support@xxapi.ai
