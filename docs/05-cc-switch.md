# CC Switch 国内下载与配置：Claude Code、Codex 接入 xxapi

CC Switch 是 GitHub 上的开源软件，用图形界面保存和切换 Claude Code、Codex 的连接。国内下载可以用 xxapi（[https://xxapi.ai](https://xxapi.ai)）提供的镜像，文件与 GitHub 发布的是同一份。装好后添加自定义供应商：Claude Code 的 API 请求地址填 `https://xxapi.ai`、用 Claude Code 分组的 API 密钥（API Key）；Codex 的填 `https://xxapi.ai/v1`、用 Codex 分组的 API 密钥。

CC Switch 只负责保存和切换连接，Claude Code、Codex 本身还要分别安装，见 [Claude Code 教程](02-claude-code.md) 和 [Codex CLI 教程](03-codex-cli.md)。

## 1. 下载安装包

两种方式选一种，下到的是同一个安装包。

**国内镜像**（固定地址，始终指向镜像里的当前版本）：

| 系统 | 下载地址 | 下载到的文件名 |
| --- | --- | --- |
| Windows（x64） | [https://xxapi.ai/downloads/cc-switch/windows-x64.msi](https://xxapi.ai/downloads/cc-switch/windows-x64.msi) | `CC-Switch-windows-x64.msi` |
| Windows（ARM64） | [https://xxapi.ai/downloads/cc-switch/windows-arm64.msi](https://xxapi.ai/downloads/cc-switch/windows-arm64.msi) | `CC-Switch-windows-arm64.msi` |
| macOS | [https://xxapi.ai/downloads/cc-switch/macos.dmg](https://xxapi.ai/downloads/cc-switch/macos.dmg) | `CC-Switch-macos.dmg` |

- 镜像只把 GitHub 发布的安装包原样放到国内服务器，不改文件内容；每天检查一次 GitHub，新版本发布满 24 小时后才同步，所以可能比 GitHub 晚一两天。
- 镜像只放 Windows 和 macOS，Linux 安装包请从 GitHub 下载。
- 同时下载的人多时可能提示繁忙或下不动，这时改用 GitHub。
- 当前镜像的版本号和每个文件的 sha256 见 [latest.json](https://xxapi.ai/downloads/cc-switch/latest.json)。镜像不是 CC Switch 官方网站。

**GitHub 官方**：打开 [https://github.com/farion1231/cc-switch/releases/latest](https://github.com/farion1231/cc-switch/releases/latest)，展开 **Assets**，按系统和芯片选择安装包。

### 核对文件（可选）

把算出来的值和 latest.json 里同一平台的 `sha256` 比，完全一样就说明下载完整。

Windows PowerShell：

```powershell
Get-FileHash .\CC-Switch-windows-x64.msi -Algorithm SHA256
```

macOS 终端：

```bash
shasum -a 256 ~/Downloads/CC-Switch-macos.dmg
```

从 GitHub 下载的文件名带版本号，命令里换成实际文件名。

## 2. 准备 xxapi 密钥和模型

打开 [API 密钥](https://xxapi.ai/keys) 复制密钥，在 [模型广场](https://xxapi.ai/pricing) 记下完整模型 ID。Claude Code 和 Codex 各用一枚密钥，见 [注册与创建密钥](01-register-and-api-key.md)。

创建密钥后弹出的 **密钥已创建** 窗口里，也可以直接点 **导入 CC Switch** 一键导入。

安装后第一次打开 CC Switch，如果提示导入已有配置，先导入并保存备份，再新增 xxapi。

## 3. 配置 Claude Code

在 CC Switch 顶部选择 **Claude Code / Claude**，点 **添加供应商**，供应商选 **自定义**：

| 项目 | 填写内容 |
| --- | --- |
| 名称 | xxapi |
| 官网 | `https://xxapi.ai` |
| API 请求地址 | `https://xxapi.ai` |
| API Key | Claude Code 分组的 xxapi API 密钥 |
| API 格式 | Anthropic Messages |
| 默认模型 | 模型广场中的 Claude 模型 ID |

如果有 Haiku、Sonnet、Opus 模型映射，第一次把默认模型和三个映射都填成同一个真实的 Claude 模型 ID，以后需要再分别调整。

点 **添加 / 保存**，回到列表对 xxapi 点 **启用**。退出正在运行的 Claude Code，重新打开终端执行 `claude`，发送“请只回复：连接成功”。

第一次启动仍要求官方账号登录时：先确认已启用 xxapi；部分版本有 **跳过 Claude Code 初次确认** 选项，可用于 API 接入的首次初始化。还不行就检查终端里是否留着旧的 `ANTHROPIC_BASE_URL`、`ANTHROPIC_AUTH_TOKEN` 或 `ANTHROPIC_API_KEY`。

## 4. 配置 Codex

在顶部选择 **Codex**，添加自定义供应商：

| 项目 | 填写内容 |
| --- | --- |
| 名称 | xxapi |
| 官网 | `https://xxapi.ai` |
| API 请求地址 | `https://xxapi.ai/v1` |
| API Key | Codex 分组的 xxapi API 密钥 |
| 默认模型 | Codex 分组里的 GPT 模型 ID |
| Wire API / 协议 | `responses` |

保存后启用 xxapi。退出 Codex 再重新打开，执行 `codex`，发送“请只回复：连接成功”。

> 在 Codex 里经 CC Switch 转换调用 Claude 模型，可能遇到 `input_schema does not support oneOf/anyOf` 或 `thinking.type.disabled` 的 400 报错，这是 CC Switch 转换时的已知问题。用 Claude 模型就直接用 Claude Code，留在 Codex 就用 GPT 模型，见 [常见报错速查](09-errors.md)。

## 已经有其他服务商

在 CC Switch 中新增 xxapi，保留原服务商。切换时点对应配置的启用按钮，再重启目标工具；正在运行的会话可能继续用旧连接。手动写过系统环境变量的，也要核对它们是否覆盖了 CC Switch 写入的文件。

## 遇到问题

| 看到的情况 | 处理方法 |
| --- | --- |
| `claude` 或 `codex` 找不到 | CC Switch 不替代工具安装，先装对应工具 |
| 配了 Claude，Codex 却没变 | 两个应用分别配置、分别启用 |
| 401 | 核对当前应用用的密钥与 xxapi 地址是否匹配 |
| 404 | Claude 地址用根域 `https://xxapi.ai`，Codex 地址带 `/v1` |
| 保存了但没生效 | 点启用，退出旧会话，再检查遗留的环境变量 |

CC Switch 自身的使用问题和功能建议，请到它的 GitHub 仓库反馈。

完整图文教程：[https://docs.xxapi.ai/cc-switch](https://docs.xxapi.ai/cc-switch)（下载页：[https://docs.xxapi.ai/cc-switch-download](https://docs.xxapi.ai/cc-switch-download)）

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
