---
name: test-notools
description: "동적 옵션 생성 테스트 (WebSearch 없이)"
allowed-tools:
  - AskUserQuestion
---

# /test-notools Command

WebSearch 없이 Turn 1 답변을 기반으로 동적 옵션을 생성하여 Turn 2 AskUserQuestion을 호출하는 테스트.

## 규칙

- 모든 질문은 반드시 AskUserQuestion 도구로 호출한다. 텍스트로 질문하지 않는다.

## Turn 1

Use AskUserQuestion to ask the user:

**Question 1**: "어떤 종류의 앱을 만들고 싶으세요?"
- **할일 관리** — 일정, 메모 등 생산성 앱
- **가계부** — 수입/지출 관리 앱
- **블로그** — 글 작성/공유 플랫폼

## Turn 2

Turn 1에서 사용자가 선택한 앱 종류에 맞는 기능을 직접 구성하여 AskUserQuestion을 호출한다.

Do not output any text before calling AskUserQuestion.

사용자가 **할일 관리**를 선택한 경우의 옵션:
- **일정 관리** — 달력에 일정 추가/수정 (간단)
- **메모장** — 텍스트 메모 작성 (간단)
- **알림 설정** — 마감일 알림 (보통)
- **태그/카테고리** — 항목 분류 (간단)

사용자가 **가계부**를 선택한 경우의 옵션:
- **수입/지출 기록** — 거래 내역 입력 (간단)
- **카테고리 분류** — 항목별 분류 (간단)
- **월별 리포트** — 월간 요약 화면 (보통)
- **예산 설정** — 카테고리별 예산 (보통)

사용자가 **블로그**를 선택한 경우의 옵션:
- **글 작성/편집** — 마크다운 에디터 (간단)
- **카테고리/태그** — 글 분류 (간단)
- **댓글** — 독자 댓글 기능 (보통)
- **구독** — 이메일 구독 (복잡)

Use AskUserQuestion to ask the user (multiSelect: true):

**Question 1**: "필요한 기능을 골라주세요"
- 사용자가 선택한 앱 종류에 해당하는 위 옵션을 사용한다.

## Turn 3

Turn 2 답변을 받으면 선택 결과를 정리하여 텍스트로 출력한다.

"테스트 완료! Turn 1 → Turn 2(동적) → Turn 3 모두 성공." 이라고 출력.
