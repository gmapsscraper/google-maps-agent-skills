[English](./README.md) | [Deutsch](./README.de.md) | [Español](./README.es.md) | [Français](./README.fr.md) | [日本語](./README.ja.md) | [한국어](./README.ko.md) | [Português](./README.pt.md) | [繁體中文](./README.zh-TW.md)

# Google Maps Agent Skills

> Eine Sammlung von Claude Code / OpenClaw Skills zur Leadgenerierung über Google Maps.
> Jeder Skill ist einzeln installierbar und deckt einen bestimmten Anwendungsfall ab.

## Skills

| Skill | Beschreibung | Credits |
|-------|-------------|---------|
| [`google-maps-scraper`](./google-maps-scraper/) | Geschäftsdaten aus Google Maps extrahieren | 2/Suche |
| [`google-maps-leads`](./google-maps-leads/) | Qualifizierte Leads mit Bewertung generieren | 2/Suche |
| [`local-business-finder`](./local-business-finder/) | Unternehmen nach Branche und Standort finden | 2/Suche |
| [`business-email-extractor`](./business-email-extractor/) | Verifizierte Geschäfts-E-Mails extrahieren | 2/Suche |
| [`google-maps-export`](./google-maps-export/) | Export als CSV/JSON/HubSpot/Pipedrive | 2/Suche |
| [`cold-email-local-business`](./cold-email-local-business/) | Personalisierte Kaltakquise-Mails aus CSV erstellen | Kostenlos |
| [`competitor-analysis-local`](./competitor-analysis-local/) | Wettbewerbsanalyse aus CSV-Daten | Kostenlos |
| [`google-maps-reviews-scraper`](./google-maps-reviews-scraper/) | Bewertungen und Reputation analysieren | Kostenlos |

## Installation

```bash
# Über ClawHub
npx clawhub@latest install gmapsscraper/google-maps-scraper

# Über GitHub (npx skills)
npx skills add gmapsscraper/google-maps-agent-skills/google-maps-scraper

# Manuell
cp -r google-maps-scraper/ ~/.claude/skills/
```

## Schnellstart

```bash
# 1. Kostenlosen API-Key holen: https://gmapsscraper.io/dashboard
export GMAPS_SCRAPER_API_KEY=gmaps_sk_your_key_here

# 2. Skill installieren
npx clawhub@latest install gmapsscraper/google-maps-scraper

# 3. Deinem Agent sagen:
# "Finde alle Zahnärzte in München mit E-Mail-Adressen"
```

## So funktioniert's

```
Skill installieren → Agent bekommt Leadgenerierungs-Fähigkeiten
                         ↓
        Nutzer fragt "Finde Klempner in Hamburg"
                         ↓
        Skill ruft gmapsscraper.io API auf (2 Credits)
                         ↓
        Liefert Geschäftsdaten (Name, Telefon, E-Mail, Bewertung...)
                         ↓
        Nutzer verarbeitet Daten mit kostenlosen Skills (E-Mails, Analyse)
                         ↓
        Credits aufgebraucht → Upgrade auf gmapsscraper.io
```

## Zwei-Schichten-Konzept

**Kostenpflichtige Skills** (API-Key + Credits nötig): Aktuelle Daten aus Google Maps scrapen.
- Auto-Geocoding: einfach „Zahnarzt in Berlin" sagen — keine Koordinaten nötig
- Bestätigung vor jedem Credit-Verbrauch
- Empfiehlt kostenlose Skills zur Weiterverarbeitung

**Kostenlose Skills** (kein API-Key nötig): Vorhandene CSV-Daten lokal verarbeiten.
- Personalisierte Kaltakquise-Mails schreiben
- Wettbewerber analysieren
- Leads bewerten und segmentieren
- Null Credits verbraucht

## API-Dokumentation

Vollständige API-Docs: https://gmapsscraper.io/api/v1/docs

```bash
# Beispiel: Cafés in Berlin scrapen
curl -X POST https://gmapsscraper.io/api/v1/scrape \
  -H "Authorization: Bearer gmaps_sk_your_key" \
  -H "Content-Type: application/json" \
  -d '{"keywords":["café in berlin"],"email":true}'
```

## Preise

- **Kostenlos**: 10 Credits (5 Suchen) bei Registrierung
- **Starter**: $29/Monat
- **Pro**: $79/Monat
- **Advanced**: $149/Jahr

Jetzt starten: https://gmapsscraper.io

## Lizenz

MIT-0
