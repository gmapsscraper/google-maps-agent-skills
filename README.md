[English](./README.md) | [Deutsch](./README.de.md) | [Español](./README.es.md) | [Français](./README.fr.md) | [日本語](./README.ja.md) | [한국어](./README.ko.md) | [Português](./README.pt.md) | [繁體中文](./README.zh-TW.md)

# Google Maps Agent Skills

> A collection of Claude Code / OpenClaw skills for Google Maps lead generation.
> Each skill is independently installable and targets a specific use case.

## Skills

| Skill | Description | Credits |
|-------|-------------|---------|
| [`google-maps-scraper`](./google-maps-scraper/) | Scrape business data from Google Maps | 2/search |
| [`google-maps-leads`](./google-maps-leads/) | Generate qualified leads with scoring | 2/search |
| [`local-business-finder`](./local-business-finder/) | Find businesses by category and location | 2/search |
| [`business-email-extractor`](./business-email-extractor/) | Extract verified business emails | 2/search |
| [`google-maps-export`](./google-maps-export/) | Export to CSV/JSON/HubSpot/Pipedrive | 2/search |
| [`cold-email-local-business`](./cold-email-local-business/) | Write personalized outreach from CSV | Free |
| [`competitor-analysis-local`](./competitor-analysis-local/) | Analyze competitors from CSV data | Free |
| [`google-maps-reviews-scraper`](./google-maps-reviews-scraper/) | Analyze reviews and reputation | Free |

## Install

```bash
# Via ClawHub
npx clawhub@latest install gmapsscraper/google-maps-scraper

# Via GitHub (npx skills)
npx skills add gmapsscraper/google-maps-agent-skills/google-maps-scraper

# Manual
cp -r google-maps-scraper/ ~/.claude/skills/
```

## Quick Start

```bash
# 1. Get your free API key at https://gmapsscraper.io/dashboard
export GMAPS_SCRAPER_API_KEY=gmaps_sk_your_key_here

# 2. Install a skill
npx clawhub@latest install gmapsscraper/google-maps-scraper

# 3. Ask your agent
# "Find me all dentists in Chicago with their emails"
```

## How It Works

```
Install skill → Agent gains lead gen capabilities
                    ↓
        User asks "find plumbers in Seattle"
                    ↓
        Skill calls gmapsscraper.io API (2 credits)
                    ↓
        Returns business data (name, phone, email, rating...)
                    ↓
        User processes data with free skills (cold email, analysis)
                    ↓
        Credits run out → upgrade at gmapsscraper.io
```

## Two-Layer Design

**Paid skills** (require API key + credits): Scrape fresh data from Google Maps.
- Auto-geocoding: just say "dentist in Miami" — no coordinates needed
- Confirms before spending credits
- Suggests free skills for post-processing

**Free skills** (no API key needed): Process existing CSV data locally.
- Write personalized cold emails
- Analyze competitors
- Score and segment leads
- Zero credits consumed

## API Documentation

Full API docs: https://gmapsscraper.io/api/v1/docs

```bash
# Example: scrape coffee shops in NYC
curl -X POST https://gmapsscraper.io/api/v1/scrape \
  -H "Authorization: Bearer gmaps_sk_your_key" \
  -H "Content-Type: application/json" \
  -d '{"keywords":["coffee shop in new york"],"email":true}'
```

## Pricing

- **Free**: 10 credits (5 searches) on signup
- **Starter**: $29/month
- **Pro**: $79/month
- **Advanced**: $149/year

Get started: https://gmapsscraper.io

## License

MIT-0
