# 01. 현재 사이트 SEO 감사

**감사일**: 2026-11-01
**방법**: Playwright로 실제 브라우저 접근 후 DOM/메타태그 추출
**대상 URL**: https://www.xandy.co.kr/

## 사이트 기본 정보

| 항목 | 값 |
|------|-----|
| 플랫폼 | 아임웹 (imweb.me) |
| 메인 도메인 | www.xandy.co.kr |
| 모바일 서브도메인 | m.xandy.co.kr |
| 테마 컬러 | `#001778` (딥 네이비) |

## 메타태그 (현재 상태)

```html
<title>잔디학원 - 대치동 물리 전문 학원</title>

<meta name="description" content="물리대회 대비반, 고급물리, 의대, 치대, 영재고, 과학고 전문 잔디학원 더 자세한 내용을 확인해 보세요!">

<meta name="keywords" content="대치동, 대치동물리, 대치물리, 물리, 물리학원, 물리대회, 물리올림피아드, 물리대회 초급, 물리대회 중급, 물리대회 고급, 한국물리올림피아드, 의대진학, 물리인강, 과학고진학, 고급물리, 치대진학, 영재고진학, 영재고, 과학고, 치대, 의대, 명문대 진학, 물리대회 대비, 잔디학원, 대치동, 물리, 전문, 학원">

<meta property="og:title" content="잔디학원 - 대치동 물리 전문 학원">
<meta property="og:description" content="물리대회 대비반, 고급물리, 의대, 치대, 영재고, 과학고 전문 잔디학원 더 자세한 내용을 확인해 보세요!">
<meta property="og:image" content="https://cdn.imweb.me/upload/S2024122694316e8189cf9/ea8cc7dddd12e.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="627">
<meta property="og:type" content="website">
<meta property="og:url" content="http://xandy.co.kr/">
```

## 사이트 소유 인증 (⚠️ 반드시 신규 사이트에 그대로 이전)

```html
<meta name="naver-site-verification" content="9cc334bd653b97f094d6e73dc16deb9fdae7b014">
<meta name="google-site-verification" content="LKDGCc4Pxt6ccnA-BeEKSeJb0rrtVL7zbVYRxd_pC5M">
<meta name="msvalidate.01" content="FE139D7AA98D4734356BBD84280AC66E">
```

> 이 세 코드가 **신규 사이트 `<head>`에 그대로** 들어가야 Search Console/네이버 서치어드바이저/빙 웹마스터 연속성이 유지됩니다.

## 구조화 데이터 (현재)

현재 사이트는 아래 JSON-LD를 넣고 있습니다:

```json
{
  "@context": "https://schema.org",
  "@type": "OnlineStore",
  "name": "잔디학원 - 대치동 물리 전문 학원",
  "url": "http://xandy.co.kr",
  "address": {
    "@type": "PostalAddress",
    "addressCountry": "KR",
    "streetAddress": "서울 강남구 삼성로64길 47 (대치동)",
    "postalCode": "06190"
  }
}
```

### 🚨 문제점

- **타입이 `OnlineStore`** → 학원 사이트에 전혀 맞지 않음 (아임웹이 교재 쇼핑몰 기능 때문에 자동 생성)
- 배송비, 반품 정책 등 **학원과 무관한 필드** 포함
- 전화번호, 운영시간 **누락**
- 지점 정보 (`LocalBusiness` 하위 속성) 활용 안 됨

### ✅ 신규 사이트의 올바른 스키마 (제안)

```json
[
  {
    "@context": "https://schema.org",
    "@type": "EducationalOrganization",
    "name": "잔디학원",
    "alternateName": "XandY",
    "url": "https://www.xandy.co.kr",
    "logo": "https://www.xandy.co.kr/logo.png",
    "description": "대치동 물리 전문 학원. 물리대회 대비, 고급물리, 의대·치대·영재고·과학고 입시 전문.",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "삼성로64길 47, 4층",
      "addressLocality": "강남구",
      "addressRegion": "서울특별시",
      "postalCode": "06190",
      "addressCountry": "KR"
    },
    "telephone": "+82-2-6951-4080",
    "sameAs": [
      "https://www.instagram.com/goldxandy/",
      "https://m.blog.naver.com/PostList.naver?blogId=tobira99",
      "https://pf.kakao.com/_QDxmdn",
      "https://www.youtube.com/channel/UCeHQ6wtLhWM6b0gdAEyugfA"
    ]
  },
  {
    "@context": "https://schema.org",
    "@type": "LocalBusiness",
    "@id": "https://www.xandy.co.kr/#localbusiness",
    "name": "잔디학원",
    "image": "https://www.xandy.co.kr/og-image.png",
    "priceRange": "₩₩",
    "address": { /* 위와 동일 */ },
    "geo": {
      "@type": "GeoCoordinates",
      "latitude": "37.4998",
      "longitude": "127.0589"
    },
    "openingHoursSpecification": [
      {
        "@type": "OpeningHoursSpecification",
        "dayOfWeek": ["Saturday", "Sunday"],
        "opens": "09:00",
        "closes": "22:00"
      }
    ]
  }
]
```

> **좌표(geo)는 추후 실측 필요** — 임시로 삼성로64길 추정값 넣음

## 헤딩 구조 (현재)

| 태그 | 개수 | 내용 |
|------|------|------|
| `<h1>` | **0개** | ❌ 아예 없음 |
| `<h2>` | 1개 | "2026년 11월" (캘린더 위젯) |
| `<h3>` | 0개 | — |

### 🚨 문제점

- **H1 태그가 비어있다는 건 SEO 치명적** — 구글이 페이지 주제를 못 잡음
- 각 페이지마다 명확한 H1이 있어야 함 (예: 홈은 `<h1>대치동 물리 전문 학원 잔디</h1>`)

## Open Graph 이미지

- URL: https://cdn.imweb.me/upload/S2024122694316e8189cf9/ea8cc7dddd12e.png
- 크기: 1200×627 (적절)
- 신규 사이트에선 **자체 CDN/정적 경로**에서 서빙 권장

## 외부 플랫폼 연결

| 플랫폼 | URL |
|--------|-----|
| 인스타그램 | https://www.instagram.com/goldxandy/ |
| 네이버 블로그 | https://m.blog.naver.com/PostList.naver?blogId=tobira99 |
| 카카오톡 채널 | https://pf.kakao.com/_QDxmdn |
| 유튜브 | https://www.youtube.com/channel/UCeHQ6wtLhWM6b0gdAEyugfA |

→ 신규 사이트 푸터/상단에 유지 + `sameAs`에도 포함

## 사이트맵

- 위치: `/sitemap.xml`
- URL 개수: **22개**
- 상세 → [02-url-structure.md](02-url-structure.md)

## 요약 체크리스트 (신규 사이트 이전 시)

### 그대로 이전
- [x] title 패턴 `잔디학원 - 대치동 물리 전문 학원`
- [x] description 문구
- [x] keywords 메타태그 전체
- [x] 네이버/구글/빙 사이트 인증 코드 3종
- [x] OG 이미지 (가능하면 더 좋은 걸로 교체)
- [x] 외부 플랫폼 링크

### 개선/신규
- [ ] JSON-LD → `EducationalOrganization` + `LocalBusiness`
- [ ] 모든 페이지에 올바른 H1 삽입
- [ ] 구조화된 FAQ 스키마 추가 검토
- [ ] 코스 정보 `Course` 스키마 추가 검토
- [ ] sitemap.xml 재생성 (Next.js의 `app/sitemap.ts`)
- [ ] robots.txt (`app/robots.ts`)
