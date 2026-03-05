# Build Guide — KCD Seoul

## 환경 요구사항

| 항목 | 버전 |
|------|------|
| Node.js | 18.17+ (권장: 20+) |
| npm | 10+ |
| Next.js | 14.2.x |
| Tailwind CSS | 3.x |

> **참고**: Node.js 18 환경에서는 Next.js 14를 사용합니다. Next.js 15+ 사용 시 Node.js 20 이상 필요.

## 개발 서버 실행

```bash
cd kcd-seoul
npm install
npm run dev
# → http://localhost:3000
```

## 프로덕션 빌드

```bash
npm run build
# 결과물: kcd-seoul/out/ (정적 파일)
```

## 정적 파일 미리보기

```bash
npx serve out
# → http://localhost:3000
```

## Vercel 배포

```bash
npx vercel
```

## 빌드 산출물 구조

```
out/
├── index.html        # 메인 페이지
├── _next/
│   └── static/       # JS/CSS 번들
└── public/           # 이미지 등 정적 에셋
```
