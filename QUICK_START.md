# 🚀 Flux-AI-Pro 快速開始指南

> **選項 A：純免費模式** - 100% 免費使用 Pollinations.ai，無需支付方式

---

## 📚 目錄

- [前置要求](#前置要求)
- [一鍵部署](#一鍵部署)
- [手動部署](#手動部署)
- [驗證部署](#驗證部署)
- [API 使用](#api-使用)
- [常見問題](#常見問題)

---

## 📦 前置要求

### 1. **Node.js** (必須)
- 版本：v18 或更高
- 下載：[https://nodejs.org/](https://nodejs.org/)
- 驗證安裝：
  ```bash
  node -v
  # 應顯示 v18.x.x 或更高
  ```

### 2. **Cloudflare 賬戶** (免費)
- 註冊：[https://dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up)
- ✅ 完全免費，無需綁定支付方式

### 3. **Git** (可選)
- 用於克隆倉庫
- 下載：[https://git-scm.com/](https://git-scm.com/)

---

## ⚡ 一鍵部署

### macOS / Linux

```bash
# 1. 克隆倉庫
git clone https://github.com/kinai9661/Flux-AI-Pro.git
cd Flux-AI-Pro

# 2. 給予執行權限
chmod +x deploy-free.sh

# 3. 一鍵部署
./deploy-free.sh
```

### Windows

```cmd
REM 1. 克隆倉庫
git clone https://github.com/kinai9661/Flux-AI-Pro.git
cd Flux-AI-Pro

REM 2. 一鍵部署
deploy-free.bat
```

### 腳本會自動：
1. ✅ 檢查 Node.js 安裝
2. ✅ 安裝 Wrangler CLI
3. ✅ 登錄 Cloudflare 賬戶
4. ✅ 部署到開發環境
5. ✅ 顯示訪問 URL

---

## 🔧 手動部署

如果你喜歡手動控制每一步：

### 步驟 1：安裝 Wrangler CLI

```bash
npm install -g wrangler
```

### 步驟 2：登錄 Cloudflare

```bash
wrangler login
```

✨ 會自動打開瀏覽器進行授權

### 步驟 3：克隆倉庫

```bash
git clone https://github.com/kinai9661/Flux-AI-Pro.git
cd Flux-AI-Pro
```

### 步驟 4：部署

```bash
# 部署到開發環境 (純免費模式)
wrangler deploy --env dev
```

### 步驟 5：獲取 URL

部署完成後，終端會顯示 Worker URL：

```
Published flux-ai-pro (dev)
  https://flux-ai-pro.your-subdomain.workers.dev
```

---

## ✅ 驗證部署

### 1. 訪問 Web 界面

直接在瀏覽器中打開 Worker URL：

```
https://your-worker.workers.dev
```

你會看到完整的 AI 圖像生成界面！

### 2. 測試 API 接口

#### 健康檢查

```bash
curl https://your-worker.workers.dev/health
```

**預期回應**：
```json
{
  "status": "ok",
  "version": "9.0.0",
  "providers": ["pollinations"],
  "cloudflare_ai_available": false,
  "timestamp": "2025-12-04T08:00:00.000Z"
}
```

#### 查看模型列表

```bash
curl https://your-worker.workers.dev/v1/models
```

**預期回應**：
```json
{
  "object": "list",
  "data": [
    {
      "id": "flux",
      "name": "Flux",
      "provider": "pollinations",
      "tier": "free"
    },
    ...
  ],
  "total": 17
}
```

---

## 💻 API 使用

### 基本圖像生成

```bash
curl -X POST https://your-worker.workers.dev/v1/images/generations \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "a beautiful sunset over mountains",
    "model": "flux-realism",
    "width": 1024,
    "height": 1024,
    "n": 1,
    "auto_hd": true,
    "auto_optimize": true
  }'
```

### 使用風格預設

```bash
curl -X POST https://your-worker.workers.dev/v1/images/generations \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "a cute cat",
    "model": "flux-anime",
    "style": "anime",
    "width": 1024,
    "height": 1024
  }'
```

### OpenAI 兼容模式

```bash
curl -X POST https://your-worker.workers.dev/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "flux-pro",
    "messages": [
      {"role": "user", "content": "畫一隻在太空的貓"}
    ]
  }'
```

### Python 示例

```python
import requests

url = "https://your-worker.workers.dev/v1/images/generations"

payload = {
    "prompt": "a futuristic city at night",
    "model": "flux-realism",
    "width": 1024,
    "height": 1024,
    "auto_hd": True,
    "auto_optimize": True
}

response = requests.post(url, json=payload)
data = response.json()

print(f"Image URL: {data['data'][0]['url']}")
```

### JavaScript 示例

```javascript
const response = await fetch('https://your-worker.workers.dev/v1/images/generations', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    prompt: 'a dragon in the sky',
    model: 'flux-anime',
    width: 1024,
    height: 1024,
    auto_hd: true
  })
});

const data = await response.json();
console.log('Image URL:', data.data[0].url);
```

---

## ❓ 常見問題

### Q1: 部署失敗，提示 "Authentication error"

**解決方法**：
```bash
# 重新登錄
wrangler logout
wrangler login

# 重試部署
wrangler deploy --env dev
```

### Q2: 如何更新已部署的 Worker？

**方法1：使用腳本**：
```bash
# 重新執行部署腳本
./deploy-free.sh  # macOS/Linux
deploy-free.bat   # Windows
```

**方法2：手動部署**：
```bash
# 拉取最新代碼
git pull

# 重新部署
wrangler deploy --env dev
```

### Q3: 生成的圖片在哪裡？

Pollinations.ai 返回的是 **圖片 URL**，不是 Base64。你可以：
- 直接在瀏覽器中打開 URL
- 下載圖片到本地
- 嵌入到你的網站/應用

### Q4: 我可以使用多少次？

✅ **完全無限制！**
- Pollinations.ai 完全免費
- Cloudflare Workers 免費計劃每天 100,000 請求
- 無需信用卡

### Q5: 如何啟用 Cloudflare AI？

查看下一個文檔：`PREMIUM_GUIDE.md`（即將推出）

或使用付費部署腳本：
```bash
./deploy-premium.sh  # macOS/Linux
deploy-premium.bat   # Windows
```

### Q6: Worker URL 是什麼？

部署後，Cloudflare 會生成一個類似這樣的 URL：

```
https://flux-ai-pro.<你的子域>.workers.dev
```

你也可以在 Cloudflare Dashboard 中：
1. 點擊 **Workers & Pages**
2. 選擇 **flux-ai-pro**
3. 查看 **Preview** 或 **Custom Domains**

### Q7: 可以綁定自定義域名嗎？

✅ **可以！**

1. 在 Cloudflare Dashboard 中點擊 Worker
2. 選擇 **Settings** > **Domains & Routes**
3. 點擊 **Add Custom Domain**
4. 輸入你的域名（例：`api.yourdomain.com`）

---

## 🎉 成功！

現在你已經成功部署了一個完全免費的 AI 圖像生成服務！

### 🔗 相關連結

- **GitHub 倉庫**: https://github.com/kinai9661/Flux-AI-Pro
- **完整文檔**: [README.md](README.md)
- **API 參考**: 查看 README.md 中的 API 文檔章節
- **Cloudflare Dashboard**: https://dash.cloudflare.com/

### 👍 下一步

1. ⭐ **Star 這個倉庫** 支持開發
2. 🐛 **提交 Issue** 報告問題
3. 🔀 **Fork 這個項目** 自定義修改
4. 💬 **分享你的作品** 在 GitHub Discussions

---

<div align="center">
  <sub>Made with ❤️ by <a href="https://github.com/kinai9661">kinai9661</a></sub>
  <br>
  <sub>Powered by Cloudflare Workers & Pollinations.ai</sub>
</div>
