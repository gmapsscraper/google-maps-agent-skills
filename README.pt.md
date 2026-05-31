[English](./README.md) | [Deutsch](./README.de.md) | [Español](./README.es.md) | [Français](./README.fr.md) | [日本語](./README.ja.md) | [한국어](./README.ko.md) | [Português](./README.pt.md) | [繁體中文](./README.zh-TW.md)

# Google Maps Agent Skills

> Coleção de skills Claude Code / OpenClaw para geração de leads via Google Maps.
> Cada skill é instalável de forma independente e atende um caso de uso específico.

## Skills

| Skill | Descrição | Créditos |
|-------|-----------|----------|
| [`google-maps-scraper`](./google-maps-scraper/) | Extrair dados de empresas do Google Maps | 2/busca |
| [`google-maps-leads`](./google-maps-leads/) | Gerar leads qualificados com pontuação | 2/busca |
| [`local-business-finder`](./local-business-finder/) | Encontrar empresas por categoria e localização | 2/busca |
| [`business-email-extractor`](./business-email-extractor/) | Extrair emails comerciais verificados | 2/busca |
| [`google-maps-export`](./google-maps-export/) | Exportar para CSV/JSON/HubSpot/Pipedrive | 2/busca |
| [`cold-email-local-business`](./cold-email-local-business/) | Escrever emails de prospecção a partir de CSV | Grátis |
| [`competitor-analysis-local`](./competitor-analysis-local/) | Analisar concorrentes a partir de dados CSV | Grátis |
| [`google-maps-reviews-scraper`](./google-maps-reviews-scraper/) | Analisar avaliações e reputação | Grátis |

## Instalação

```bash
# Via ClawHub
npx clawhub@latest install gmapsscraper/google-maps-scraper

# Via GitHub (npx skills)
npx skills add gmapsscraper/google-maps-agent-skills/google-maps-scraper

# Manual
cp -r google-maps-scraper/ ~/.claude/skills/
```

## Início rápido

```bash
# 1. Obtenha sua chave API gratuita em https://gmapsscraper.io/dashboard
export GMAPS_SCRAPER_API_KEY=gmaps_sk_your_key_here

# 2. Instale um skill
npx clawhub@latest install gmapsscraper/google-maps-scraper

# 3. Peça ao seu agente:
# "Encontre todos os dentistas em São Paulo com emails"
```

## Como funciona

```
Instalar skill → Agente ganha capacidades de geração de leads
                         ↓
        Usuário pede "encontre encanadores em Curitiba"
                         ↓
        Skill chama a API gmapsscraper.io (2 créditos)
                         ↓
        Retorna dados comerciais (nome, telefone, email, nota...)
                         ↓
        Usuário processa dados com skills gratuitos (emails, análise)
                         ↓
        Créditos esgotados → upgrade em gmapsscraper.io
```

## Design em duas camadas

**Skills pagos** (chave API + créditos necessários): Extraem dados atualizados do Google Maps.
- Geocodificação automática: basta dizer "dentista em Belo Horizonte" — sem coordenadas
- Confirmação antes de gastar créditos
- Sugere skills gratuitos para pós-processamento

**Skills gratuitos** (sem chave API): Processam dados CSV existentes localmente.
- Escrever emails de prospecção personalizados
- Analisar concorrentes
- Pontuar e segmentar leads
- Zero créditos consumidos

## Documentação da API

Documentação completa: https://gmapsscraper.io/api/v1/docs

```bash
# Exemplo: extrair cafeterias em São Paulo
curl -X POST https://gmapsscraper.io/api/v1/scrape \
  -H "Authorization: Bearer gmaps_sk_your_key" \
  -H "Content-Type: application/json" \
  -d '{"keywords":["cafeteria em são paulo"],"email":true}'
```

## Preços

- **Grátis**: 10 créditos (5 buscas) ao se cadastrar
- **Starter**: $29/mês
- **Pro**: $79/mês
- **Advanced**: $149/ano

Comece agora: https://gmapsscraper.io

## Licença

MIT-0
