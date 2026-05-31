[English](./README.md) | [Deutsch](./README.de.md) | [Español](./README.es.md) | [Français](./README.fr.md) | [日本語](./README.ja.md) | [한국어](./README.ko.md) | [Português](./README.pt.md) | [繁體中文](./README.zh-TW.md)

# Google Maps Agent Skills

> 一套用於 Google Maps 開發客戶的 Claude Code / OpenClaw 技能集合。
> 每個技能可獨立安裝，各自對應不同的使用場景。

## 技能列表

| 技能 | 說明 | 點數 |
|------|------|------|
| [`google-maps-scraper`](./google-maps-scraper/) | 從 Google Maps 擷取商家資料 | 2/次搜尋 |
| [`google-maps-leads`](./google-maps-leads/) | 產生帶評分的潛在客戶名單 | 2/次搜尋 |
| [`local-business-finder`](./local-business-finder/) | 依產業類別與地點搜尋商家 | 2/次搜尋 |
| [`business-email-extractor`](./business-email-extractor/) | 擷取已驗證的商業電子郵件 | 2/次搜尋 |
| [`google-maps-export`](./google-maps-export/) | 匯出為 CSV/JSON/HubSpot/Pipedrive | 2/次搜尋 |
| [`cold-email-local-business`](./cold-email-local-business/) | 從 CSV 資料撰寫客製化開發信 | 免費 |
| [`competitor-analysis-local`](./competitor-analysis-local/) | 從 CSV 資料分析競爭對手 | 免費 |
| [`google-maps-reviews-scraper`](./google-maps-reviews-scraper/) | 分析評論與商譽 | 免費 |

## 安裝

```bash
# 透過 ClawHub
npx clawhub@latest install gmapsscraper/google-maps-scraper

# 透過 GitHub (npx skills)
npx skills add gmapsscraper/google-maps-agent-skills/google-maps-scraper

# 手動安裝
cp -r google-maps-scraper/ ~/.claude/skills/
```

## 快速開始

```bash
# 1. 取得免費 API 金鑰：https://gmapsscraper.io/dashboard
export GMAPS_SCRAPER_API_KEY=gmaps_sk_your_key_here

# 2. 安裝技能
npx clawhub@latest install gmapsscraper/google-maps-scraper

# 3. 對你的 Agent 說：
# 「幫我找台北所有的牙醫診所，要有 email」
```

## 運作方式

```
安裝技能 → Agent 獲得開發客戶的能力
                    ↓
        使用者說「幫我找高雄的水電行」
                    ↓
        技能呼叫 gmapsscraper.io API（消耗 2 點）
                    ↓
        回傳商家資料（店名、電話、email、評分⋯）
                    ↓
        使用免費技能處理資料（寫開發信、做分析）
                    ↓
        點數用完 → 到 gmapsscraper.io 升級方案
```

## 雙層設計

**付費技能**（需要 API 金鑰 + 點數）：從 Google Maps 擷取最新資料。
- 自動地理編碼：只要說「信義區牙醫」就好 — 不需要輸入座標
- 消耗點數前會先確認
- 建議使用免費技能做後續處理

**免費技能**（不需要 API 金鑰）：在本機處理現有的 CSV 資料。
- 撰寫客製化開發信
- 分析競爭對手
- 為潛在客戶評分與分群
- 零點數消耗

## API 文件

完整 API 文件：https://gmapsscraper.io/api/v1/docs

```bash
# 範例：擷取台北的咖啡廳
curl -X POST https://gmapsscraper.io/api/v1/scrape \
  -H "Authorization: Bearer gmaps_sk_your_key" \
  -H "Content-Type: application/json" \
  -d '{"keywords":["咖啡廳 台北"],"email":true}'
```

## 方案價格

- **免費**：註冊即送 10 點（可搜尋 5 次）
- **Starter**：$29/月
- **Pro**：$79/月
- **Advanced**：$149/年

立即開始：https://gmapsscraper.io

## 授權條款

MIT-0
