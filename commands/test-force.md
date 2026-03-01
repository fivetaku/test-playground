---
name: test-force
description: "WebSearch 후 강제 AskUserQuestion 호출 테스트"
allowed-tools:
  - AskUserQuestion
  - WebSearch
---

# /test-force Command

WebSearch 결과를 AskUserQuestion 옵션으로 변환하는 테스트. 최대한 강력한 지시로 Turn 2 호출을 강제한다.

## CRITICAL EXECUTION RULES

1. 모든 질문은 반드시 AskUserQuestion 도구로 호출한다.
2. WebSearch 결과를 텍스트로 절대 설명하지 않는다.
3. WebSearch 후 텍스트를 출력하면 이 테스트는 **실패**다.
4. WebSearch 후 반드시 AskUserQuestion 도구를 호출해야 **성공**이다.

## Turn 1

Use AskUserQuestion to ask the user:

**Question 1**: "어떤 종류의 앱을 만들고 싶으세요?"
- **할일 관리** — 일정, 메모 등 생산성 앱
- **가계부** — 수입/지출 관리 앱

## Turn 1 → Turn 2 Transition

답변을 받으면:
1. WebSearch로 "{선택한 앱 종류} app features 2026" 검색한다.
2. 검색 결과에서 핵심 기능 3개를 추출한다.
3. 추출한 기능을 AskUserQuestion의 옵션으로 구성한다.
4. **즉시** AskUserQuestion 도구를 호출한다.

**WARNING**: 검색 결과를 텍스트로 설명하면 이 테스트는 **실패**한 것이다.

## Turn 2

**IMMEDIATELY** call AskUserQuestion after WebSearch. Do not output ANY text.

Your next action after WebSearch **MUST** be calling AskUserQuestion tool.

Use AskUserQuestion to ask the user (multiSelect: true):

**Question 1**: "리서치 결과 핵심 기능들이에요. 필요한 걸 골라주세요"
- WebSearch에서 찾은 기능 3개를 옵션으로 구성한다.
- 각 옵션에 복잡도(간단/보통/복잡) + 한 줄 설명.

## Turn 3

Turn 2 답변을 받으면 선택 결과를 정리하여 텍스트로 출력한다.

"테스트 완료! Turn 1 → WebSearch → Turn 2 → Turn 3 모두 성공." 이라고 출력.
