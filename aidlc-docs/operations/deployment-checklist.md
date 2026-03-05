# Deployment Checklist — KCD Seoul 홈페이지

> **배포 전 모든 항목을 완료해야 합니다.**
> 최종 업데이트: 2026-03-05

---

## Pre-Deployment

### 문서 검증
- [x] `aidlc-docs/`의 모든 산출물이 현재 코드베이스와 일치하는가
- [x] `audit.md`에 전 단계의 승인 기록이 완전한가
- [x] ADR-0001이 최신 아키텍처 결정(Next.js 14 + Tailwind v3)을 반영하는가
- [x] `aidlc-state.md`가 현재 상태를 정확히 반영하는가

### 코드 품질
- [x] `next build` 성공 (Static export, 0 errors)
- [x] TypeScript 타입 체크 통과
- [ ] 브라우저 크로스 테스트 (Chrome, Safari, Firefox, Edge)
- [ ] 모바일 반응형 확인 (320px, 768px, 1440px)
- [ ] 다크 모드 렌더링 확인

### 콘텐츠
- [ ] 행사 날짜/장소 플레이스홀더 → 실제 정보로 교체
  - `components/sections/Hero.tsx` — 날짜, 장소
  - `components/sections/Schedule.tsx` — 날짜, 장소
  - `data/speakers.ts` — 실제 발표자 정보
  - `data/schedule.ts` — 실제 세션 정보
  - `data/sponsors.ts` — 실제 스폰서 정보
- [ ] 연락처 이메일 교체 (`contact@kcd-seoul.kr`, `sponsor@kcd-seoul.kr`)
- [ ] SNS 링크 교체 (Twitter, GitHub)
- [ ] 발표자 사진 `public/images/speakers/` 에 추가
- [ ] 스폰서 로고 `public/images/sponsors/` 에 추가

### 보안
- [x] XSS 방어 (React 기본 이스케이핑)
- [x] 외부 링크 `rel="noopener noreferrer"` 전체 적용
- [x] 민감 정보 하드코딩 없음
- [ ] `npm audit` — 1 high severity 취약점 확인 및 처리

### 인프라
- [ ] 배포 플랫폼 선택 및 설정 (Vercel 권장)
- [ ] 커스텀 도메인 설정 (예: kcd-seoul.kr)
- [ ] HTTPS 인증서 확인

## Deployment

### Vercel 배포 (권장)

```bash
# Vercel CLI 설치
npm i -g vercel

# 프로젝트 루트에서 실행
cd kcd-seoul
vercel

# 프로덕션 배포
vercel --prod
```

### GitHub Pages 배포 (대안)

```bash
npm run build
# out/ 폴더를 gh-pages 브랜치에 push
```

- [ ] 배포 시작 시간 기록: ___________
- [ ] 배포 완료 확인: ___________
- [ ] 배포 URL 기록: ___________

## Post-Deployment

- [ ] 메인 URL 접속 정상 확인
- [ ] 전체 섹션 스크롤 확인 (히어로→소개→발표자→일정→스폰서→등록)
- [ ] 내비게이션 링크 동작 확인
- [ ] 등록 폼 제출 테스트
- [ ] 모바일 햄버거 메뉴 동작 확인
- [ ] 스폰서 로고 외부 링크 확인
- [ ] 배포 결과 `audit.md` 기록 완료

---

**최종 승인**

| 역할 | 이름 | 승인 날짜 |
|------|------|---------|
| 개발 담당자 | | |
| 행사 주최자 | | |
