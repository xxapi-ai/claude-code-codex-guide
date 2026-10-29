# Claude Code 国内使用教程：安装并配置中转 API

Claude Code 接入 xxapi（[https://xxapi.ai](https://xxapi.ai)）要填三项：`ANTHROPIC_BASE_URL` 填 `https://xxapi.ai`（末尾不加 `/v1`），`ANTHROPIC_AUTH_TOKEN` 填 Claude Code 分组的 API 密钥（API Key），`ANTHROPIC_MODEL` 填模型广场里的 Claude 模型 ID。xxapi 的接入地址国内可直接访问，不需要登录 Anthropic 官方账号。

Windows 10 1809 及以上、macOS 13 及以上、常见 Linux 发行版均可使用。下面采用官方原生安装，不需要先装 Node.js。

## 1. 准备密钥与模型

打开 [API 密钥](https://xxapi.ai/keys)，创建或复制一枚 Claude Code 分组的密钥（还没有账号先看 [注册与创建密钥](01-register-and-api-key.md)）。再从 [模型广场](https://xxapi.ai/pricing) 复制要使用的 Claude 模型 ID。

## 2. 打开终端

- **Windows**：按 `Win + R`，输入 `powershell`，回车。提示符以 `PS` 开头即可，无需管理员权限。已经在 WSL 里工作的，全程用下面的 Linux 步骤。
- **macOS**：按 `Command + 空格`，搜索“终端”并打开。
- **Linux**：打开系统的 Terminal。

## 3. 安装并检查版本

Windows PowerShell：

```powershell
irm https://claude.ai/install.ps1 | iex
```

macOS / Linux：

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

安装完成后，关闭终端再重新打开，执行：

```sh
claude --version
```

显示版本号即安装成功。

## 4. 填入 xxapi 配置

把两处占位文字换成自己的 API 密钥和模型 ID，再执行。地址保持 `https://xxapi.ai`，末尾不加 `/v1`。

Windows PowerShell：

```powershell
$env:ANTHROPIC_BASE_URL = "https://xxapi.ai"
$env:ANTHROPIC_AUTH_TOKEN = "替换为你的xxapi_API_Key"
$env:ANTHROPIC_MODEL = "替换为模型广场中的Claude模型ID"
```

macOS / Linux：

```bash
export ANTHROPIC_BASE_URL="https://xxapi.ai"
export ANTHROPIC_AUTH_TOKEN="替换为你的xxapi_API_Key"
export ANTHROPIC_MODEL="替换为模型广场中的Claude模型ID"
```

执行后没有新文字是正常的，暂时不要关闭这个窗口。

**以前配置过其他服务**：先备份 `~/.claude/settings.json`（Windows 是 `%USERPROFILE%\.claude\settings.json`），把里面 `env` 的旧地址、旧密钥和模型改成 xxapi 的值，不要留两套。设置过 `ANTHROPIC_API_KEY` 的，不要和 `ANTHROPIC_AUTH_TOKEN` 同时保留不同的密钥。用 CC Switch 管理的配置，应在 CC Switch 里改。

## 5. 进入练习文件夹并启动

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\xxapi-demo" | Out-Null
Set-Location "$env:USERPROFILE\xxapi-demo"
claude
```

macOS / Linux：

```bash
mkdir -p ~/xxapi-demo
cd ~/xxapi-demo
claude
```

按提示选择主题。遇到文件夹信任确认时，核对路径是 `xxapi-demo` 后再继续。

## 6. 核对地址，发第一条消息

输入 `/status`，确认 `Anthropic base URL` 是 `https://xxapi.ai`，凭据来源是 `ANTHROPIC_AUTH_TOKEN`，模型与刚才选择的一致。按 Esc 回到输入框，发送：

```text
请只回复“连接成功”，先不要读取或修改文件。
```

收到回复后，到 xxapi [使用日志](https://xxapi.ai/usage-logs/common) 里能看到这次请求。

## 7. 保存设置，下次直接使用

刚才的配置只在那个终端窗口里有效。连接成功后，把设置写进个人配置文件 `settings.json`：

- Windows：按 `Win + R`，输入 `%USERPROFILE%\.claude` 回车，打开或新建 `settings.json`（记事本保存类型选“所有文件”）。
- macOS / Linux：文件在 `~/.claude/settings.json`。

空文件填入下面的内容；已经有设置的，只把这三项合并到现有 `env`，保留其他内容。

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://xxapi.ai",
    "ANTHROPIC_AUTH_TOKEN": "替换为你的xxapi_API_Key",
    "ANTHROPIC_MODEL": "替换为模型广场中的Claude模型ID"
  }
}
```

文件里有密钥，留在自己电脑上即可。新开终端运行 `claude`，`/status` 仍显示 xxapi 就完成了。

## 常见问题

**提示找不到 claude**：先重新开终端。Windows 可执行 `& "$env:USERPROFILE\.local\bin\claude.exe" --version`，macOS / Linux 可执行 `~/.local/bin/claude --version`。完整路径能运行时，把对应 `.local/bin` 目录加入用户 Path。

**一直要求官方登录，或仍使用旧地址**：第 4 步和启动 Claude Code 必须在同一个终端窗口里完成。检查个人设置和项目下的 `.claude/settings.local.json`，再用 `/status` 看实际生效的地址。

**主模型能用，辅助模型报错**：Claude Code 的辅助任务可能用其他 Claude 模型，密钥分组需要包含该模型。到模型广场找对应可用的模型，或把报错和请求时间发给 support@xxapi.ai。

更多报错见 [常见报错速查](09-errors.md)。

完整图文教程：[https://docs.xxapi.ai/claude-code](https://docs.xxapi.ai/claude-code)

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
