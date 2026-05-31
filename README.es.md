[English](./README.md) | [Deutsch](./README.de.md) | [Español](./README.es.md) | [Français](./README.fr.md) | [日本語](./README.ja.md) | [한국어](./README.ko.md) | [Português](./README.pt.md) | [繁體中文](./README.zh-TW.md)

# Google Maps Agent Skills

> Colección de skills de Claude Code / OpenClaw para generación de leads con Google Maps.
> Cada skill se instala por separado y cubre un caso de uso específico.

## Skills

| Skill | Descripción | Créditos |
|-------|-------------|----------|
| [`google-maps-scraper`](./google-maps-scraper/) | Extraer datos de negocios de Google Maps | 2/búsqueda |
| [`google-maps-leads`](./google-maps-leads/) | Generar leads cualificados con puntuación | 2/búsqueda |
| [`local-business-finder`](./local-business-finder/) | Buscar negocios por categoría y ubicación | 2/búsqueda |
| [`business-email-extractor`](./business-email-extractor/) | Extraer emails verificados de empresas | 2/búsqueda |
| [`google-maps-export`](./google-maps-export/) | Exportar a CSV/JSON/HubSpot/Pipedrive | 2/búsqueda |
| [`cold-email-local-business`](./cold-email-local-business/) | Escribir emails de prospección desde CSV | Gratis |
| [`competitor-analysis-local`](./competitor-analysis-local/) | Analizar competidores desde datos CSV | Gratis |
| [`google-maps-reviews-scraper`](./google-maps-reviews-scraper/) | Analizar reseñas y reputación | Gratis |

## Instalación

```bash
# Vía ClawHub
npx clawhub@latest install gmapsscraper/google-maps-scraper

# Vía GitHub (npx skills)
npx skills add gmapsscraper/google-maps-agent-skills/google-maps-scraper

# Manual
cp -r google-maps-scraper/ ~/.claude/skills/
```

## Inicio rápido

```bash
# 1. Obtén tu API key gratis en https://gmapsscraper.io/dashboard
export GMAPS_SCRAPER_API_KEY=gmaps_sk_your_key_here

# 2. Instala un skill
npx clawhub@latest install gmapsscraper/google-maps-scraper

# 3. Pídele a tu agente:
# "Encuentra todos los dentistas en Madrid con sus emails"
```

## Cómo funciona

```
Instalar skill → El agente obtiene capacidades de generación de leads
                         ↓
        Usuario pide "busca fontaneros en Barcelona"
                         ↓
        Skill llama a la API de gmapsscraper.io (2 créditos)
                         ↓
        Devuelve datos del negocio (nombre, teléfono, email, valoración...)
                         ↓
        Usuario procesa datos con skills gratuitos (emails, análisis)
                         ↓
        Créditos agotados → upgrade en gmapsscraper.io
```

## Diseño en dos capas

**Skills de pago** (requieren API key + créditos): Extraen datos frescos de Google Maps.
- Geocodificación automática: solo di "dentista en Sevilla" — sin coordenadas
- Confirma antes de gastar créditos
- Sugiere skills gratuitos para el post-procesamiento

**Skills gratuitos** (sin API key): Procesan datos CSV existentes en local.
- Escribir emails de prospección personalizados
- Analizar competidores
- Puntuar y segmentar leads
- Cero créditos consumidos

## Documentación de la API

Docs completos: https://gmapsscraper.io/api/v1/docs

```bash
# Ejemplo: extraer cafeterías en Madrid
curl -X POST https://gmapsscraper.io/api/v1/scrape \
  -H "Authorization: Bearer gmaps_sk_your_key" \
  -H "Content-Type: application/json" \
  -d '{"keywords":["cafetería en madrid"],"email":true}'
```

## Precios

- **Gratis**: 10 créditos (5 búsquedas) al registrarte
- **Starter**: $29/mes
- **Pro**: $79/mes
- **Advanced**: $149/año

Empieza ahora: https://gmapsscraper.io

## Licencia

MIT-0
