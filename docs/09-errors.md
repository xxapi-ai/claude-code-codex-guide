# Claude Code / Codex 常见报错速查（xxapi）

在 Claude Code、Codex 里通过 xxapi（[https://xxapi.ai](https://xxapi.ai)）使用时，大多数报错都能从客户端这一侧查出原因：地址填错、密钥分组和模型对不上、余额或密钥额度用完、对话太长，或者 CC Switch 转换出错。按报错原文在下面找到对应一行，照“怎么办”做；解决不了，把报错末尾的请求 ID 发给 support@xxapi.ai。

## 速查表

| 报错原文（节选） | 最常见的原因 | 怎么办 |
| --- | --- | --- |
| 401、无效的密钥、未提供密钥 | 密钥没复制完整、有空格或占位文字，或者地址还指向别的平台 | 从 [API 密钥页面](https://xxapi.ai/keys) 重新复制完整密钥；确认地址是 xxapi |
| 该密钥已过期、该密钥状态不可用 | 这枚密钥过期或被禁用 | 在密钥列表里看状态，改好再试，或新建一枚 |
| 404，或返回一整页 HTML | 地址填错：多了或少了 `/v1`，或填成了注册页、控制台页面 | Claude Code 填 `https://xxapi.ai`，Codex 填 `https://xxapi.ai/v1` |
| 当前分组 … 暂不支持模型 … | 密钥的分组里没有这个模型，最常见是拿 Claude Code 分组的密钥调 GPT 模型（或反过来）；也可能是模型 ID 拼错 | 换用对应分组的密钥；模型 ID 从 [模型广场](https://xxapi.ai/pricing) 整段复制 |
| 该密钥无权访问模型 … | 这枚密钥设了模型限制 | 编辑密钥，在“分组与模型限制”里加上模型或清空限制 |
| 余额不足，请先充值。 | 账号余额不够，新账号余额是 0 | 到 [钱包](https://xxapi.ai/wallet) 充值后重发 |
| 该密钥额度已用完。 | 密钥自己设了额度上限，账号可能还有余额 | 编辑密钥，调高额度或打开“无限配额” |
| prompt is too long | 对话加附件超过了模型的上下文长度 | 输入 `/compact` 压缩，或新开对话；别把大文件整段贴进去 |
| Codex 提示“压缩已中断”，报 Model … is not available in group … | 对话中途换了模型，Codex 先用上一个模型压缩，而它不在你的分组里 | 新开对话，一开始就选分组里有的模型 |
| `input_schema does not support oneOf, allOf, or anyOf` | Codex 经 CC Switch 转换调用 Claude 模型，CC Switch 转换时的已知问题 | 用 Claude 模型就直接用 Claude Code；留在 Codex 就用 GPT 模型 |
| `"thinking.type.disabled" is not supported for this model` | 同上，Codex 经 CC Switch 调 Opus 5.5 时把思考设成了关闭 | 同上 |
| `CERTIFICATE_VERIFY_FAILED: certificate has expired` | 电脑日期不对，或代理、杀毒软件替换了证书，或地址填错 | 核对系统时间，暂时关掉代理或 HTTPS 扫描，再检查地址 |
| `Failed to fetch` | 浏览器类工具：网络或代理断开、地址不对，或请求超过 64 MB | 先在浏览器打开 `https://xxapi.ai`；带大图时缩小图片、少带几张 |
| 服务器繁忙，请稍后重试 | 偶尔出现多是临时问题；同一个长对话每条都报，多半是这个对话本身的问题 | 偶尔出现等半分钟再发；长对话每条都报就新开对话；一直出现把请求 ID 发给客服 |

## 几个容易混的地方

**Claude Code 和 Codex 的地址不一样。** Claude Code 用 Anthropic 格式，地址是根域 `https://xxapi.ai`；Codex 用 OpenAI 兼容格式，地址带 `/v1`。工具会自己在后面拼请求路径，不要把 `/v1/messages`、`/chat/completions` 再填一遍。

**一枚密钥只属于一个分组。** Claude 模型和 GPT 模型在不同分组，两个工具都用就各建一枚密钥。

**改了配置要重开。** Claude Code、Codex 和 CC Switch 切换后，正在运行的会话可能还在用旧连接。完全退出再打开，用 `/status` 看实际生效的地址和模型。

**换过密钥或分组的长对话。** 每条都报错、新开对话却正常时，直接新开对话继续。

## 找客服时带上这些

发邮件到 support@xxapi.ai，附上：工具名称和版本、电脑系统、卡住的步骤、完整报错、报错末尾 `(request id: …)` 里的请求 ID、出错时间、模型 ID。截图里遮住 API 密钥，保留地址和模型 ID。

## 每种报错的详细排查

- 常见问题总页：[https://docs.xxapi.ai/help](https://docs.xxapi.ai/help)
- prompt is too long：[https://docs.xxapi.ai/errors/prompt-too-long](https://docs.xxapi.ai/errors/prompt-too-long)
- Codex 换模型后压缩中断：[https://docs.xxapi.ai/errors/codex-compact-model-not-available](https://docs.xxapi.ai/errors/codex-compact-model-not-available)
- input_schema 不支持 anyOf：[https://docs.xxapi.ai/errors/input-schema-anyof](https://docs.xxapi.ai/errors/input-schema-anyof)
- thinking.type.disabled 400：[https://docs.xxapi.ai/errors/thinking-disabled-400](https://docs.xxapi.ai/errors/thinking-disabled-400)
- 证书过期报错：[https://docs.xxapi.ai/errors/certificate-expired](https://docs.xxapi.ai/errors/certificate-expired)
- Failed to fetch：[https://docs.xxapi.ai/errors/failed-to-fetch](https://docs.xxapi.ai/errors/failed-to-fetch)

完整图文教程：[https://docs.xxapi.ai/help](https://docs.xxapi.ai/help)

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
