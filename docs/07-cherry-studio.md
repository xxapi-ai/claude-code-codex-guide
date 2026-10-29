# Cherry Studio 接入 Claude、GPT 中转 API（xxapi）

在 Cherry Studio 里添加 xxapi（[https://xxapi.ai](https://xxapi.ai)）作为自定义提供商：用 Claude 时端点选 **Anthropic**、地址填 `https://xxapi.ai`（软件会自动补上 `/v1/messages`），密钥用 Claude Code 分组的 API 密钥（API Key），同步模型后就能在聊天窗口里用。用 GPT 时另加一个提供商，端点选 OpenAI，地址同样填根地址。

## 1. 安装软件，准备密钥

从 Cherry Studio 官网 [https://www.cherry-ai.com/](https://www.cherry-ai.com/) 下载安装包并打开。准备一枚 xxapi API 密钥，还没有的话先看 [注册与创建密钥](01-register-and-api-key.md)；模型 ID 在 [模型广场](https://xxapi.ai/pricing) 查。

## 2. 添加 xxapi

点 **设置 → 模型服务 → 添加服务商**，选自定义提供商：

| 填写项 | 填写内容 |
| --- | --- |
| 提供商名称 | `xxapi` |
| API 密钥 | 你创建的 xxapi API 密钥 |
| 端点或提供商类型 | `Anthropic` |
| Anthropic API 地址 | `https://xxapi.ai` |

填好后，地址下方的预览会显示 `/v1/messages`，完整请求路径由软件添加。保存后打开提供商右上角的开关。

旧版可能写“添加提供商”和“提供商类型”；新版会让你分别填写不同端点，用 Claude 时找到 Anthropic 那一栏填根地址即可。

## 3. 同步并选择模型

点 **同步模型**（旧版可能叫 **管理** 或 **获取模型列表**），找到你要用的模型，添加或启用。没有自动出现时，点添加模型，粘贴模型广场里的完整模型 ID。

回到首页新建对话，点顶部模型名称，选 **xxapi** 下面的模型。

## 4. 发第一条消息

```text
请用一句话介绍你可以帮我做什么。
```

收到正常回复就完成了。

## 想用 GPT 聊天

再添加一个提供商，名称用 `xxapi · GPT` 方便辨认，密钥用 Codex 分组的 API 密钥。地址都填根地址，让软件补全路径：

| 要用的模型 | 端点或提供商类型 | API 地址 | 下方请求预览应包含 |
| --- | --- | --- | --- |
| Claude | Anthropic | `https://xxapi.ai` | `/v1/messages` |
| GPT 等兼容聊天模型 | OpenAI | `https://xxapi.ai` | `/v1/chat/completions` |

如果模型详情要求 Responses 接口，就选 Responses 端点，并确认地址预览为 `https://xxapi.ai/v1/responses`。模型支持哪种接口，以 xxapi 当前的模型详情为准。

想在 Cherry Studio 里画图，见 [GPT Image 2 API 调用示例](11-gpt-image-2-api.md) 末尾的说明。

## 卡住时先看这里

- **401 或密钥错误**：重新从 [密钥页面](https://xxapi.ai/keys) 复制完整密钥，检查提供商是否已启用。
- **提示“当前分组 … 暂不支持模型 …”**：核对模型 ID 和这枚密钥的分组（Claude 用 Claude Code 分组，GPT 用 Codex 分组）。
- **404**：看地址下方的预览，地址框里不要重复填 `/v1/messages` 或 `/chat/completions`。
- **检测失败但没有详细原因**：确认检测时选的是聊天模型。图片模型应在绘画页面验证。

已经配置过其他平台的，保留原提供商，另外添加 xxapi，确认能用后再决定是否停用旧的。

完整图文教程：[https://docs.xxapi.ai/cherry](https://docs.xxapi.ai/cherry)

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
