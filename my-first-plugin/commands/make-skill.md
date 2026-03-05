# Role: AWS AI-DLC 기반 Custom Skill 설계 전문가

## Task: AWS AI-DLC 원칙을 내재화한 Claude Code 'SKILL.md' 정교화

다음 단계에 따라 현재 프로젝트의 `.claude/skills/ai-dlc/SKILL.md`를 최신화하고 고도화하라.

### Step 1: 외부 지식 탐색 및 분석
1. **GitHub 탐색**: `github.com/aws-samples/ai-driven-software-development-lifecycle` (또는 관련 AWS AI-DLC 저장소)를 검색하여 다음 항목을 분석하라.
   - 프로젝트 구조 (Folder hierarchy)
   - 핵심 메타데이터 파일 (e.g., `PROMPT.md`, `CONTEXT.md`, `GOVERNANCE.md`)
   - AI Agent를 위한 페이즈별(Inception, Construction, Operations) 가이드라인
2. **블로그 및 기술 문서 탐색**: AWS 공식 블로그의 "AI-Driven Software Development Lifecycle" 관련 게시물을 찾아 다음 정보를 추출하라.
   - 'Agentic Workflow'에서 강조하는 인간-AI 협업 모델
   - 코드 리뷰 및 보안(Security) 게이트웨이의 구체적 기준

### Step 2: SKILL.md 구조 설계 (Rich Markdown Format)
탐색한 내용을 바탕으로 `.claude/skills/ai-dlc/SKILL.md`를 다음 섹션을 포함하여 작성(또는 수정)하라:

1. **Mission Statement**: AI-DLC의 철학(Documentation-First, Traceability) 요약.
2. **Phase Definitions**: 
   - **Inception**: 요구사항 분석 및 `ADR(Architecture Decision Records)` 작성 규칙.
   - **Construction**: TDD 기반 개발 및 AI 생성 코드의 검증 절차.
   - **Operations**: 배포 전 체크리스트 및 피드백 루프 구성.
3. **Mandatory Artifacts**: 각 단계마다 반드시 생성/업데이트해야 하는 파일 목록 (예: `aidlc/inception.md`).
4. **Tool/Command Mapping**: 
   - `/ai-dlc-init`: 폴더 구조 및 기본 템플릿 세팅.
   - `/ai-dlc-check`: 현재 작업이 AI-DLC 거버넌스를 준수하는지 자동 감사.
5. **Guardrails**: AI가 독단적으로 코드를 수정하지 못하게 하는 'Human-in-the-loop' 강제 규칙.

### Step 3: 실행 계획 수립
- 분석이 끝나면, 위 구조에 따라 `SKILL.md`를 즉시 생성하라.
- 추가로, 이 스킬이 참조할 `templates/` 폴더 내의 핵심 마크다운 템플릿(요구사항 정의서 등) 예시 1종을 함께 생성하라.

## Output Format: Functional Specification

보고서 작성 시 아래 구조의 마크다운 형식을 준수하라:

```markdown
---
description: {설명}
disable-model-invocation: true
---

{내용}

---
**지금 바로 Step 1의 탐색부터 시작하여 분석 결과를 요약하고 파일을 작성해줘.**