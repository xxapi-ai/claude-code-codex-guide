# Claude 桌面版接入第三方 API：Claude Desktop 配置 xxapi

Claude 桌面版（Claude Desktop）可以通过应用内置的第三方推理设置接入 xxapi（[https://xxapi.ai](https://xxapi.ai)）：选 **Gateway**，Gateway base URL 填 `https://xxapi.ai`（末尾不加 `/v1`），Gateway API key 填 Claude Code 分组的 API 密钥（API Key），模型列表里填模型广场中的 Claude 模型 ID。用的是官方下载的原版应用，不需要改程序文件。

适用于 Windows 和 macOS。桌面应用有自己的配置入口，Claude Code 终端的 `settings.json` 不会替它配置；Linux 请先用 [Claude Code](02-claude-code.md)。

## 1. 准备模型与密钥

打开 [模型广场](https://xxapi.ai/pricing)，复制一个 Claude 模型的完整 ID，再到 [API 密钥](https://xxapi.ai/keys) 创建能访问它的密钥（Claude Code 分组）。

## 2. 下载并安装 Claude Desktop

进入 Claude 官方下载页 [https://claude.com/download](https://claude.com/download)，选择 Windows 或 macOS 版本。Windows 用官方的 `.msix` 安装包；macOS 打开 `.dmg`，把 Claude 拖进“应用程序”。

## 3. 打开第三方推理设置

先停留在登录页面。macOS 用屏幕顶部菜单；Windows 点登录窗口左上角的应用菜单 `☰`。

1. 依次选择 **Help → Troubleshooting → Enable Developer Mode**，应用重启后会多出 Developer 菜单。
2. 打开 **Developer → Configure Third-Party Inference**，看到 Connection 设置页面。

## 4. 填入 xxapi 地址和密钥

在 Connection 中选择 **Gateway**：

| 界面字段 | 填写内容 |
| --- | --- |
| Inference provider | `Gateway` |
| Gateway base URL | `https://xxapi.ai` |
| Credential kind | `Static API key` |
| Gateway API key | 你自己的 xxapi API 密钥 |
| Gateway auth scheme | `x-api-key` |

未提到的字段保持默认。旧版本的字段位置可能不同，也可能没有独立的 Credential kind 下拉框。

以前配过其他服务的，先用配置窗口的 Export 把旧配置导出到自己电脑（文件可能含密钥，不要外传）。窗口是只读状态，说明设备有管理员下发的配置，需要管理员调整。

## 5. 填写要使用的模型

在配置窗口找到 **Models / Model list**（旧版本可能在 **Identity & models**），把第 1 步复制的完整模型 ID 加进去并放在第一项作为默认模型。填的是接口使用的 ID，不是自己起的显示名称。上下文扩展、1M 等选项先保持默认。

窗口提供 JSON 编辑入口时，模型列表对应 `inferenceModels`：

```json
{
  "inferenceModels": [
    { "name": "替换为模型广场中的Claude模型ID" }
  ]
}
```

## 6. 保存并重启

点 **Apply Changes**，再点 **Save & Restart**（旧版本可能是 **Apply locally**）。重启后如果让你选择运行方式，选刚保存的第三方配置。有 **Test connection** 的可以先测一下，出错要看具体内容。

## 7. 发一条消息，再核对记录

进入 Chat，选中刚配置的模型，新建会话，发送：

```text
请只回复“连接成功”，先不要读取或修改文件。
```

收到回复后，到 xxapi [使用日志](https://xxapi.ai/usage-logs/common) 核对请求时间和模型。以后切换服务商，也要完全退出再重开应用。

## 常见问题

**找不到 Developer 菜单**：先完成 Help → Troubleshooting → Enable Developer Mode 并等应用重启。仍没有就更新官方应用。

**Gateway was unreachable、401 或测试失败**：检查地址是根域 `https://xxapi.ai`、密钥正确、auth scheme 选 `x-api-key`；模型不存在时核对 Model list。

**Claude Code 已配好，桌面版仍要求登录**：桌面版读自己的第三方推理设置，在第 3 步的窗口确认已保存，完全退出再重开。

**Cowork 和远程功能**：Cowork 对系统和虚拟化有额外要求，远程、云端或官方账号专属功能有独立条件，不会因为设置了 API 密钥就自动可用。先跑通基本对话。

完整图文教程：[https://docs.xxapi.ai/claude-desktop](https://docs.xxapi.ai/claude-desktop)

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
