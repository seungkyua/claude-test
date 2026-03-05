# Operations Runbook — KCD Seoul 홈페이지

> **최종 업데이트**: 2026-03-05

---

## 서비스 개요

| 항목 | 내용 |
|------|------|
| 서비스명 | KCD Seoul 2026 홈페이지 |
| 유형 | 정적 사이트 (Static Site) |
| 기술 스택 | Next.js 14 + Tailwind CSS v3 → 정적 HTML/CSS/JS |
| 배포 플랫폼 | Vercel (권장) / GitHub Pages |
| 소유팀 | KCD Seoul 운영위원회 |
| 연락처 | contact@kcd-seoul.kr |

## 아키텍처

```
사용자 브라우저
      │
      ▼
  Vercel CDN (글로벌 엣지)
      │
      ▼
  정적 파일 서빙 (out/)
  ├── index.html
  ├── _next/static/  (JS 번들, CSS)
  └── images/        (발표자/스폰서 이미지)
```

> **백엔드 없음**: 완전한 정적 사이트. 서버 장애 지점 없음.
> 등록 폼 제출 시 외부 서비스(Formspree 등) 연동 필요.

---

## 로컬 개발

```bash
git clone <repository-url>
cd kcd-seoul
npm install
npm run dev       # http://localhost:3000
```

## 프로덕션 빌드

```bash
npm run build     # out/ 디렉토리 생성
```

## 배포

### Vercel (권장)

```bash
vercel --prod
```

### 수동 배포

```bash
npm run build
# out/ 폴더를 웹 서버에 업로드
```

---

## 콘텐츠 업데이트 가이드

### 행사 기본 정보 변경

**날짜/장소 변경:**
- `components/sections/Hero.tsx` — 히어로 섹션 날짜/장소 텍스트
- `components/sections/Schedule.tsx` — 일정 섹션 부제목

### 발표자 추가/수정

`data/speakers.ts` 파일 수정:

```typescript
{
  id: "s7",
  name: "새 발표자",
  company: "소속 회사",
  role: "직책",
  topic: "발표 주제",
  bio: "간략한 소개",
  imageUrl: "/images/speakers/speaker7.jpg",  // public/images/speakers/ 에 추가
}
```

### 세션 일정 추가/수정

`data/schedule.ts` 파일 수정. `type` 값:
- `"keynote"` — 파란 배지
- `"session"` — 연파란 배지
- `"break"` / `"lunch"` — 회색/노란색 배지

### 스폰서 추가/수정

`data/sponsors.ts` 파일 수정. `tier` 값: `"gold"` | `"silver"` | `"bronze"`

로고 이미지는 `public/images/sponsors/` 에 추가 후 `logoUrl` 경로 업데이트.

---

## 트러블슈팅

### 빌드 실패

```bash
# Node.js 버전 확인 (18.17+ 필요)
node --version

# 의존성 재설치
rm -rf node_modules package-lock.json
npm install
npm run build
```

### 스타일이 적용되지 않는 경우

```bash
# Tailwind 콘텐츠 경로 확인
# tailwind.config.js → content 배열에 해당 파일 경로 포함 여부 확인
```

### 이미지가 표시되지 않는 경우

- `public/images/` 경로에 파일이 존재하는지 확인
- `next.config.mjs`의 `images.unoptimized: true` 설정 확인

---

## 모니터링

정적 사이트이므로 별도 서버 모니터링 불필요. 다음 항목만 주기적 확인:

| 항목 | 주기 | 방법 |
|------|------|------|
| 사이트 접속 가능 여부 | 행사 전주 매일 | URL 직접 접속 |
| 등록 폼 정상 동작 | 행사 전주 매일 | 테스트 제출 |
| Vercel 배포 상태 | 배포 시마다 | Vercel 대시보드 |

---

## 행사 종료 후

1. 홈페이지를 아카이브 상태로 전환 (등록 폼 비활성화)
2. `Registration.tsx`에서 폼 제거 후 "행사가 종료되었습니다" 메시지 표시
3. 재빌드 및 재배포
4. 다음 연도 행사 준비 시 Inception 사이클 재시작
