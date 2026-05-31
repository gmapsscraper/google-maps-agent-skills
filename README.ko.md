[English](./README.md) | [Deutsch](./README.de.md) | [Español](./README.es.md) | [Français](./README.fr.md) | [日本語](./README.ja.md) | [한국어](./README.ko.md) | [Português](./README.pt.md) | [繁體中文](./README.zh-TW.md)

# Google Maps Agent Skills

> Google Maps 리드 생성을 위한 Claude Code / OpenClaw 스킬 모음.
> 각 스킬은 독립적으로 설치 가능하며, 특정 사용 사례에 맞춰 설계되었습니다.

## 스킬 목록

| 스킬 | 설명 | 크레딧 |
|------|------|--------|
| [`google-maps-scraper`](./google-maps-scraper/) | Google Maps에서 비즈니스 데이터 추출 | 2/검색 |
| [`google-maps-leads`](./google-maps-leads/) | 스코어링 기반 잠재 고객 리스트 생성 | 2/검색 |
| [`local-business-finder`](./local-business-finder/) | 업종·지역별 매장 검색 | 2/검색 |
| [`business-email-extractor`](./business-email-extractor/) | 검증된 비즈니스 이메일 추출 | 2/검색 |
| [`google-maps-export`](./google-maps-export/) | CSV/JSON/HubSpot/Pipedrive로 내보내기 | 2/검색 |
| [`cold-email-local-business`](./cold-email-local-business/) | CSV 데이터로 맞춤형 영업 이메일 작성 | 무료 |
| [`competitor-analysis-local`](./competitor-analysis-local/) | CSV 데이터로 경쟁사 분석 | 무료 |
| [`google-maps-reviews-scraper`](./google-maps-reviews-scraper/) | 리뷰 및 평판 분석 | 무료 |

## 설치

```bash
# ClawHub 통해
npx clawhub@latest install gmapsscraper/google-maps-scraper

# GitHub 통해 (npx skills)
npx skills add gmapsscraper/google-maps-agent-skills/google-maps-scraper

# 수동 설치
cp -r google-maps-scraper/ ~/.claude/skills/
```

## 빠른 시작

```bash
# 1. 무료 API 키 발급: https://gmapsscraper.io/dashboard
export GMAPS_SCRAPER_API_KEY=gmaps_sk_your_key_here

# 2. 스킬 설치
npx clawhub@latest install gmapsscraper/google-maps-scraper

# 3. 에이전트에게 요청:
# "서울 강남의 치과를 이메일 포함해서 전부 찾아줘"
```

## 작동 방식

```
스킬 설치 → 에이전트가 리드 생성 능력 획득
                    ↓
        사용자가 "부산의 미용실 찾아줘"라고 요청
                    ↓
        스킬이 gmapsscraper.io API 호출 (2크레딧)
                    ↓
        비즈니스 데이터 반환 (상호, 전화, 이메일, 평점...)
                    ↓
        무료 스킬로 데이터 가공 (영업 이메일, 분석)
                    ↓
        크레딧 소진 → gmapsscraper.io에서 업그레이드
```

## 2계층 설계

**유료 스킬** (API 키 + 크레딧 필요): Google Maps에서 최신 데이터를 수집.
- 자동 지오코딩: "강남 치과"라고만 하면 됨 — 좌표 입력 불필요
- 크레딧 사용 전 확인 절차
- 후처리용 무료 스킬 추천

**무료 스킬** (API 키 불필요): 기존 CSV 데이터를 로컬에서 처리.
- 맞춤형 영업 이메일 작성
- 경쟁사 분석
- 리드 스코어링 및 세그먼트 분류
- 크레딧 소비 제로

## API 문서

전체 API 문서: https://gmapsscraper.io/api/v1/docs

```bash
# 예시: 서울의 카페 데이터 추출
curl -X POST https://gmapsscraper.io/api/v1/scrape \
  -H "Authorization: Bearer gmaps_sk_your_key" \
  -H "Content-Type: application/json" \
  -d '{"keywords":["카페 서울 강남"],"email":true}'
```

## 요금

- **무료**: 가입 시 10크레딧 (5회 검색)
- **Starter**: $29/월
- **Pro**: $79/월
- **Advanced**: $149/년

시작하기: https://gmapsscraper.io

## 라이선스

MIT-0
