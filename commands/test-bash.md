---
name: test-bash
description: "AskUserQuestion → Bash → AskUserQuestion 테스트"
allowed-tools:
  - AskUserQuestion
  - Bash
---

# /test-bash Command

Bash 실행 후 AskUserQuestion을 호출하는 테스트. omc-setup 패턴과 동일한 구조.

## 규칙

- 모든 질문은 반드시 AskUserQuestion 도구로 호출한다. 텍스트로 질문하지 않는다.
- Bash 결과를 텍스트로 설명하지 않는다. 즉시 다음 AskUserQuestion을 호출한다.

## Turn 1

Use AskUserQuestion to ask the user:

**Question 1**: "어떤 종류의 앱을 만들고 싶으세요?"
- **할일 관리** — 일정, 메모 등 생산성 앱
- **가계부** — 수입/지출 관리 앱

**Question 2**: "누가 사용할 건가요?"
- **나만 쓸 거예요 (추천)** — 가장 빠르게 완성
- **여러 사람이 쓸 거예요** — 로그인 등 추가 필요

## Turn 1 → Turn 2

답변을 받으면 Bash로 간단한 명령을 실행한다:

```bash
echo "앱 종류: $(date +%Y)" && echo "리서치 시뮬레이션 완료"
```

Bash 결과를 텍스트로 설명하지 말고 즉시 Turn 2의 AskUserQuestion을 호출한다.

## Turn 2

Bash 실행 후 즉시 AskUserQuestion을 호출한다. Do not output any text before calling AskUserQuestion.

Use AskUserQuestion to ask the user:

**Question 1** (multiSelect: true): "어떤 기능이 필요하세요?"
- **기본 CRUD** — 데이터 생성, 읽기, 수정, 삭제 (간단)
- **검색/필터** — 데이터 검색 및 필터링 (간단)
- **대시보드** — 통계와 요약 화면 (보통)
- **알림** — 푸시 알림, 이메일 알림 (복잡)

## Turn 3

Turn 2 답변을 받으면 선택 결과를 정리하여 텍스트로 출력한다.

"테스트 완료! Turn 1 → Bash → Turn 2 → Turn 3 모두 성공." 이라고 출력.
