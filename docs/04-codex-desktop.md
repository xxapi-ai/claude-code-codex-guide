# Codex 桌面版配置第三方 API：本地 Codex 接入 xxapi

Codex 桌面版和终端版读同一份 `config.toml`：`base_url` 填 xxapi 的 `https://xxapi.ai/v1`（`wire_api` 为 `"responses"`），`XXAPI_API_KEY` 填 Codex 分组的 API 密钥（API Key），模型 ID 从 [模型广场](https://xxapi.ai/pricing) 的 Codex 分组复制。桌面部分要多做的一步，是让从图标打开的应用也能读到这个密钥。

OpenAI 官方已把原 Codex app 入口合并到 ChatGPT 桌面应用，本篇配置的是其中的 **本地 Codex**。建议先按 [Codex CLI 配置](03-codex-cli.md) 在终端跑通，再做桌面版。

## 1. 安装官方桌面应用

打开 OpenAI 官方下载页 [https://chatgpt.com/download/](https://chatgpt.com/download/)，安装适合自己系统的 ChatGPT 桌面应用。macOS 安装包标注为 Apple Silicon，先在“关于本机”确认芯片类型。Linux 用户先用 Codex CLI。

## 2. 完全退出应用，再检查配置

在应用菜单选择 Quit / 退出（只关窗口它可能还在后台）。打开配置文件：

| 系统 | 配置文件 |
| --- | --- |
| Windows | `%USERPROFILE%\.codex\config.toml` |
| macOS | `~/.codex/config.toml` |

内容与终端版一致：

```toml
model = "替换为模型广场中的Codex模型ID"
model_provider = "xxapi"
web_search = "disabled"

[model_providers.xxapi]
name = "xxapi"
base_url = "https://xxapi.ai/v1"
wire_api = "responses"
env_key = "XXAPI_API_KEY"
```

已有配置时修改同名项，其他内容保留。桌面应用不会读取 WSL 里另一个 Linux 用户的 `.codex` 目录。

## 3. 让桌面应用读到密钥

终端里临时 `export` 或 `$env:` 设置的变量，通常不会传给从图标打开的应用。

**Windows**：开始菜单搜索“编辑账户的环境变量”，在上方 **用户变量** 区域点“新建”，变量名填 `XXAPI_API_KEY`，变量值填自己的 xxapi API 密钥。保存后注销并重新登录 Windows。

**macOS**：在终端执行（先把密钥填进去）：

```bash
export XXAPI_API_KEY="替换为你的xxapi_API_Key"
launchctl setenv XXAPI_API_KEY "$XXAPI_API_KEY"
```

这会让当前登录会话中新启动的应用读到该变量，重启或注销后要重新执行。要清除可执行 `launchctl unsetenv XXAPI_API_KEY`。

## 4. 打开本地 Codex，发第一条消息

重新打开 ChatGPT 桌面应用，选择 **Codex**，再选“打开文件夹”或“选择项目”，打开练习文件夹 `xxapi-demo`（Windows 输入 `%USERPROFILE%\xxapi-demo`，macOS 按 `Command + Shift + G` 输入 `~/xxapi-demo`）。

确认用的是本机上的 Codex 会话；网页版、云端和手机端不会因为改了这个本地文件而接入 xxapi。检查模型与 `config.toml` 一致，发送：

```text
请只回复“连接成功”，先不要读取或修改文件。
```

再到 xxapi [使用日志](https://xxapi.ai/usage-logs/common) 核对请求时间和模型。只看到应用有回复，还不能判断走的是哪家服务。

## 5. 以后切换模型或服务商

修改 `config.toml`，或在管理该文件的 [CC Switch](05-cc-switch.md) 里切换，然后 **完全退出桌面应用再重开**，新建会话检查模型。旧会话可能仍沿用原模型。更换了密钥，也要同步更新第 3 步的变量。

## 常见问题

**终端可用，桌面提示缺少密钥**：检查桌面所在系统和终端是否一致（尤其是 WSL）。Windows 注销登录后重试；macOS 重新执行 `launchctl setenv` 后，从应用菜单彻底退出再打开。

**仍要求登录官方账号**：确认是本地 Codex，检查应用版本、配置路径和环境变量。读取不到自定义服务商时，应用会落回默认登录流程。先让同一系统的 Codex CLI 读到正确配置。

**有回复，但 xxapi 没有记录**：核对日志的筛选范围和时间，确认是本地 Codex，新会话选中的模型和服务商正确。

完整图文教程：[https://docs.xxapi.ai/codex-desktop](https://docs.xxapi.ai/codex-desktop)

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
