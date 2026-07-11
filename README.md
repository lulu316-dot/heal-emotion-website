# 跨时空情感疗愈网页

单文件 Canvas 情感疗愈网页，包含首页东西方碰撞、对话页粒子生命树、疗愈师匹配、情绪卡片生成。

## 本地运行

直接双击 `app.html` 即可打开。

如果浏览器限制 `fetch("api-config.json")`，请用本地静态服务器运行，例如：

```bash
python -m http.server 8080
```

然后访问：

```text
http://localhost:8080/app.html
```

## API 配置

真实 API Key 不要提交到 GitHub。

1. 复制示例文件：

```bash
copy api-config.example.json api-config.json
```

2. 在 `api-config.json` 中填写你的配置：

```json
{
  "enabled": true,
  "provider": "openai",
  "apiKey": "YOUR_API_KEY",
  "model": "YOUR_MODEL_ID",
  "endpoint": "https://your-provider.example.com/v1",
  "maxOutputTokens": 80,
  "temperature": 0.7
}
```

`api-config.json` 已写入 `.gitignore`，不会被提交。

## 注意

前端读取 API Key 只能避免把 Key 上传到 GitHub，不能防止浏览器端查看。正式上线建议使用后端代理隐藏 API Key。
