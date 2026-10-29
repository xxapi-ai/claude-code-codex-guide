# 注册 xxapi 并创建 API 密钥（新手第一步）

先在 xxapi（[https://xxapi.ai](https://xxapi.ai)）注册登录，到 [API 密钥页面](https://xxapi.ai/keys) 点「创建 API 密钥」，选好你用的工具和分组后创建并复制密钥，再到 [钱包](https://xxapi.ai/wallet) 充值，就可以去工具里填地址、密钥和模型 ID 了。接入地址：Claude Code 填 `https://xxapi.ai`，Codex 和其他 OpenAI 兼容工具填 `https://xxapi.ai/v1`。

API 密钥（API Key）是一串连接凭证，后面把它粘贴到工具的密钥输入框里即可，它不是账号密码。

## 1. 注册并登录

打开 [xxapi 注册页](https://xxapi.ai/sign-up)，选择页面提供的注册方式，按提示完成注册，再登录。

**完成标志**：能进入 xxapi 控制台，并打开 [API 密钥页面](https://xxapi.ai/keys)。

第一次登录、还没有密钥时，控制台会自动打开 **新手向导**，按“选分组、创建密钥、接入工具、充值”四步带你做完；关掉后，点顶栏的 **新手** 或 API 密钥页右上角的 **新手向导** 可以重新打开。

## 2. 找到你需要的模型

打开 [模型广场](https://xxapi.ai/pricing)，在分组卡片上点「详情」，看你想用的模型在哪些分组。

分组决定这枚密钥能用哪些模型、按什么价格扣费。创建密钥时选包含目标模型的分组即可，不需要把分组名称当成模型 ID 填进工具。

## 3. 创建 API 密钥

打开 [API 密钥页面](https://xxapi.ai/keys)，点右上角 **创建 API 密钥**。

1. 在 **你用什么工具？** 里选你要接的工具，例如 Claude Code、Codex 或生图。
2. 在下面的分组卡片里选一个。每张卡片写着分组名称、约官方价多少（生图分组写每张多少钱）和一句说明，带 **推荐** 角标的分组会默认选中。个别分组选中后要先勾选确认说明，才能创建。
3. **名称** 会自动填成分组名，可以改成容易认出的名字，例如 `我的 Claude Code`。
4. **高级设置** 里的额度、过期时间、模型限制和 IP 白名单，第一次保持默认，不设置就不限制。
5. 点底部的 **创建 API 密钥**。

创建后会弹出 **密钥已创建**，可以直接复制密钥，也可以点 **导入 CC Switch** 一键导入。关掉后，在密钥列表里点这一行最右边的 **⋯**，同样能 **复制密钥**、**复制连接信息** 或 **导入 CC Switch**。

**完成标志**：列表里有这枚密钥，并且已经复制到剪贴板。

> 向别人求助或截图时，用 `sk-你的密钥` 代替真实内容，截图也要遮住密钥。

## 4. 为什么 Claude Code 和 Codex 要两枚密钥

一枚密钥只属于一个分组，只能调用这个分组里的模型、按这个分组的价格扣费。Claude 模型在 Claude Code 分组，GPT 模型在 Codex 分组，所以两个工具都要用，就各建一枚。

| 工具 | API 地址 | 密钥 | 模型 |
| --- | --- | --- | --- |
| Claude Code | `https://xxapi.ai` | Claude Code 分组的密钥 | Claude 模型 |
| Codex | `https://xxapi.ai/v1` | Codex 分组的密钥 | GPT 模型 |

两枚密钥都从同一个账号余额里扣费，不用分别充值。用错了会看到“当前分组 … 暂不支持模型 …”，换用对应分组的密钥即可。

## 5. 充值

新账号的余额是 0。不充值的话，工具发出第一条消息就会收到“余额不足，请先充值。”。打开 [钱包](https://xxapi.ai/wallet) 充值，到账后就能用：

- 付 ¥1，到账 $1。
- 余额不过期，不按月清零。
- 支付宝、微信都能付，也支持 Stripe。
- 按用量扣费，没有月费。

最低充值金额和实际支付金额以钱包页为准。

## 下一步

- 终端写代码：[Claude Code](02-claude-code.md) 或 [Codex CLI](03-codex-cli.md)
- 图形界面切换：[CC Switch](05-cc-switch.md)
- 聊天软件：[Cherry Studio](07-cherry-studio.md)

完整图文教程：[https://docs.xxapi.ai/getting-started](https://docs.xxapi.ai/getting-started)

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
