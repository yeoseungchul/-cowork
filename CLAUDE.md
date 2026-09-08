# CLAUDE.md — 서진 에이전트 운영 지침

> **Hermes Agent 폐쇄형 학습 루프 원칙** 기반의 성장형 에이전트 환경.  
> 매 세션이 끝날 때 이 저장소는 이전보다 더 똑똑해진다.

---

## 🧠 에이전트 정체성

- 페르소나 → `SOUL.md` 참조
- 성장 로그 → `GROWTH.md` 참조
- 사용자 모델 → `memory/user-profile.md` 참조

---

## 📁 디렉토리 구조

```
-cowork/
├── CLAUDE.md           ← 이 파일 (에이전트 두뇌)
├── SOUL.md             ← 페르소나 & 가치관
├── GROWTH.md           ← 자기 개선 로그
│
├── memory/
│   ├── user-profile.md ← 사용자 모델 (지속 성장)
│   ├── patterns.md     ← 세션 간 학습된 패턴
│   └── context.md      ← 현재 작업 컨텍스트
│
├── skills/
│   ├── README.md       ← 스킬 인덱스
│   └── [skill-name].md ← 재사용 가능한 절차형 스킬
│
├── sessions/
│   └── YYYY-MM-DD.md   ← 세션 로그 (자동 생성)
│
├── tasks/
│   └── [task-name].md  ← 작업 추적
│
└── .claude/
    ├── settings.json   ← 훅 & 권한
    └── agents/         ← 서브에이전트 정의
```

---

## 🔄 폐쇄형 학습 루프 (Closed-Loop Learning)

Hermes Agent의 5가지 자기개선 메커니즘을 구현한다.

### 1. 세션 시작 시 컨텍스트 로드

세션을 시작할 때 반드시 다음 순서로 읽는다:

```
1. SOUL.md              → 페르소나 재확인
2. memory/user-profile.md → 사용자 선호 & 패턴
3. memory/patterns.md   → 이전 세션 학습 내용
4. memory/context.md    → 현재 진행 중인 작업
5. GROWTH.md            → 에이전트 성장 이력
```

### 2. 자율 스킬 생성 (Autonomous Skill Creation)

복잡한 작업을 완료한 후, 해당 절차를 `skills/` 디렉토리에 저장한다.

**스킬 생성 트리거:**
- 3단계 이상의 절차가 필요한 작업
- 반복될 가능성이 높은 작업 유형
- 새로운 도메인 지식이 필요했던 경우

**스킬 파일 형식:** `skills/[동사-명사].md`

### 3. 지속적 스킬 정제 (Continuous Skill Refinement)

기존 스킬을 사용한 후, 개선점을 발견하면 해당 스킬 파일을 업데이트한다.

### 4. 패턴 인코딩 (Pattern Encoding)

세션 종료 시 `memory/patterns.md`에 다음을 기록한다:
- 자주 요청되는 작업 유형
- 사용자의 선호 방식
- 효과적이었던 접근법
- 피해야 할 실수

### 5. 사용자 모델링 (User Modeling)

`memory/user-profile.md`를 지속적으로 업데이트한다:
- 커뮤니케이션 스타일 선호도
- 도메인 지식 수준
- 의사결정 패턴

---

## 🔧 세션 종료 프로토콜

> 세션이 끝나기 전, 아래 작업을 수행하고 커밋·푸시한다.

```bash
# 1. 오늘 세션 로그 저장
sessions/YYYY-MM-DD.md 작성

# 2. 패턴 업데이트
memory/patterns.md 업데이트

# 3. 새 스킬 있으면 저장
skills/[스킬명].md 작성

# 4. 성장 로그 업데이트
GROWTH.md 업데이트

# 5. 커밋 & 푸시
git add -A && git commit -m "session: [날짜] [주요작업]"
git push -u origin [브랜치명]
```

---

## ✍️ 문서 작성 원칙

1. **오타·글자 깨짐 금지** — 작성 후 반드시 검수
2. **회사명 정확 기재** — (주)서진항공 / (주)서진월드투어
3. **격식체 유지** — 공문서는 존댓말, 내부 메모는 평어 가능
4. **도메인 용어 정확 사용** — 인바운드/아웃바운드, 무사증, 메디컬투어

---

## 🤖 서브에이전트 사용 지침

병렬 처리가 필요한 경우 `.claude/agents/`의 서브에이전트를 활용한다:
- 복잡한 리서치 → `general-purpose` 에이전트
- 넓은 코드베이스 탐색 → `Explore` 에이전트
- 구현 계획 수립 → `Plan` 에이전트

---

## 📊 성능 지표

매 세션 후 GROWTH.md에 기록:
- 완료한 주요 작업 수
- 신규 스킬 생성 수
- 기존 스킬 정제 수
- 메모리 업데이트 항목 수
