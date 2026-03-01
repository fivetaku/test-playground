---
name: test-ask
description: "AskUserQuestion 다단계 호출 테스트"
allowed-tools:
  - AskUserQuestion
  - WebSearch
---

# /test-ask Command

AskUserQuestion 도구의 다단계 호출을 테스트한다.

## 규칙

- 모든 질문은 반드시 AskUserQuestion 도구로 호출한다. 텍스트로 질문하지 않는다.
- 리서치 결과를 텍스트로 설명하지 않는다. 즉시 AskUserQuestion 옵션에 녹인다.

## Turn 1

Use AskUserQuestion to ask the user:

**Question 1**: "어떤 종류의 앱을 만들고 싶으세요?"
- **할일 관리** — 일정, 메모 등 생산성 앱
- **가계부** — 수입/지출 관리 앱
- **블로그** — 글 작성/공유 플랫폼

**Question 2**: "누가 사용할 건가요?"
- **나만 쓸 거예요 (추천)** — 가장 빠르게 완성
- **여러 사람이 쓸 거예요** — 로그인 등 추가 필요

## Turn 1 → Turn 2

답변을 받으면 WebSearch로 "{선택한 앱 종류} app features 2026" 리서치한다.
리서치 결과를 텍스트로 설명하지 말고 즉시 Turn 2의 AskUserQuestion을 호출한다.

## Turn 2

리서치 결과를 바탕으로 즉시 AskUserQuestion을 호출한다. Do not output any text before calling AskUserQuestion.

Use AskUserQuestion to ask the user:

**Question 1** (multiSelect: true): "리서치 결과 핵심 기능들이에요. 필요한 걸 골라주세요"
- 리서치에서 찾은 기능 3-4개를 옵션으로 구성한다.
- 각 옵션에 복잡도(간단/보통/복잡) + 한 줄 설명.

## Turn 3

Turn 2 답변을 받으면 선택 결과를 정리하여 텍스트로 출력한다.

"테스트 완료! Turn 1 → WebSearch → Turn 2 → Turn 3 모두 성공." 이라고 출력.
