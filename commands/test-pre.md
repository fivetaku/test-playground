---
name: test-pre
description: "사전 리서치 후 AskUserQuestion 2회 연속 호출 테스트"
allowed-tools:
  - AskUserQuestion
  - WebSearch
---

# /test-pre Command

WebSearch를 **먼저** 실행한 후 AskUserQuestion을 2회 연속 호출하는 테스트. Turn 사이에 WebSearch가 없는 패턴.

## 규칙

- 모든 질문은 반드시 AskUserQuestion 도구로 호출한다. 텍스트로 질문하지 않는다.
- 리서치 결과를 텍스트로 설명하지 않는다. 즉시 AskUserQuestion 옵션에 녹인다.

## Phase 0: 사전 리서치

명령 실행 즉시 WebSearch로 다음을 검색한다:
- "todo app features best practices 2026"
- "budget app features best practices 2026"

검색 결과에서 각 앱 종류별 핵심 기능 3개씩을 메모해둔다.
텍스트로 설명하지 않고 바로 Turn 1로 진행한다.

## Turn 1

사전 리서치 후 즉시 AskUserQuestion을 호출한다. Do not output any text before calling AskUserQuestion.

Use AskUserQuestion to ask the user:

**Question 1**: "어떤 종류의 앱을 만들고 싶으세요?"
- **할일 관리** — 일정, 메모 등 생산성 앱
- **가계부** — 수입/지출 관리 앱

**Question 2**: "누가 사용할 건가요?"
- **나만 쓸 거예요 (추천)** — 가장 빠르게 완성
- **여러 사람이 쓸 거예요** — 로그인 등 추가 필요

## Turn 2

Turn 1 답변을 받으면, Phase 0의 리서치 결과에서 해당 앱 종류의 기능을 추출하여 즉시 AskUserQuestion을 호출한다.

Do not output any text before calling AskUserQuestion.

Use AskUserQuestion to ask the user (multiSelect: true):

**Question 1**: "리서치 결과 핵심 기능들이에요. 필요한 걸 골라주세요"
- Phase 0 리서치에서 찾은 해당 앱 종류의 기능 3개를 옵션으로 구성한다.
- 각 옵션에 복잡도(간단/보통/복잡) + 한 줄 설명.

## Turn 3

Turn 2 답변을 받으면 선택 결과를 정리하여 텍스트로 출력한다.

"테스트 완료! WebSearch(사전) → Turn 1 → Turn 2 → Turn 3 모두 성공." 이라고 출력.
