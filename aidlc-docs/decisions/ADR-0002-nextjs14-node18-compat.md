# ADR-0002: Next.js 14 + Tailwind CSS v3 채택 (Node.js 18 호환)

> **상태**: Accepted
> **날짜**: 2026-03-05
> **Supersedes**: ADR-0001 일부 수정 (버전 조정)

---

## Context

`create-next-app` 실행 시 최신 버전인 Next.js 16.1.6이 설치됨.
그러나 현재 환경의 Node.js 버전이 18.20.8로, Next.js 16과 Tailwind CSS v4가
요구하는 Node.js 20+ 미충족.

- Next.js 16: Node.js >=20.9.0 필요
- Tailwind CSS v4 (`@tailwindcss/oxide`): Node.js >= 20 필요

## Decision

**Next.js 14.2.x + Tailwind CSS v3**로 조정한다.

- Next.js 14.2는 Node.js 18.17+ 지원 (LTS 버전 중 가장 최신 안정 릴리즈)
- Tailwind CSS v3는 Node.js 18 완전 지원
- `next.config.ts` → `next.config.mjs` 변환 (Next.js 14에서 `.ts` 미지원)

## Consequences

**긍정적**:
- 현재 환경(Node.js 18)에서 정상 빌드 및 운영 가능
- Next.js 14는 LTS 지원 버전으로 안정성 높음

**부정적**:
- 최신 Next.js 기능(Partial Prerendering 등) 미사용
- 추후 Node.js 20 업그레이드 후 Next.js 15/16 마이그레이션 필요

## Migration Path

```bash
# Node.js 20 설치 후
nvm install 20
nvm use 20
npm install next@latest tailwindcss@latest @tailwindcss/postcss
```

## Alternatives Considered

| 대안 | 기각 이유 |
|------|---------|
| Node.js 20 설치 후 Next.js 16 사용 | 현재 환경 제약, 사용자 승인 필요 |
| 순수 HTML/CSS/JS | 컴포넌트 재사용성 저하 |
