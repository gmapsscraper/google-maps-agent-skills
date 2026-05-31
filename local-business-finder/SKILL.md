---
name: local-business-finder
description: Find any local business by category and location on Google Maps. Get names, phone numbers, emails, websites, ratings, and hours. Search restaurants, dentists, plumbers, or any service.
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
    emoji: "📍"
    homepage: https://gmapsscraper.io
---

# Local Business Finder

Find any local business by category and location. Get complete profiles including contact info, ratings, reviews, and hours — all from Google Maps.

## When to Use

- User wants to find businesses near a location
- User asks "find me all [business type] in [city]"
- User needs a directory of local services
- User is researching a local market

## Important: Credit System

Each search costs 2 credits. Free accounts get 10 credits (5 searches).
Help users search smart — specific queries get better results.

## Workflow

### Step 1: Understand the Request

Parse what the user needs:
- **Business type**: restaurants, dentists, gyms, lawyers, etc.
- **Location**: city, neighborhood, zip code
- **Filters**: minimum rating, must have website, etc.

### Step 2: Optimize the Query

Help the user be specific to maximize results per credit:

| Too broad (wastes credits) | Optimized (better results) |
|---------------------------|---------------------------|
| "restaurant" | "thai restaurant in downtown Portland OR" |
| "doctor" | "family doctor accepting patients in Austin TX" |
| "store" | "pet store in Brooklyn NY" |

### Step 3: Confirm Before Searching

```
📍 Business Search:
   Looking for: {{business_type}}
   Location: {{location}}
   Expected: 20-80 results
   Cost: 2 credits
   
   Proceed?
```

### Step 4: Execute Search

```bash
curl -X POST "https://gmapsscraper.io/api/v1/jobs" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $GMAPS_SCRAPER_API_KEY" \
  -d '{
    "name": "Find: {{business_type}} in {{location}}",
    "keywords": ["{{business_type}} in {{location}}"],
    "lang": "en",
    "depth": 2,
    "email": true
  }'
```

### Step 5: Download & Present

```bash
curl -s "https://gmapsscraper.io/api/v1/jobs/{{job_id}}/download" \
  -H "Authorization: Bearer $GMAPS_SCRAPER_API_KEY" \
  --output businesses.csv
```

Present results in a clean, scannable format:

```
Found {{count}} businesses!

1. **{{name}}** ⭐ {{rating}} ({{reviews}} reviews)
   📞 {{phone}} | 🌐 {{website}} | ✉️ {{email}}
   📍 {{address}}

2. **{{name}}** ⭐ {{rating}} ({{reviews}} reviews)
   📞 {{phone}} | 🌐 {{website}}
   📍 {{address}}
...
```

### Step 6: Apply Filters (if requested)

- Rating >= X
- Has phone / email / website
- Within specific neighborhood
- Open on weekends

### Step 7: Offer Next Steps

- "Want cold emails for these businesses?" → `cold-email-local-business`
- "Want to analyze the competition?" → `competitor-analysis-local`
- "Export to spreadsheet?" → save as formatted CSV

## Common Search Categories

| Category | Best Keywords |
|----------|--------------|
| Food | "restaurant", "cafe", "pizza", "sushi bar" |
| Health | "dentist", "doctor", "pharmacy", "gym" |
| Home | "plumber", "electrician", "house cleaner" |
| Auto | "mechanic", "car wash", "tire shop" |
| Professional | "lawyer", "accountant", "insurance agent" |
| Beauty | "hair salon", "barber", "spa", "nail salon" |

## When Credits Run Out

```
⚡ Credits used up!

You've found {{total}} businesses with your free searches.
Upgrade for unlimited searches: https://gmapsscraper.io/#pricing

💡 Meanwhile, you can still analyze your existing data for free using
the competitor-analysis-local or cold-email-local-business skills!
```

## Get Started

1. Sign up at https://gmapsscraper.io (5 free searches)
2. Set: `export GMAPS_SCRAPER_API_KEY=your_key`
3. Start finding businesses!

Unlimited from $29/month.
