# Construction Plan — KCD Seoul 홈페이지

> **상태**: In Progress
> **작성일**: 2026-03-05
> **승인일**: 2026-03-05

---

## 프로젝트 구조 (Application Design)

```
kcd-seoul/                          ← Next.js 프로젝트 루트
├── app/
│   ├── layout.tsx                  # 루트 레이아웃 (메타데이터, 폰트)
│   ├── page.tsx                    # 메인 페이지 (섹션 조합)
│   └── globals.css                 # 전역 스타일
├── components/
│   ├── layout/
│   │   ├── Navbar.tsx              # 내비게이션 바 (스크롤 스파이)
│   │   └── Footer.tsx              # 푸터
│   └── sections/
│       ├── Hero.tsx                # 히어로 섹션
│       ├── About.tsx               # 행사 소개
│       ├── Speakers.tsx            # 발표자 목록
│       ├── Schedule.tsx            # 세션 일정표
│       ├── Sponsors.tsx            # 스폰서
│       └── Registration.tsx        # 참가 등록 폼
├── data/
│   ├── speakers.ts                 # 발표자 데이터 (플레이스홀더)
│   ├── schedule.ts                 # 일정 데이터 (플레이스홀더)
│   └── sponsors.ts                 # 스폰서 데이터 (플레이스홀더)
├── types/
│   └── index.ts                    # 공통 타입 정의
├── public/
│   └── images/                     # 이미지 에셋
├── next.config.ts
├── tailwind.config.ts
└── package.json
```

---

## Work Units

| WU ID | 제목 | 우선순위 | 의존성 |
|-------|------|---------|--------|
| WU-001 | 프로젝트 초기 설정 | High | - |
| WU-002 | 레이아웃 + 내비게이션 | High | WU-001 |
| WU-003 | 히어로 + 행사 소개 섹션 | High | WU-002 |
| WU-004 | 발표자 목록 섹션 | High | WU-002 |
| WU-005 | 세션 일정표 섹션 | High | WU-002 |
| WU-006 | 스폰서 섹션 | Medium | WU-002 |
| WU-007 | 참가 등록 폼 섹션 | High | WU-002 |
| WU-008 | 푸터 + 마무리 | Medium | WU-003~007 |

---

## WU-001: 프로젝트 초기 설정 ✅

- [x] `create-next-app` 실행 (TypeScript + Tailwind CSS + App Router)
- [x] 타입 정의 파일 생성 (`types/index.ts`)
- [x] 플레이스홀더 데이터 파일 생성 (`data/`)
- [x] 전역 스타일 및 컬러 팔레트 설정 (Kubernetes 브랜드 컬러: `#326CE5`)
- [x] `next.config.ts` 정적 export 설정

## WU-002: 레이아웃 + 내비게이션 ✅

- [x] `app/layout.tsx` — 메타데이터 (OG tags, SEO)
- [x] `Navbar.tsx` — 고정 상단 바, 섹션 링크, 모바일 햄버거 메뉴

## WU-003: 히어로 + 행사 소개 섹션 ✅

- [x] `Hero.tsx` — 행사명, 날짜, 장소, 등록 CTA 버튼, 배경 그라디언트
- [x] `About.tsx` — 행사 목적, 참가 대상, 주요 주제 3가지 카드

## WU-004: 발표자 목록 섹션 ✅

- [x] `Speakers.tsx` — 발표자 카드 그리드 (사진, 이름, 소속, 주제)
- [x] `data/speakers.ts` — 더미 발표자 6명 데이터

## WU-005: 세션 일정표 섹션 ✅

- [x] `Schedule.tsx` — 타임라인 레이아웃, 시간/트랙/발표자/주제 표시
- [x] `data/schedule.ts` — 더미 세션 10개 데이터

## WU-006: 스폰서 섹션 ✅

- [x] `Sponsors.tsx` — Gold/Silver/Bronze 등급별 로고 그리드
- [x] `data/sponsors.ts` — 더미 스폰서 9개 데이터

## WU-007: 참가 등록 폼 섹션 ✅

- [x] `Registration.tsx` — 순수 React 상태 기반 폼 컴포넌트
- [x] 유효성 검사 (이름 필수, 이메일 형식, 소속 필수, 직책 필수)
- [x] 제출 성공 상태 처리 (성공 화면 전환)

## WU-008: 푸터 + 마무리 ✅

- [x] `Footer.tsx` — SNS 링크, 문의 이메일, 저작권
- [x] 최종 통합 (`app/page.tsx`에서 모든 섹션 조합)
- [x] 빌드 통과 (`next build` 성공, Static export)

---

## 보안 게이트웨이 체크리스트

- [x] XSS: React의 기본 이스케이핑으로 방어 (innerHTML 미사용)
- [x] 외부 링크: `rel="noopener noreferrer"` 전체 적용
- [x] 민감 정보: 하드코딩 없음 (이메일 주소는 플레이스홀더)
- [ ] 의존성: npm audit 통과 (1 high severity — 확인 필요)
