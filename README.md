<div align="center">

# 跨时空情感疗愈

一个以东西方哲学为人格内核、以 Canvas 粒子生命树为视觉反馈的情绪对话网页。

`原生 HTML` · `Canvas 2D` · `零构建依赖` · `桌面与移动端适配`

</div>

---

## 项目简介

用户从首页进入后写下当下的烦恼，系统会在 10 位疗愈师中匹配更贴合的哲学人格，并在对话过程中驱动粒子生命树逐步生长。任何阶段都可以生成一张包含树画面、疗愈师、时间与哲理金句的情绪卡片。

项目不依赖框架或构建工具，核心体验集中在单文件 [app.html](./app.html) 中。根目录 [index.html](./index.html) 是 GitHub Pages 入口，会自动进入最新版应用。

## 核心体验

| 模块 | 内容 |
| --- | --- |
| 首页 | 太极星尘、几何星座、中央碰撞火花与向内坍缩转场 |
| 疗愈师匹配 | 在王阳明、庄子、苏轼、老子、孔孟、奥勒留、尼采、加缪、叔本华、阿德勒中匹配 |
| 对话 | 支持本地智能模拟回复，也可在本地接入 OpenAI 兼容 API |
| 粒子生命树 | 五阶段生长、哲学家专属形态、鼠标交互与结晶效果 |
| 情绪卡片 | 390 × 680 Canvas 合成、移动端预览与 PNG 下载 |
| 性能保护 | 对象池、离屏缓存、页面隐藏暂停、自适应粒子档位 |

## 快速开始

### 直接体验

双击 `index.html` 或 `app.html` 即可运行。未配置 API 时，应用会自动使用内置的本地智能回复。

### 使用本地服务器

浏览器可能限制本地文件读取配置，建议在项目目录启动静态服务器：

```bash
python -m http.server 8080
```

然后访问：

```text
http://localhost:8080/
```

## 本地 API 配置

> [!WARNING]
> 真实 API Key 只能保存在被 `.gitignore` 排除的本地配置中。不要把 Key 写入 `app.html`、README、示例文件或任何准备提交的文件。

复制一份示例配置：

```powershell
Copy-Item api-config.example.json api-config.json
```

在本地 `api-config.json` 中填写：

```json
{
  "enabled": true,
  "provider": "mimo",
  "apiKey": "PASTE_YOUR_API_KEY_HERE",
  "model": "mimo-v2.5-pro",
  "endpoint": "https://api.xiaomimimo.com/v1/chat/completions",
  "maxOutputTokens": 2048,
  "temperature": 0.7
}
```

以下文件默认不会被 Git 跟踪：

```text
api-config.json
api-config.js
api-config.local.*
.env
.env.*
```

提交前可以运行：

```bash
git check-ignore api-config.json api-config.js
git status --short --ignored
```

输出中应看到配置文件以 `!!` 标记为已忽略，并且不能出现在普通的待提交文件列表中。

### 关于前端 API Key

`.gitignore` 只能防止 Key 被上传到 GitHub，不能阻止访问者在浏览器开发者工具中看到前端请求携带的 Key。因此：

- 本地个人使用：可以使用被忽略的配置文件。
- 公开 GitHub Pages：建议保留本地模拟回复，不要部署真实 Key。
- 公开站点使用真实 API：应通过后端或 Serverless 代理调用，并把 Key 存入服务端环境变量。

## GitHub Pages 发布

1. 将本项目推送到 GitHub 仓库。
2. 在仓库 `Settings > Pages` 中选择从分支部署。
3. 选择发布分支和根目录 `/`。
4. Pages 会打开根目录 `index.html`，并进入 `app.html`。

发布前请再次确认 `api-config.json`、`api-config.js`、`.env` 和录屏文件没有被提交。

## 文件结构

```text
.
├─ index.html                  # GitHub Pages 入口
├─ app.html                    # 完整生产版应用
├─ README.md                   # 项目说明
├─ .gitignore                  # API、媒体和本地文件保护
├─ api-config.example.json     # 安全的 JSON 配置模板
├─ api-config.example.js       # 安全的 JS 配置模板
├─ tree-engine.html            # 粒子树独立原型
├─ taiji-spiral-home.html      # 太极星尘独立原型
├─ chat.html                   # 对话页独立原型
├─ card-generator.html         # 卡片生成独立原型
└─ 1.html                      # 早期实验页面
```

## 浏览器与性能

- 推荐最新版 Chrome、Edge、Safari 或 Firefox。
- 页面不可见时会暂停 Canvas 动画。
- 低 FPS 持续出现时会自动降低动态粒子绘制量。
- 移动端会使用更低的粒子数量和响应式上下布局。

## 隐私说明

对话历史默认只存在于当前浏览器页面内，项目本身不包含数据库。接入第三方 API 后，用户输入会发送给对应 API 服务，请根据实际部署场景补充隐私政策和用户告知。
