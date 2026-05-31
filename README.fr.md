[English](./README.md) | [Deutsch](./README.de.md) | [Español](./README.es.md) | [Français](./README.fr.md) | [日本語](./README.ja.md) | [한국어](./README.ko.md) | [Português](./README.pt.md) | [繁體中文](./README.zh-TW.md)

# Google Maps Agent Skills

> Une collection de skills Claude Code / OpenClaw pour la génération de leads via Google Maps.
> Chaque skill s'installe indépendamment et couvre un cas d'usage précis.

## Skills

| Skill | Description | Crédits |
|-------|-------------|---------|
| [`google-maps-scraper`](./google-maps-scraper/) | Extraire les données d'entreprises depuis Google Maps | 2/recherche |
| [`google-maps-leads`](./google-maps-leads/) | Générer des leads qualifiés avec scoring | 2/recherche |
| [`local-business-finder`](./local-business-finder/) | Trouver des entreprises par catégorie et localisation | 2/recherche |
| [`business-email-extractor`](./business-email-extractor/) | Extraire des emails professionnels vérifiés | 2/recherche |
| [`google-maps-export`](./google-maps-export/) | Exporter en CSV/JSON/HubSpot/Pipedrive | 2/recherche |
| [`cold-email-local-business`](./cold-email-local-business/) | Rédiger des emails de prospection depuis un CSV | Gratuit |
| [`competitor-analysis-local`](./competitor-analysis-local/) | Analyser la concurrence à partir de données CSV | Gratuit |
| [`google-maps-reviews-scraper`](./google-maps-reviews-scraper/) | Analyser les avis et la réputation | Gratuit |

## Installation

```bash
# Via ClawHub
npx clawhub@latest install gmapsscraper/google-maps-scraper

# Via GitHub (npx skills)
npx skills add gmapsscraper/google-maps-agent-skills/google-maps-scraper

# Manuellement
cp -r google-maps-scraper/ ~/.claude/skills/
```

## Démarrage rapide

```bash
# 1. Obtenez votre clé API gratuite sur https://gmapsscraper.io/dashboard
export GMAPS_SCRAPER_API_KEY=gmaps_sk_your_key_here

# 2. Installez un skill
npx clawhub@latest install gmapsscraper/google-maps-scraper

# 3. Demandez à votre agent :
# "Trouve-moi tous les dentistes à Paris avec leurs emails"
```

## Comment ça marche

```
Installer le skill → L'agent acquiert des capacités de génération de leads
                         ↓
        L'utilisateur demande "trouve des plombiers à Lyon"
                         ↓
        Le skill appelle l'API gmapsscraper.io (2 crédits)
                         ↓
        Renvoie les données (nom, téléphone, email, note...)
                         ↓
        L'utilisateur traite les données avec les skills gratuits (emails, analyse)
                         ↓
        Crédits épuisés → upgrade sur gmapsscraper.io
```

## Architecture à deux niveaux

**Skills payants** (clé API + crédits requis) : Extraient des données fraîches de Google Maps.
- Géocodage automatique : dites simplement « dentiste à Marseille » — pas de coordonnées nécessaires
- Confirmation avant chaque dépense de crédits
- Suggère les skills gratuits pour le post-traitement

**Skills gratuits** (pas de clé API) : Traitent des données CSV existantes en local.
- Rédiger des emails de prospection personnalisés
- Analyser les concurrents
- Noter et segmenter les leads
- Zéro crédit consommé

## Documentation API

Documentation complète : https://gmapsscraper.io/api/v1/docs

```bash
# Exemple : extraire les cafés à Paris
curl -X POST https://gmapsscraper.io/api/v1/scrape \
  -H "Authorization: Bearer gmaps_sk_your_key" \
  -H "Content-Type: application/json" \
  -d '{"keywords":["café à paris"],"email":true}'
```

## Tarifs

- **Gratuit** : 10 crédits (5 recherches) à l'inscription
- **Starter** : 29 $/mois
- **Pro** : 79 $/mois
- **Advanced** : 149 $/an

Commencer : https://gmapsscraper.io

## Licence

MIT-0
