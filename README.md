# 🎨 Flux AI Pro - Hybrid Edition (v9.0.0)

[![Deploy to Cloudflare Workers](https://img.shields.io/badge/Deploy%20to-Cloudflare%20Workers-orange?style=for-the-badge&logo=cloudflare)](https://workers.cloudflare.com/)
[![Version](https://img.shields.io/badge/Version-9.0.0%20Hybrid-blue?style=for-the-badge)](https://github.com/kinai9661/Flux-AI-Pro)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Cost](https://img.shields.io/badge/Cost-混合架構%20免費%2F付費-success?style=for-the-badge)](https://developers.cloudflare.com/workers-ai/models/flux-1-schnell/)

> **基於 Cloudflare Workers 的混合架構 AI 圖像生成平台。**
> 
> **🆓 Pollinations.ai** (17 個免費模型 + Auto HD + 智能優化) + **⚡ Cloudflare Workers AI** (官方 FLUX.2 [dev] + 多圖輸入 + 企業級 SLA)

---

## 🆕 v9.0.0 混合架構亮點

### 雙提供商靈活選擇

| 提供商 | 成本 | 特性 | 適用場景 |
|--------|------|------|----------|
| **🆓 Pollinations** | 100% 免費 | 17 模型 + 12 風格 + NSFW + Auto HD | 個人項目、學習測試、無預算限制 |
| **⚡ Cloudflare AI** | 按量計費 | FLUX.2 官方 + 多圖輸入 + Hex 色碼 + 企業級穩定性 | 生產環境、商業項目、高級控制需求 |

### 🎯 核心升級

#### Cloudflare Workers AI 獨享功能
- **🖼️ 多圖參考輸入**: 最多上傳 4 張圖片引導生成 (Image-to-Image)
- **🎨 Hex 主題色**: 指定 #FF5733 格式的主題配色
- **💰 實時成本預估**: UI 自動計算費用並彈窗確認
- **⚡ 官方 FLUX.2 [dev]**: Black Forest Labs 官方模型，企業級 SLA
- **📊 精準成本計算**: 基於官方 $0.00062/tile/step 定價

#### 保留 v8.5.0 完整功能
- ✅ 自動高清 (Auto HD): 智能注入 8k/UHD 提示詞 + 尺寸優化
- ✅ 智能參數優化: 根據模型/尺寸/風格自動調整 Steps/Guidance
- ✅ 17 種頂級模型 (Pollinations): Flux Pro/Realism, SD3.5, SDXL Lightning 等
- ✅ 12 種藝術風格: 日漫、賽博朋克、寫實、油畫、水彩等
- ✅ NSFW 支持 + 私密模式
- ✅ OpenAI 兼容 API: 直接對接 NextChat/LobeChat
- ✅ 歷史記錄: 本地存儲最近 100 條

---

## 💸 Cloudflare AI 成本預估

基於官方定價 ([Workers AI Pricing](https://developers.cloudflare.com/workers-ai/platform/pricing/)):

| 尺寸 | 步數 | Tiles | 輸入成本 | 輸出成本 | **總計** |
|------|------|-------|----------|----------|---------|
| 512×512 | 20 | 1 | $0.0042 | $0.0082 | **$0.0124** |
| 1024×1024 | 30 | 4 | $0.0252 | $0.0492 | **$0.0744** |
| 1536×1536 | 35 | 9 | $0.0661 | $0.1292 | **$0.1953** |
| 2048×2048 | 40 | 16 | $0.1344 | $0.2624 | **$0.3968** |

> **計算公式**: `(input_per_tile × tiles × steps) + (output_per_tile × tiles × steps)`
> 
> **Tile 定義**: 每個 512×512 區域算 1 個 tile (例: 1024×1024 = 4 tiles)

**💡 成本對比**: Pollinations **完全免費**，Cloudflare AI 適合需要官方模型 + 高級功能的生產環境。

---

## 🚀 部署指南

### 前置要求
- [Node.js](https://nodejs.org/) (v18+)
- [Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/install-and-update/) (v3.0+)
- Cloudflare 賬號 (免費計劃即可)
- **(可選) Cloudflare Workers AI**: 需啟用付費 (綁定支付方式即可使用)

### 快速部署

#### 1. 克隆項目
```bash
git clone https://github.com/kinai9661/Flux-AI-Pro.git
cd Flux-AI-Pro
```

#### 2. 安裝 Wrangler
```bash
npm install -g wrangler
wrangler login
```

#### 3. 部署配置

**僅使用免費 Pollinations (跳過 Cloudflare AI)**:
```bash
# 直接部署，自動使用 Pollinations
wrangler deploy
```

**啟用 Cloudflare AI (混合架構)**:
```bash
# 1. 確保 wrangler.toml 包含 [ai] binding
# 2. 在 Cloudflare Dashboard 啟用 Workers AI (綁定支付方式)
# 3. 部署
wrangler deploy --env production

# 測試環境 (禁用 Cloudflare AI)
wrangler deploy --env dev
```

#### 4. 驗證部署
訪問 Worker URL (如 `https://flux-ai-pro.your-subdomain.workers.dev`):
- ✅ 提供商下拉框顯示 "Pollinations" 和 "Cloudflare AI"
- ✅ 切換到 Cloudflare AI 顯示成本預估卡片
- ✅ 生成圖片後查看成本顯示

---

## 🎨 模型與風格列表

### Pollinations.ai 免費模型 (17 個)

<details>
<summary><strong>查看完整列表 (點擊展開)</strong></summary>

| 分類 | 模型 ID | 描述 | 特性 |
|------|---------|------|------|
| **Flux 標準** | `flux` | 基礎版 | 均衡速度與質量 |
| | `flux-realism` | 超寫實 | 照片級細節 |
| | `flux-anime` | 動漫 | 日系二次元 |
| | `flux-3d` | 3D 渲染 | Blender/C4D 風格 |
| | `flux-pro` | 專業版 | 最高質量 |
| | `any-dark` | 暗黑 | 風格化強烈 |
| | `turbo` | 極速版 | 4-8 步出圖 |
| **Flux 高級** | `flux-1.1-pro` 🧪 | v1.1 Pro | 實驗性 (6x 速度) |
| | `flux-kontext` 🧪 | Context | 智能語境理解 |
| | `flux-kontext-pro` 🧪 | Context Pro | 專業語境控制 |
| **SD3 系列** | `sd3` 🧪 | SD3 標準 | 穩定性高 |
| | `sd3.5-large` 🧪 | SD3.5 Large | 🔥 旗艦畫質 |
| | `sd3.5-turbo` 🧪 | SD3.5 Turbo | 快速迭代 |
| **SDXL** | `sdxl` 🧪 | SDXL 1.0 | 經典模型 |
| | `sdxl-lightning` 🧪 | Lightning | 閃電生成 |

> 🧪 = 實驗性模型 (Pollinations 正在測試中，可能自動回退到穩定模型)

</details>

### Cloudflare Workers AI 官方模型

| 模型 ID | 名稱 | 特性 |
|---------|------|------|
| `flux-2-dev` | FLUX.2 [dev] ⚡ | 官方模型 + 多圖輸入 + Hex 色碼 |

### 12 種藝術風格 (兩提供商通用)

- 🎌 **Japanese Manga** (日本漫畫)
- ✨ **Anime** (動漫風格)
- 📷 **Photorealistic** (寫實攝影)
- 🌃 **Cyberpunk** (賽博朋克)
- 🎨 **Oil Painting** (油畫)
- 💧 **Watercolor** (水彩)
- 📐 **Vector** (矢量圖)
- 👾 **Pixel Art** (像素藝術)
- 🌿 **Studio Ghibli** (吉卜力)
- 💥 **Comic Book** (美式漫畫)
- ✏️ **Sketch** (素描)
- 🐉 **Fantasy** (奇幻)

---

## 🔌 API 文檔

### 1. 圖像生成 (Standard)

**Endpoint:** `POST /v1/images/generations`

#### Request Body (混合架構)
```json
{
  "provider": "cloudflare",  // 🆕 可選: "pollinations" (默認) 或 "cloudflare"
  "prompt": "a futuristic city with flying cars",
  "model": "flux-2-dev",     // Cloudflare: flux-2-dev | Pollinations: flux/flux-realism 等
  "width": 1024,
  "height": 1024,
  "n": 1,
  "auto_hd": true,           // v8.5.0: 自動高清
  "auto_optimize": true,     // v8.5.0: 智能優化
  "input_images": [          // 🆕 Cloudflare 專屬: Base64 圖片數組 (最多 4 張)
    "data:image/jpeg;base64,/9j/4AAQ..."
  ],
  "hex_color": "#FF5733",    // 🆕 Cloudflare 專屬: 主題色
  "private": true
}
```

#### Response
```json
{
  "created": 1733300000,
  "data": [
    {
      "url": "data:image/png;base64,...",  // Cloudflare: Base64 | Pollinations: URL
      "provider": "Cloudflare Workers AI",
      "model": "flux-2-dev",
      "width": 1024,
      "height": 1024,
      "seed": 123456,
      "hd_optimized": true,
      "auto_optimized": true,
      "cost": "$0.0744",       // 🆕 Cloudflare 顯示費用 | Pollinations: "FREE"
      "cost_breakdown": {      // 🆕 詳細成本
        "tiles": 4,
        "steps": 30,
        "input_cost": "0.025200",
        "output_cost": "0.049200",
        "total": "0.0744"
      },
      "tier": "premium",       // 🆕 "free" 或 "premium"
      "input_images": 2,       // 🆕 使用的參考圖片數
      "hex_color": "#FF5733"   // 🆕 使用的主題色
    }
  ]
}
```

### 2. 聊天生成 (OpenAI Compatible)

**Endpoint:** `POST /v1/chat/completions`

```json
{
  "model": "flux-pro",
  "provider": "pollinations",  // 🆕 可選
  "messages": [
    { "role": "user", "content": "畫一隻在太空的貓" }
  ],
  "width": 1024,
  "height": 1024,
  "auto_hd": true
}
```

### 3. 查詢接口

| Endpoint | 方法 | 描述 |
|----------|------|------|
| `/v1/models` | GET | 列出所有可用模型 (兩提供商) |
| `/v1/providers` | GET | 查詢提供商信息 |
| `/v1/styles` | GET | 列出所有風格預設 |
| `/health` | GET | 健康檢查 |

---

## ⚙️ 配置文件

### wrangler.toml
```toml
name = "flux-ai-pro"
main = "worker.js"
compatibility_date = "2025-12-04"

# 🆕 啟用 Cloudflare Workers AI
[ai]
binding = "AI"

[vars]
ENABLE_CLOUDFLARE = "true"
PROJECT_VERSION = "9.0.0"

# 開發環境 (禁用 Cloudflare AI)
[env.dev]
vars = { ENABLE_CLOUDFLARE = "false" }

# 生產環境
[env.production]
vars = { ENABLE_CLOUDFLARE = "true" }
```

### worker.js 核心配置
```javascript
const CONFIG = {
  PROJECT_VERSION: "9.0.0",
  DEFAULT_PROVIDER: "pollinations",  // 默認使用免費服務
  
  PROVIDERS: {
    pollinations: {
      enabled: true,
      tier: "free",
      models: [ /* 17 個模型 */ ]
    },
    cloudflare: {
      enabled: true,
      tier: "premium",
      pricing: {
        input_per_tile: 0.00021,
        output_per_tile: 0.00041
      }
    }
  },
  
  // v8.5.0 功能保留
  HD_OPTIMIZATION: { enabled: true },
  OPTIMIZATION_RULES: { /* 智能優化規則 */ }
};
```

---

## 📅 更新日誌

### v9.0.0 (2025-12-04) - 🚀 混合架構版
- **重大更新**: 集成 Cloudflare Workers AI (FLUX.2 官方模型)
- **新增**: 雙提供商切換 UI (免費/付費)
- **新增**: 實時成本預估 + 確認彈窗
- **新增**: 多圖參考輸入 (Cloudflare 專屬，最多 4 張)
- **新增**: Hex 色碼主題控制 (Cloudflare 專屬)
- **新增**: `CloudflareProvider` 類 + 成本計算邏輯
- **優化**: `MultiProviderRouter` 支持動態提供商選擇
- **保留**: v8.5.0 所有功能 (Auto HD、智能優化、17 模型、12 風格)

### v8.5.0 (2025-11-29) - 💎 自動高清版
- **新增**: Auto HD (自動高清) 功能
- **新增**: `HDOptimizer` 類
- **優化**: Web UI 高清開關

### v8.4.0 - 🎬 動態 UI
- **新增**: 實時進度條模擬
- **新增**: 狀態消息反饋

### v8.3.0 - 🧠 智能優化
- **新增**: 自動計算 Steps/Guidance

### v8.0.0 - 🦄 架構重構
- **重構**: 多提供商架構
- **新增**: 歷史記錄系統

---

## 🌐 演示與部署

- **最新演示站**: [https://koy.xx.kg/](https://koy.xx.kg/) *(v8.5.0 - 純免費版)*
- **GitHub 倉庫**: [kinai9661/Flux-AI-Pro](https://github.com/kinai9661/Flux-AI-Pro)
- **部署平台**: Cloudflare Workers (免費計劃支持)

### 一鍵部署

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/kinai9661/Flux-AI-Pro)

---

## 💡 使用建議

### 選擇 Pollinations (免費) 當:
- 個人學習、娛樂使用
- 預算為零
- 不需要官方模型保證
- 可接受偶爾的服務波動

### 選擇 Cloudflare AI (付費) 當:
- 生產環境部署
- 商業項目需要 SLA
- 需要多圖參考輸入功能
- 需要精確色彩控制
- 願意為質量和穩定性付費

### 混合使用策略:
1. **日常測試**: 使用 Pollinations 免費試驗
2. **正式交付**: 切換到 Cloudflare AI 生成最終版
3. **成本控制**: 設置每日預算提醒 (Cloudflare Dashboard)

---

## ⚠️ 重要提醒

### Cloudflare Workers AI
1. **需要綁定支付方式** (信用卡/PayPal)，但僅按實際使用量計費
2. **免費額度**: 前 10,000 神經元 (Neurons) 免費/天 ([官方詳情](https://developers.cloudflare.com/workers-ai/platform/pricing/))
3. **成本控制**: 建議在 Dashboard 設置預算警報
4. **API 限制**: 並發請求受賬戶等級限制

### Pollinations.ai
1. 完全免費，但服務穩定性由第三方控制
2. 請遵守其 [使用條款](https://pollinations.ai/terms)
3. 部分實驗性模型可能不可用 (自動回退)

### 法律與責任
- 請勿生成非法、仇恨或違反當地法律的內容
- NSFW 功能僅供合法成年人使用
- 用戶需自行承擔生成內容帶來的責任

---

## 🤝 貢獻

歡迎提交 Issue 或 Pull Request!

### 開發指南
```bash
# 本地開發
wrangler dev

# 類型檢查
npm run typecheck  # (如果項目使用 TypeScript)

# 部署測試環境
wrangler deploy --env dev
```

---

## 📄 許可證

MIT License - 查看 [LICENSE](LICENSE) 文件

---

<div align="center">
  <sub>Made with ❤️ by <a href="https://github.com/kinai9661">kinai9661</a> | Powered by Cloudflare Workers & Pollinations.ai</sub>
  <br><br>
  <a href="https://workers.cloudflare.com">
    <img src="https://img.shields.io/badge/Cloudflare-Workers-orange?logo=cloudflare&style=flat-square" alt="Cloudflare Workers">
  </a>
  <a href="https://pollinations.ai">
    <img src="https://img.shields.io/badge/Pollinations-AI-green?style=flat-square" alt="Pollinations AI">
  </a>
</div>