[English](./README.md) | [Deutsch](./README.de.md) | [Español](./README.es.md) | [Français](./README.fr.md) | [日本語](./README.ja.md) | [한국어](./README.ko.md) | [Português](./README.pt.md) | [繁體中文](./README.zh-TW.md)

# Google Maps Agent Skills

> Google Maps を活用したリード獲得のための Claude Code / OpenClaw スキル集。
> 各スキルは個別にインストール可能で、特定のユースケースに対応しています。

## スキル一覧

| スキル | 説明 | クレジット |
|--------|------|-----------|
| [`google-maps-scraper`](./google-maps-scraper/) | Google Maps からビジネスデータを抽出 | 2/検索 |
| [`google-maps-leads`](./google-maps-leads/) | スコアリング付きの見込み客リストを生成 | 2/検索 |
| [`local-business-finder`](./local-business-finder/) | 業種・エリアで店舗を検索 | 2/検索 |
| [`business-email-extractor`](./business-email-extractor/) | 認証済みビジネスメールを抽出 | 2/検索 |
| [`google-maps-export`](./google-maps-export/) | CSV/JSON/HubSpot/Pipedrive へエクスポート | 2/検索 |
| [`cold-email-local-business`](./cold-email-local-business/) | CSV データからパーソナライズした営業メールを作成 | 無料 |
| [`competitor-analysis-local`](./competitor-analysis-local/) | CSV データから競合を分析 | 無料 |
| [`google-maps-reviews-scraper`](./google-maps-reviews-scraper/) | 口コミ・評判を分析 | 無料 |

## インストール

```bash
# ClawHub 経由
npx clawhub@latest install gmapsscraper/google-maps-scraper

# GitHub 経由 (npx skills)
npx skills add gmapsscraper/google-maps-agent-skills/google-maps-scraper

# 手動
cp -r google-maps-scraper/ ~/.claude/skills/
```

## クイックスタート

```bash
# 1. 無料の API キーを取得: https://gmapsscraper.io/dashboard
export GMAPS_SCRAPER_API_KEY=gmaps_sk_your_key_here

# 2. スキルをインストール
npx clawhub@latest install gmapsscraper/google-maps-scraper

# 3. エージェントに聞く:
# 「東京の歯医者をメールアドレス付きで全部探して」
```

## 仕組み

```
スキルをインストール → エージェントがリード獲得能力を獲得
                         ↓
        ユーザーが「大阪の美容院を探して」と依頼
                         ↓
        スキルが gmapsscraper.io API を呼び出し（2クレジット）
                         ↓
        ビジネスデータを返却（店名、電話、メール、評価...）
                         ↓
        無料スキルでデータを加工（営業メール作成、分析）
                         ↓
        クレジット切れ → gmapsscraper.io でアップグレード
```

## 2層設計

**有料スキル**（APIキー＋クレジットが必要）：Google Maps から最新データを取得。
- 自動ジオコーディング：「渋谷の歯医者」と言うだけ — 座標指定不要
- クレジット消費前に確認
- 後処理には無料スキルを提案

**無料スキル**（APIキー不要）：既存の CSV データをローカルで処理。
- パーソナライズした営業メールを作成
- 競合を分析
- リードをスコアリング・セグメント分け
- クレジット消費ゼロ

## APIドキュメント

完全なAPIドキュメント: https://gmapsscraper.io/api/v1/docs

```bash
# 例: 東京のカフェを抽出
curl -X POST https://gmapsscraper.io/api/v1/scrape \
  -H "Authorization: Bearer gmaps_sk_your_key" \
  -H "Content-Type: application/json" \
  -d '{"keywords":["カフェ 東京"],"email":true}'
```

## 料金

- **無料**: 登録時に10クレジット（5回検索）
- **Starter**: $29/月
- **Pro**: $79/月
- **Advanced**: $149/年

今すぐ始める: https://gmapsscraper.io

## ライセンス

MIT-0
