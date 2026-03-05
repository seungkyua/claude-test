# ADR-0001: Next.js + TypeScript + Tailwind CSS 채택

> **상태**: Accepted
> **날짜**: 2026-03-05
> **결정자**: 사용자 (AI-DLC Inception 단계)

---

## Context

KCD Seoul 행사 홈페이지는 다음 요구사항을 만족해야 한다:
- SEO 최적화 (행사명 검색 상위 노출)
- 빠른 페이지 로드 성능 (Lighthouse 90+)
- 무료 정적 배포 가능
- 빠른 개발 속도

## Decision

**Next.js 14 (App Router) + TypeScript + Tailwind CSS** 조합을 채택한다.

- **Next.js**: SSG(Static Site Generation) 모드로 빌드하여 완전한 정적 파일 생성 → Vercel/GitHub Pages 무료 배포
- **TypeScript**: 컴포넌트 props 타입 안전성 확보
- **Tailwind CSS**: 유틸리티 클래스 기반으로 디자인 시스템 일관성 유지, 빠른 UI 개발

## Consequences

**긍정적**:
- `next export`로 정적 HTML 생성 → 서버 불필요
- App Router의 Server Components로 초기 번들 크기 최소화
- Tailwind JIT로 사용하지 않는 CSS 자동 제거

**부정적**:
- React 학습 곡선 (순수 HTML 대비)
- Node.js 빌드 환경 필요

## Alternatives Considered

| 대안 | 기각 이유 |
|------|---------|
| 순수 HTML/CSS/JS | 컴포넌트 재사용성 낮음, 유지보수 어려움 |
| Vue 3 + Vite | 팀 경험 및 생태계 대비 Next.js 선호 |
| Gatsby | Next.js 대비 생태계 축소 추세 |
