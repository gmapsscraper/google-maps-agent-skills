# GMaps Scraper Skills Collection

> 🦞 A collection of Claude Code / OpenClaw skills for Google Maps lead generation.
> Each skill is independently installable and targets a specific use case.

## Skills List

| Skill Name | Keyword Target | Description |
|-----------|---------------|-------------|
| `google-maps-scraper` | google maps scraper | Scrape business data from Google Maps |
| `google-maps-leads` | google maps leads | Generate qualified leads from Google Maps |
| `local-business-finder` | local business finder | Find businesses by category and location |
| `business-email-extractor` | business email finder | Extract verified business emails |
| `google-maps-export` | google maps export csv | Export Maps data to CSV/JSON/CRM |
| `cold-email-local-business` | cold email local business | Write personalized outreach to local businesses |
| `competitor-analysis-local` | local competitor analysis | Analyze competitors from Google Maps data |
| `google-maps-reviews-scraper` | google maps reviews | Scrape and analyze business reviews |

## Install

```bash
# Via ClawHub
npx clawhub@latest install gmapsscraper/google-maps-scraper

# Via npx skills (GitHub)
npx skills add gmapsscraper/gmapsscraper-skills/google-maps-scraper

# Manual
cp -r google-maps-scraper/ ~/.claude/skills/
```

## How It Works

1. User installs a skill → Agent gains Google Maps lead gen capabilities
2. Skill provides workflow guidance + data processing logic
3. When user needs actual data → skill calls gmapsscraper.io API (free tier: 100 leads)
4. User gets value → upgrades for more credits

## API

All skills use the gmapsscraper.io API. Set your API key:

```bash
export GMAPS_SCRAPER_API_KEY=your_key_here
```

Get a free API key at: https://gmapsscraper.io/dashboard

## Publishing

```bash
# Publish all skills to ClawHub
for dir in */; do
  if [ -f "$dir/SKILL.md" ]; then
    cd "$dir" && npx clawhub@latest publish && cd ..
  fi
done
```

## License

MIT-0
