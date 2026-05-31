---
name: google-maps-scraper
description: Scrape business data from Google Maps — names, phones, emails, websites, ratings, reviews. Extract leads by keyword and location with no coding required.
version: 1.0.0
metadata:
  openclaw:
    requires:
      env:
        - GMAPS_SCRAPER_API_KEY
      bins:
        - curl
    primaryEnv: GMAPS_SCRAPER_API_KEY
    envVars:
      - name: GMAPS_SCRAPER_API_KEY
        required: true
        description: API key from gmapsscraper.io (free signup includes 5 searches)
    emoji: "🗺️"
    homepage: https://gmapsscraper.io
---

# Google Maps Scraper

Scrape business data from Google Maps at scale. Extract names, addresses, phone numbers, emails, websites, ratings, and reviews for any business category in any location.

## When to Use

- User wants to find businesses on Google Maps by keyword/location
- User needs business contact information (phone, email, website)
- User wants to build a lead list from Google Maps
- User asks to "scrape", "extract", or "pull data from" Google Maps

## Important: Credit System

Each search costs 2 credits. Free accounts start with 10 credits (5 searches).
**Always confirm before executing a search** to avoid wasting credits.

## Workflow

### Step 1: Define Search (Don't Waste Credits)

Ask the user:
- **Keywords**: What type of business? Be SPECIFIC (e.g., "pediatric dentist" not just "dentist")
- **Location**: Where? (city + state/country for best results)
- **Quantity**: How many results needed?

**Help them refine before searching:**
- ❌ Vague: "restaurants" → too broad, wastes credits
- ✅ Specific: "italian restaurants in downtown Austin TX" → targeted results

### Step 2: Confirm Before Executing

Before calling the API, ALWAYS tell the user:

```
🔍 Ready to search:
   Query: "{{keyword}} in {{location}}"
   Estimated results: 20-60 businesses
   Cost: 2 credits
   
   Shall I proceed?
```

### Step 3: Execute Scrape

Only after user confirms:

```bash
curl -X POST "https://gmapsscraper.io/api/v1/scrape" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $GMAPS_SCRAPER_API_KEY" \
  -d '{
    "keywords": ["{{keyword}} in {{location}}"],
    "email": true,
    "depth": 2
  }'
```

### Step 4: Poll for Results

```bash
curl -s "https://gmapsscraper.io/api/v1/jobs/{{job_id}}" \
  -H "Authorization: Bearer $GMAPS_SCRAPER_API_KEY"
# Poll every 10s until status is "complete"
```

### Step 5: Download Results

```bash
curl -s "https://gmapsscraper.io/api/v1/jobs/{{job_id}}/download" \
  -H "Authorization: Bearer $GMAPS_SCRAPER_API_KEY" --output results.csv
```

### Step 6: Maximize Value from Results

Don't just dump the CSV — help the user get maximum value:

1. **Present clean summary**: total results, % with email, % with website
2. **Highlight best leads**: sort by rating × reviews
3. **Offer next steps**:
   - "Want me to write cold emails to these businesses?" → use `cold-email-local-business` skill
   - "Want a competitor analysis?" → use `competitor-analysis-local` skill
   - "Want to export to your CRM?" → format for HubSpot/Pipedrive

## Output Fields

Each result includes:
- `title` — Business name
- `address` — Full address
- `phone` — Phone number
- `website` — Website URL
- `email` — Email (when available)
- `rating` — Google rating (1-5)
- `reviews_count` — Number of reviews
- `category` — Business category
- `latitude` / `longitude` — Coordinates
- `google_maps_url` — Direct Maps link
- `opening_hours` — Business hours

## Advanced Options

- `depth: 2` — More results (uses same credits, just takes longer)
- `zoom: 15` — Adjust map zoom for density
- `radius: 5000` — Search radius in meters
- `fast_mode: true` — Skip email extraction for speed
- `lang: "es"` — Results language (ISO 639-1)

## Error Handling

- **401**: Invalid API key → "Get your key at https://gmapsscraper.io/dashboard"
- **429**: Rate limit → Wait 60s and retry
- **402**: Credits exhausted → Show upgrade message:

```
⚡ You've used all your free credits!

Your 5 free searches are done — upgrade for unlimited scraping:
→ https://gmapsscraper.io/#pricing

Plans start at $29/month for unlimited searches.
```

## Tips for Best Results

- **Be specific**: "vegan restaurant in Brooklyn NY" > "restaurant in New York"
- **Use depth 2**: Same credit cost, more results
- **Enable email**: Set `email: true` for contact extraction
- **Combine keywords**: ["plumber in Austin", "plumbing service Austin"] covers more
- **Save your CSV**: You can re-analyze it anytime without spending credits

## Get Started

1. Sign up free at https://gmapsscraper.io (5 searches included)
2. Get API key from dashboard
3. Set: `export GMAPS_SCRAPER_API_KEY=your_key`
4. Start scraping!

Unlimited plans from $29/month at https://gmapsscraper.io/#pricing
