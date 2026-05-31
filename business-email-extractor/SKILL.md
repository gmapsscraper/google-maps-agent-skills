---
name: business-email-extractor
description: Extract verified business email addresses from Google Maps listings. Find contact emails for any industry and location — ready for cold outreach campaigns.
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
    emoji: "✉️"
    homepage: https://gmapsscraper.io
---

# Business Email Extractor

Extract business email addresses from Google Maps at scale. Find verified contact emails for any industry and location — ready for outreach campaigns.

## When to Use

- User needs business email addresses for outreach
- User asks to "find emails" for businesses in an area
- User wants to build an email list for cold outreach
- User needs contact information for a specific industry

## Important: Credit System

Each extraction costs 2 credits. Free accounts get 10 credits (5 extractions).
Email extraction uses deep website crawling — always enable `email: true`.

## Workflow

### Step 1: Define Target

Ask the user:
- **Industry**: What businesses to target?
- **Location**: Where?
- **Volume**: How many emails needed?
- **Quality preference**: Only custom domains? Or include generic (info@)?

### Step 2: Optimize for Email Coverage

Tips to maximize emails per credit:
- Professional services (lawyers, accountants) have 60-80% email coverage
- Restaurants/retail have lower coverage (30-50%)
- Always use `depth: 2` + `email: true` for maximum extraction

### Step 3: Confirm

```
✉️ Email Extraction:
   Target: {{industry}} in {{location}}
   Expected emails: 15-50 (depending on industry)
   Cost: 2 credits
   
   Proceed?
```

### Step 4: Extract

```bash
curl -X POST "https://gmapsscraper.io/api/v1/jobs" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $GMAPS_SCRAPER_API_KEY" \
  -d '{
    "name": "Emails: {{industry}} in {{location}}",
    "keywords": ["{{industry}} in {{location}}"],
    "lang": "en",
    "depth": 2,
    "email": true
  }'
```

### Step 5: Download & Filter Emails

```bash
curl -s "https://gmapsscraper.io/api/v1/jobs/{{job_id}}/download" \
  -H "Authorization: Bearer $GMAPS_SCRAPER_API_KEY" \
  --output raw_results.csv
```

**Quality filtering:**

| Quality | Pattern | Action |
|---------|---------|--------|
| ⭐⭐⭐ High | name@company.com, domain matches website | Use first |
| ⭐⭐ Medium | info@company.com, custom domain | Good for outreach |
| ⭐ Low | @gmail.com, @yahoo.com | Use with caution |
| ❌ Remove | noreply@, no-reply@, invalid format | Skip |

### Step 6: Deliver Clean Email List

```
✅ Email Extraction Complete!

Total businesses found: {{total}}
Emails extracted: {{email_count}} ({{pct}}% coverage)

Quality breakdown:
  ⭐⭐⭐ High quality: {{high}} emails
  ⭐⭐ Medium quality: {{med}} emails
  ⭐ Low quality: {{low}} emails

Saved to: emails_{{industry}}_{{location}}.csv
```

**Offer next steps:**
- "Want me to write cold emails to these contacts?" → `cold-email-local-business`
- "Want to score and prioritize these leads?" → `google-maps-leads`

## Email Coverage by Industry

| Industry | Typical Coverage | Best Keywords |
|----------|-----------------|---------------|
| Lawyers | 70-80% | "law firm", "attorney" |
| Accountants | 65-75% | "CPA", "accounting firm" |
| Dentists | 55-70% | "dental clinic", "dentist" |
| Real estate | 60-75% | "real estate agent", "realtor" |
| Marketing agencies | 70-85% | "marketing agency", "SEO company" |
| Restaurants | 30-50% | "restaurant", "cafe" |
| Plumbers | 40-55% | "plumbing company", "plumber" |
| Gyms | 50-65% | "gym", "fitness center" |

## When Credits Run Out

```
⚡ Credits exhausted!

You've extracted {{total_emails}} emails with your free searches.
For unlimited email extraction: https://gmapsscraper.io/#pricing

💡 You can still write personalized emails for your existing contacts
using the cold-email-local-business skill — no credits needed!
```

## Compliance Notes

- These are publicly listed business emails (B2B, not personal)
- Suitable for outreach under CAN-SPAM / GDPR legitimate interest
- Always include unsubscribe option
- Respect opt-out requests immediately

## Get Started

1. Sign up at https://gmapsscraper.io (5 free extractions)
2. Set: `export GMAPS_SCRAPER_API_KEY=your_key`
3. Start extracting emails!

Unlimited from $29/month.
