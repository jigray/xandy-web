# 02. URL 구조

## 현재 사이트맵 (총 22개 URL)

`https://www.xandy.co.kr/sitemap.xml` 기준.

| # | URL | 추정 역할 |
|---|-----|-----------|
| 1 | `/Home` | 홈 (사이트맵엔 `/Home`이지만 실제 접속은 `/`로 리다이렉트) |
| 2 | `/35` | 학원 소개 (상위 허브) |
| 3 | `/about` | 인사말 |
| 4 | `/facilities-overview` | 시설 안내 |
| 5 | `/contact` | 오시는 길 |
| 6 | `/teachers` | 강사진 소개 |
| 7 | `/class-structure` | 수업 구성 |
| 8 | `/schedule` | 스케줄 |
| 9 | `/all-schedule` | 시간표 (전체) |
| 10 | `/the-physics-league-schedule` | 물리대회 스케줄 |
| 11 | `/xandy-academy` | (상세 미파악) |
| 12 | `/Level-A` | 레벨 A 수업 |
| 13 | `/Level-B` | 레벨 B 수업 |
| 14 | `/Level-C` | 레벨 C 수업 |
| 15 | `/Level-D` | 레벨 D 수업 |
| 16 | `/Level-E` | 레벨 E 수업 |
| 17 | `/Notice` | 공지사항 |
| 18 | `/37` | 게시판 (상세 미파악) |
| 19 | `/38` | 게시판 (상세 미파악) |
| 20 | `/39` | 게시판 (상세 미파악) |
| 21 | `/shop_view/1` | 교재 상세 1 |
| 22 | `/shop_view/2` | 교재 상세 2 |

> 참고: `/35`, `/37`, `/38`, `/39` 같은 숫자 URL은 아임웹의 **페이지 ID 기반 자동 URL**로 보임. 재구축 시 **의미 있는 slug로 바꾸거나 리다이렉트로 매핑** 필요.

## 신규 URL 매핑 전략

### 원칙

1. **slug가 의미 있는 URL은 그대로 유지** (예: `/about`, `/teachers`, `/Level-A`)
2. **숫자 URL은 의미 있는 slug로 교체 + 301 리다이렉트**
3. **대소문자는 현재 그대로 유지** (SEO 영향 최소화)

### 매핑 테이블

| 현재 URL | 신규 URL | 조치 |
|---------|---------|------|
| `/` | `/` | 유지 |
| `/Home` | `/` | 301 리다이렉트 → `/` |
| `/35` | `/about-academy` 또는 유지 | **결정 필요** |
| `/about` | `/about` | 유지 |
| `/facilities-overview` | `/facilities-overview` | 유지 |
| `/contact` | `/contact` | 유지 |
| `/teachers` | `/teachers` | 유지 |
| `/class-structure` | `/class-structure` | 유지 |
| `/schedule` | `/schedule` | 유지 |
| `/all-schedule` | `/all-schedule` | 유지 (또는 `/schedule`로 통합?) |
| `/the-physics-league-schedule` | `/the-physics-league-schedule` | 유지 |
| `/xandy-academy` | `/xandy-academy` | 유지 (내용 확인 필요) |
| `/Level-A` ~ `/Level-E` | 동일 유지 | 유지 |
| `/Notice` | `/Notice` 또는 `/notice` | 대소문자 유지 추천 |
| `/37`, `/38`, `/39` | 의미 있는 slug | **301 리다이렉트** |
| `/shop_view/1`, `/shop_view/2` | 교재 유지 여부 결정 | **범위 결정 필요** |

### Next.js에서 리다이렉트 설정 예시

```typescript
// next.config.ts
import type { NextConfig } from 'next';

const config: NextConfig = {
  async redirects() {
    return [
      { source: '/Home', destination: '/', permanent: true },
      // /37, /38, /39는 콘텐츠 파악 후 매핑
    ];
  },
};

export default config;
```

## 신규 Next.js 라우트 구조 (초안)

```
app/
├── layout.tsx                           # 공통 레이아웃 (meta, header, footer)
├── page.tsx                             # / (홈)
├── about/
│   └── page.tsx                         # /about (인사말)
├── facilities-overview/
│   └── page.tsx                         # /facilities-overview
├── contact/
│   └── page.tsx                         # /contact
├── teachers/
│   └── page.tsx                         # /teachers
├── class-structure/
│   └── page.tsx                         # /class-structure
├── schedule/
│   └── page.tsx                         # /schedule
├── all-schedule/
│   └── page.tsx                         # /all-schedule
├── the-physics-league-schedule/
│   └── page.tsx                         # /the-physics-league-schedule
├── xandy-academy/
│   └── page.tsx                         # /xandy-academy
├── Level-[level]/
│   └── page.tsx                         # /Level-A ~ /Level-E (dynamic)
├── Notice/
│   ├── page.tsx                         # /Notice (목록)
│   └── [slug]/
│       └── page.tsx                     # /Notice/[slug] (상세)
├── sitemap.ts                           # /sitemap.xml 자동 생성
└── robots.ts                            # /robots.txt
```

### 주의

- Next.js는 **파일명 대소문자가 라우트에 그대로 반영**됨 → `/Level-A`, `/Notice` 처럼 **대문자가 섞인 경로**는 폴더명도 대문자 유지.
- 또는 **소문자로 통일하고 리다이렉트** 처리하는 방법도 있음. 어느 쪽이 SEO 영향 적을지 **별도 결정 필요**.

## 숙제: 콘텐츠 파악 필요한 페이지

Playwright로 추가 크롤링해서 아래 페이지들의 **실제 콘텐츠**를 파악해야 함:

- [ ] `/35` — 학원 소개 허브 페이지의 실제 콘텐츠
- [ ] `/xandy-academy` — 뭘 설명하는 페이지인지
- [ ] `/37`, `/38`, `/39` — 게시판인지, 특수 페이지인지
- [ ] `/shop_view/1`, `/shop_view/2` — 어떤 교재인지
- [ ] 각 Level-A ~ E 페이지의 내용 차이
- [ ] `/schedule` vs `/all-schedule` 차이
