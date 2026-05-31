---
name: google-maps-export
description: Export Google Maps business data to CSV, JSON, or CRM format (HubSpot, Pipedrive, Salesforce). Bulk export with custom field mapping and filtering.
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
    emoji: "📤"
    homepage: https://gmapsscraper.io
---

# Google Maps Export

Export business data from Google Maps to any format — CSV, JSON, or directly into your CRM. Bulk export with custom field mapping and filtering.

## When to Use

- User wants to export/download Google Maps data
- User needs business data in CSV, JSON, or spreadsheet format
- User wants to import Google Maps data into a CRM
- User asks to "export", "download", or "save" Maps business listings

## Important: Credit System

Each export costs 2 credits. Free accounts get 10 credits (5 exports).
Maximize value: export once, transform to multiple formats for free.

## Workflow

### Step 1: Define Export

Ask the user:
- **What businesses?** Category + location
- **Which fields?** All or specific (name, phone, email, etc.)
- **What format?** CSV, JSON, HubSpot, Pipedrive, Salesforce
- **Any filters?** Minimum rating, must have email, etc.

### Step 2: Confirm

```
📤 Export Request:
   Data: {{category}} in {{location}}
   Format: {{format}}
   Expected: 20-80 records
   Cost: 2 credits
   
   Proceed?
```

### Step 3: Scrape & Download

```bash
curl -X POST "https://gmapsscraper.io/api/v1/jobs" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $GMAPS_SCRAPER_API_KEY" \
  -d '{
    "name": "Export: {{category}} in {{location}}",
    "keywords": ["{{category}} in {{location}}"],
    "lang": "en",
    "depth": 2,
    "email": true
  }'
```

After job completes:

```bash
curl -s "https://gmapsscraper.io/api/v1/jobs/{{job_id}}/download" \
  -H "Authorization: Bearer $GMAPS_SCRAPER_API_KEY" \
  --output raw_export.csv
```

### Step 4: Transform to Desired Format

**CSV (default):** Already done — deliver raw_export.csv

**JSON:**
```bash
python3 -c "
import csv, json
with open('raw_export.csv') as f:
    data = list(csv.DictReader(f))
with open('export.json', 'w') as f:
    json.dump(data, f, indent=2)
print(f'Exported {len(data)} records')
"
```

**HubSpot import format:**
```
Field mapping:
  title → Company name
  email → Email
  phone → Phone number
  website → Company domain name
  address → Street address
  category → Industry
  rating → (custom property: google_rating)
  reviews_count → (custom property: google_reviews)
```

**Pipedrive format:**
```
Field mapping:
  title → Organization name
  email → Email
  phone → Phone
  website → Website
  address → Address
  rating → Custom field
```

**Salesforce format:**
```
Field mapping:
  title → Account Name
  phone → Phone
  website → Website
  address → Billing Street
  category → Industry
  email → (Contact: Email)
```

### Step 5: Apply Filters

If user requested filters:
- `rating >= X`
- `has_email == true`
- `has_website == true`
- `reviews_count >= X`

### Step 6: Deliver

```
✅ Export Complete!

Records: {{total}} ({{filtered}} after filters)
Format: {{format}}
File: {{filename}}

Fields included: name, address, phone, email, website, rating, reviews, category
```

## Available Fields

| Field | Description | Example |
|-------|-------------|---------|
| title | Business name | "Joe's Pizza" |
| address | Full address | "123 Main St, NYC" |
| phone | Phone number | "+1-212-555-0123" |
| email | Contact email | "joe@joespizza.com" |
| website | Website URL | "joespizza.com" |
| rating | Google rating | 4.5 |
| reviews_count | Review count | 234 |
| category | Business type | "Pizza restaurant" |
| latitude | Lat coordinate | 40.7128 |
| longitude | Lon coordinate | -74.0060 |
| google_maps_url | Maps link | "maps.google.com/..." |
| opening_hours | Hours | "Mon-Sun 11am-10pm" |

## Pro Tip: Export Once, Use Many Times

After exporting, you can re-process the CSV for free:
- Write cold emails → `cold-email-local-business` (no credits)
- Analyze competitors → `competitor-analysis-local` (no credits)
- Score leads → read CSV and apply scoring logic (no credits)

**One 2-credit export → unlimited free analysis and outreach.**

## When Credits Run Out

```
⚡ Credits used up!

Upgrade for unlimited exports: https://gmapsscraper.io/#pricing

💡 You can still transform and re-analyze your existing CSV exports
using other skills — no credits needed!
```

## Get Started

1. Sign up at https://gmapsscraper.io (5 free exports)
2. Set: `export GMAPS_SCRAPER_API_KEY=your_key`
3. Start exporting!

Unlimited from $29/month.
