---
description: AWS AI-Driven Development Lifecycle (AI-DLC) 워크플로우를 강제하는 적응형 소프트웨어 개발 거버넌스 스킬. 각 페이즈(Inception/Construction/Operations)에서 인간-AI 협업, 문서 우선 원칙, 감사 추적을 보장한다.
---

# AWS AI-DLC 워크플로우 거버넌스

## Mission Statement

**AI-DLC(AI-Driven Development Lifecycle)**는 AI를 소프트웨어 개발의 보조 도구가 아닌, 의사결정 파트너로 위치시키는 AWS의 적응형 방법론이다.

**핵심 철학 3가지**:
1. **Documentation-First**: 코드 삭제 후에도 "무엇을, 왜 만들었는지"의 완전한 기록이 남아야 한다. 모든 산출물은 `aidlc-docs/`에 먼저 생성된다.
2. **Traceability**: 모든 AI 입출력과 사용자 결정은 ISO 8601 타임스탬프와 함께 `audit.md`에 기록된다. 요약이 아닌 원본 그대로 보존한다.
3. **Human-in-the-Loop**: AI는 계획을 수립하고 선택지를 제시한다. 실행은 반드시 사용자의 명시적 승인 후에만 이루어진다.

---

## Phase Definitions

### Phase 1: Inception (무엇을, 왜)

**목적**: 비즈니스 요구사항을 검증된 기술 명세로 변환한다.

**실행 단계**:
1. **Workspace Detection**: 기존 코드 확인 → Greenfield(신규) vs Brownfield(기존) 판단. `aidlc-state.md` 존재 시 이전 세션에서 재개.
2. **Requirements Analysis**: 요청 명확도와 복잡도에 따라 깊이 조정 (minimal / standard / comprehensive).
3. **Reverse Engineering** (Brownfield 전용): 기존 패키지, 비즈니스 로직, 아키텍처, API, 의존성 다이어그램 분석.
4. **User Stories**: 사용자 대면 기능, 복잡한 비즈니스 로직, 멀티 컴포넌트 변경 시 실행. 단순 리팩토링은 스킵.
5. **Application Design**: 새 컴포넌트가 필요한 경우, 메서드·비즈니스 규칙·서비스 레이어·의존성 정의.
6. **Units Generation**: 복잡한 시스템을 구조화된 작업 단위(Work Unit)로 분해.

**ADR(Architecture Decision Records) 규칙**:
- 아키텍처적 결정(프레임워크 선택, 데이터 모델, 외부 의존성)은 반드시 `aidlc-docs/decisions/ADR-NNNN-title.md`로 기록한다.
- ADR 형식: Context → Decision → Consequences → Alternatives Considered
- 이전 결정을 번복할 경우 새 ADR을 생성하고 기존 ADR을 Superseded로 표시한다.

**승인 게이트**: 각 단계 완료 후 사용자 명시적 승인 필요. 승인 내용은 `audit.md`에 기록.

---

### Phase 2: Construction (어떻게)

**목적**: 승인된 설계를 기반으로 품질이 검증된 코드를 생성한다.

**작업 단위(Work Unit)별 순서 실행**:
1. **Functional Design** (신규 데이터 모델 또는 복잡한 비즈니스 로직 시): 상세 설계 명세 작성.
2. **NFR Requirements** (성능·보안·확장성 요구 시): 비기능 요구사항 정의.
3. **NFR Design**: NFR 요구사항이 존재하는 경우 아키텍처 패턴 적용.
4. **Infrastructure Design**: 클라우드 서비스 매핑, 배포 아키텍처, IAC(Infrastructure as Code) 설계.
5. **Code Generation** (항상 실행): 두 단계로 분리 — ① 상세 실행 계획 수립 → ② 승인 후 코드 생성.

**AI 생성 코드 검증 절차 (TDD 기반)**:
- 코드 생성 전 테스트 케이스 먼저 작성 (Red)
- AI가 테스트를 통과하는 코드 생성 (Green)
- 중복 제거 및 가독성 개선 (Refactor)
- `build-and-test/` 폴더에 빌드·단위·통합·성능 테스트 지침 생성

**보안 게이트웨이 기준**:
- OWASP Top 10 취약점 스캔 (인젝션, XSS, IDOR 등)
- IAM 최소 권한 원칙 준수 확인
- 시크릿/자격증명 하드코딩 금지 검증
- 의존성 CVE 확인 (HIPAA·PCI-DSS·SOC 2 확장 룰 적용 가능)

**완료 패턴**: 표준화된 2가지 선택지 메시지 — "변경 요청" 또는 "계속 진행". 단계 완료 즉시 계획 체크박스 `[x]` 업데이트.

---

### Phase 3: Operations (배포 및 운영)

**목적**: 생산 환경 배포 준비 상태를 검증하고 피드백 루프를 구성한다.

**배포 전 체크리스트**:
- [ ] `aidlc-docs/`의 모든 산출물이 현재 코드베이스와 일치하는가
- [ ] `audit.md`에 전 단계의 승인 기록이 완전한가
- [ ] 보안 게이트웨이 모든 항목 통과했는가
- [ ] ADR이 최신 아키텍처 결정을 반영하는가
- [ ] 롤백 절차가 문서화되어 있는가

**피드백 루프 구성**:
- 배포 후 모니터링 지표를 `aidlc-docs/operations/runbook.md`에 정의
- 인시던트 발생 시 Post-Mortem을 `aidlc-docs/operations/postmortem-YYYYMMDD.md`로 기록
- 운영 이슈는 다음 Inception 사이클의 입력 요구사항으로 환류

---

## Mandatory Artifacts

각 단계에서 반드시 생성 또는 업데이트해야 하는 파일:

| 단계 | 필수 파일 | 설명 |
|------|-----------|------|
| **공통 (항상)** | `aidlc-docs/audit.md` | 모든 사용자 입력 및 AI 응답의 타임스탬프 로그 |
| **공통 (항상)** | `aidlc-state.md` | 현재 페이즈·단계·진행 상태 |
| **Inception** | `aidlc-docs/inception/requirements.md` | 요구사항 명세서 |
| **Inception** | `aidlc-docs/inception/user-stories.md` | 사용자 스토리 (해당 시) |
| **Inception** | `aidlc-docs/decisions/ADR-NNNN-*.md` | 아키텍처 결정 기록 |
| **Construction** | `aidlc-docs/construction/plan.md` | 승인된 구현 계획 (체크박스 포함) |
| **Construction** | `aidlc-docs/construction/functional-design.md` | 기능 설계 명세 (해당 시) |
| **Construction** | `build-and-test/*.md` | 빌드 및 테스트 지침 |
| **Operations** | `aidlc-docs/operations/runbook.md` | 운영 런북 |
| **Operations** | `aidlc-docs/operations/deployment-checklist.md` | 배포 전 체크리스트 |

**디렉토리 규칙**:
- 애플리케이션 코드: 워크스페이스 루트에만 위치
- 문서 산출물: `aidlc-docs/`에만 위치
- 코드를 `aidlc-docs/` 내부에 절대 배치 금지

---

## Tool / Command Mapping

### `/ai-dlc-init`
**목적**: 신규 프로젝트에 AI-DLC 폴더 구조 및 기본 템플릿 세팅.

실행 시 생성되는 구조:
```
aidlc-docs/
├── audit.md                    # 감사 로그 (자동 생성)
├── inception/
│   ├── requirements.md         # 요구사항 명세서 템플릿
│   └── user-stories.md         # 사용자 스토리 템플릿
├── decisions/                  # ADR 저장소
├── construction/
│   └── plan.md                 # 구현 계획 템플릿
└── operations/
    ├── runbook.md              # 운영 런북 템플릿
    └── deployment-checklist.md # 배포 체크리스트 템플릿
aidlc-state.md                  # 현재 단계 추적 파일
build-and-test/                 # 테스트 지침 폴더
```

### `/ai-dlc-check`
**목적**: 현재 작업이 AI-DLC 거버넌스를 준수하는지 자동 감사.

감사 항목:
1. `aidlc-state.md`에서 현재 페이즈와 단계 확인
2. 해당 페이즈의 Mandatory Artifacts 존재 여부 확인
3. `audit.md`에 최근 사용자 승인 기록 확인
4. `aidlc-docs/`에 코드 파일이 없는지 확인
5. 미완료 계획 체크박스 확인
6. 위반 항목 목록과 수정 방법 보고

---

## Guardrails (Human-in-the-Loop 강제 규칙)

AI는 다음 상황에서 **반드시 멈추고 사용자 승인을 요청**해야 한다:

### 절대 금지 사항
- `aidlc-docs/`에 해당 단계의 필수 문서가 없는 상태에서 코드 파일 수정 금지
- 사용자 승인 없이 다음 단계로 자동 진행 금지
- `audit.md`에 원본이 아닌 요약된 사용자 입력 기록 금지
- 계획 수립과 코드 생성을 단일 단계로 통합 금지 (반드시 분리)
- 3가지 이상의 선택지 제시 금지 (표준: 2가지 선택지만)

### 승인 요청 시점
| 트리거 | 필요한 승인 |
|--------|------------|
| 페이즈 전환 (Inception → Construction) | 명시적 승인 + audit.md 기록 |
| 코드 생성 시작 전 | plan.md 검토 및 승인 |
| 아키텍처 결정 사항 | ADR 작성 후 승인 |
| 외부 의존성 추가 | NFR/보안 검토 후 승인 |
| 배포 실행 전 | 배포 체크리스트 완료 확인 |

### Audit 로그 형식 (필수 준수)
```
[ISO8601-Timestamp] | [Phase/Stage] | [Raw User Input] | [AI Response Summary]
```
예시:
```
[2026-03-04T09:15:00+09:00] | [Inception/Requirements] | [사용자: "인증 시스템 추가해줘"] | [AI: 요구사항 분석 단계 시작, 상세 명세 요청]
```

---

## 활성화 방법

이 스킬은 다음 형식으로 활성화한다:

```
"Using AI-DLC, [작업 요청 내용]"
```

예시:
- `"Using AI-DLC, 사용자 인증 시스템을 구현해줘"`
- `"Using AI-DLC, 기존 결제 모듈을 리팩토링해줘"`

---

*참고 출처: [AWS AI-DLC 공식 저장소](https://github.com/awslabs/aidlc-workflows) | [AWS DevOps 블로그](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)*
