# GPT Image 2 API 调用示例：curl、Python 生成图片（xxapi）

在 xxapi（[https://xxapi.ai](https://xxapi.ai)）上调用 GPT Image 2：用生图分组的 API 密钥（API Key），向 `https://xxapi.ai/v1/images/generations` 发 OpenAI 兼容的图片请求，`model` 填 `gpt-image-2` 就能出图。按张计价，不按 token，每张价格看 [模型广场](https://xxapi.ai/pricing) 的生图分组或 [价格表](https://docs.xxapi.ai/pricing)。

## 1. 准备密钥

在 [API 密钥页面](https://xxapi.ai/keys) 创建一枚 **生图** 分组的密钥，放进环境变量（macOS、Linux 终端）：

```bash
export XXAPI_API_KEY="替换为你的xxapi_API_Key"
```

## 2. 用 curl 生成一张图

```bash
curl https://xxapi.ai/v1/images/generations \
  -H "Authorization: Bearer $XXAPI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-image-2",
    "prompt": "一只戴圆框眼镜的橘猫坐在书桌前，温暖的手绘插画，正方形构图，不要文字",
    "n": 1,
    "size": "1024x1024"
  }'
```

返回的是 JSON，`data` 里每张图一项：

```json
{
  "created": 1761700000,
  "data": [
    { "b64_json": "iVBORw0KGgoAAAANSUhEUgAA..." }
  ]
}
```

- `b64_json` 是图片本身（base64 编码），解码后保存成文件即可。
- 有时这一项给的是 `url`（图片地址）而不是 `b64_json`，两种都要处理；图片地址会过期，拿到后尽快下载。
- 按生成的张数扣费，`n` 是一次要几张，第一次测试填 `1`。
- 生成一张需要等一会儿，不要连续重复发送。

## 3. 用 Python 保存图片

需要 `openai` 库（`pip install openai`）：

```python
import base64, os, urllib.request
from openai import OpenAI

client = OpenAI(base_url="https://xxapi.ai/v1", api_key=os.environ["XXAPI_API_KEY"])
result = client.images.generate(model="gpt-image-2", prompt="一只戴圆框眼镜的橘猫，手绘插画", n=1, size="1024x1024")
image = result.data[0]
if image.b64_json:
    open("cat.png", "wb").write(base64.b64decode(image.b64_json))
else:
    urllib.request.urlretrieve(image.url, "cat.png")
```

## 4. 修改已有图片

改图用 `https://xxapi.ai/v1/images/edits`（上传图片，`multipart/form-data`），参数与 OpenAI 的图片编辑接口相同。

## 5. 不写代码：在 Cherry Studio 里出图

在 Cherry Studio 的 **设置 → 模型服务 → 添加** 里新增提供商：名称 `xxapi · GPT Image 2`，提供商类型选 `New API`，API 地址填 `https://xxapi.ai`，密钥填生图分组的密钥。添加模型 `gpt-image-2`，把端点设为 **图像生成（OpenAI）**，然后在 **+ → 绘画** 里选这个模型生成。需要改图时，再给模型加 **图像编辑（OpenAI）** 端点。

## 常见问题

- **提示“图片请求未通过内容安全审核”**：提示词或上传的图片没有通过审核，改写提示词或换一张图片再试，原样重试还会失败。
- **当前分组 … 暂不支持模型 …**：确认用的是生图分组的密钥，模型 ID 与模型广场一致。
- **Failed to fetch 或总在相近时长中断**：先确认能打开 `https://xxapi.ai`，再检查本地代理和客户端的超时设置。带大图改图时，请求超过 64 MB 也会失败。
- **返回 HTML 或 Unexpected token**：地址误填成了登录页、控制台地址或完整请求路径。

完整图文教程：[https://docs.xxapi.ai/image-2](https://docs.xxapi.ai/image-2)

注册：[https://xxapi.ai/sign-up](https://xxapi.ai/sign-up)
