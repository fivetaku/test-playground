---
name: test-chain
description: "WebSearch → Bash → AskUserQuestion 체인 테스트"
allowed-tools:
  - AskUserQuestion
  - WebSearch
  - Bash
---

# /test-chain Command

WebSearch 후 Bash를 실행하고 AskUserQuestion을 호출하는 테스트. Bash가 WebSearch 컨텍스트를 "리셋"하는지 확인한다.

## 규칙

- 모든 질문은 반드시 AskUserQuestion 도구로 호출한다. 텍스트로 질문하지 않는다.
- WebSearch/Bash 결과를 텍스트로 설명하지 않는다.

## Turn 1

Use AskUserQuestion to ask the user:

**Question 1**: "어떤 종류의 앱을 만들고 싶으세요?"
- **할일 관리** — 일정, 메모 등 생산성 앱
- **가계부** — 수입/지출 관리 앱

## Turn 1 → Turn 2

답변을 받으면 순서대로 실행한다:

1. WebSearch로 "{선택한 앱 종류} app features 2026" 검색한다.
2. 검색 결과에서 핵심 기능 3개를 추출한다.
3. Bash로 `echo "features extracted"` 실행한다.
4. 즉시 AskUserQuestion을 호출한다.

## Turn 2

Bash 실행 후 즉시 AskUserQuestion을 호출한다. Do not output any text before calling AskUserQuestion.

Use AskUserQuestion to ask the user (multiSelect: true):

**Question 1**: "리서치 결과 핵심 기능들이에요. 필요한 걸 골라주세요"
- WebSearch에서 찾은 기능 3개를 옵션으로 구성한다.
- 각 옵션에 복잡도(간단/보통/복잡) + 한 줄 설명.

## Turn 3

Turn 2 답변을 받으면 선택 결과를 정리하여 텍스트로 출력한다.

"테스트 완료! Turn 1 → WebSearch → Bash → Turn 2 → Turn 3 모두 성공." 이라고 출력.
