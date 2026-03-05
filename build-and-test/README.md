# Build and Test Guidelines

> 이 폴더에는 프로젝트의 빌드, 단위 테스트, 통합 테스트, 성능 테스트 지침이 포함됩니다.
> Construction 단계에서 Code Generation 전에 테스트 케이스를 먼저 작성합니다 (TDD).

---

## TDD 워크플로우

```
1. Red   → 테스트 케이스 먼저 작성 (실패 상태)
2. Green → 테스트를 통과하는 최소한의 코드 작성
3. Refactor → 중복 제거 및 가독성 개선
```

## 파일 구조

```
build-and-test/
├── README.md              # 이 파일
├── unit-tests.md          # 단위 테스트 지침 및 케이스
├── integration-tests.md   # 통합 테스트 지침
├── performance-tests.md   # 성능 테스트 지침
└── build-guide.md         # 빌드 절차
```

## 파일 생성 시점

각 Work Unit의 Code Generation 단계 시작 전에 해당 테스트 파일을 생성합니다.
