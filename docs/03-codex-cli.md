# Codex 中转站配置：Codex CLI 配置 API

Codex CLI 接入 xxapi（[https://xxapi.ai](https://xxapi.ai)）要填三项：`~/.codex/config.toml` 里 `base_url` 填 `https://xxapi.ai/v1`（`wire_api` 为 `"responses"`），环境变量 `XXAPI_API_KEY` 填 Codex 分组的 API 密钥（API Key），`model` 填模型广场里 Codex 分组的 GPT 模型 ID。xxapi 的接入地址国内可直接访问，不需要登录 OpenAI 官方账号。

下面使用官方独立安装程序，无需预装 Node.js。

## 1. 选好模型和密钥

打开 [模型广场](https://xxapi.ai/pricing)，在 Codex 分组里选一个 GPT 模型，复制完整 ID。再到 [API 密钥](https://xxapi.ai/keys) 创建一枚选择同一分组的密钥。Claude Code 分组的密钥不能用在 Codex 上，原因见 [注册与创建密钥](01-register-and-api-key.md)。

## 2. 安装 Codex

Windows（PowerShell）：

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

macOS / Linux：

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

安装结束后重新开终端，检查版本：

```sh
codex --version
```

## 3. 打开个人配置文件

Windows PowerShell（记事本询问是否创建新文件时选“是”）：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex" | Out-Null
notepad "$env:USERPROFILE\.codex\config.toml"
```

macOS / Linux：

```bash
mkdir -p ~/.codex
nano ~/.codex/config.toml
```

在 nano 中粘贴后按 `Ctrl + O`、回车保存，再按 `Ctrl + X` 退出。文件已有内容时，先复制一份备份。

## 4. 写入服务商配置

新文件直接粘贴下面全部内容，把 `model` 后的文字换成第 1 步复制的模型 ID，其余保持不变：

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

前三行要放在文件开头、任何 `[方括号]` 表名之前。`env_key` 填的是变量名称，真实密钥下一步再填。

**已有旧配置**：把顶层 `model_provider` 改成 `xxapi`，更新 `model`，再添加 `[model_providers.xxapi]`；已有同名表就修改它，不要复制出第二个。这个服务商表里不要同时加 `requires_openai_auth = true`，它会切换到另一套登录凭据。设置了 `CODEX_HOME` 或启动时带 `--profile` 的，Codex 可能读的是另一份配置。

## 5. 在终端填入密钥

Windows PowerShell：

```powershell
$env:XXAPI_API_KEY = "替换为你的xxapi_API_Key"
```

macOS / Linux：

```bash
export XXAPI_API_KEY="替换为你的xxapi_API_Key"
```

已有的 `auth.json` 可以保留，不需要编辑。

## 6. 启动并发第一条消息

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\xxapi-demo" | Out-Null
Set-Location "$env:USERPROFILE\xxapi-demo"
codex
```

macOS / Linux：

```bash
mkdir -p ~/xxapi-demo
cd ~/xxapi-demo
codex
```

进入后输入 `/status`，检查服务商为 `xxapi`、模型为你填入的 ID。然后发送：

```text
请只回复“连接成功”，先不要读取或修改文件。
```

收到回复后，到 xxapi [使用日志](https://xxapi.ai/usage-logs/common) 核对时间和模型。之后进入自己的项目目录运行 `codex` 即可。

`config.toml` 已经保存，但密钥只在刚才的窗口里有效；下次打开终端重新执行第 5 步，或用系统环境变量长期保存 `XXAPI_API_KEY`。

## 常见问题

**提示缺少 XXAPI_API_KEY**：第 5 步和启动 Codex 要在同一个窗口。不要把真实密钥填进 `env_key` 的引号里。

**404、模型不存在或接口不支持**：检查 Base URL 是 `https://xxapi.ai/v1`、没有重复 `/v1`；模型是 Codex 分组里的 GPT 模型，这枚密钥也选了同一分组，模型 ID 没有多余空格。

**仍然出现旧服务商，或 TOML 报重复字段**：顶层 `model_provider` 要和服务商表名一致，并位于第一个表头之前。完全退出 Codex 后新开会话，再看 `/status`。

**中途换模型后“压缩已中断”**：新开一个对话，一开始就选分组里有的模型，见 [常见报错速查](09-errors.md)。

想用桌面窗口，继续看 [Codex 桌面版配置](04-codex-desktop.md)。

完整图文教程：[https://docs.xxapi.ai/codex](https://docs.xxapi.ai/codex)

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
