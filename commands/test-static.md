---
name: test-static
description: "CONTROL: AskUserQuestion 2회 연속 호출 (중간 도구 없음)"
allowed-tools:
  - AskUserQuestion
---

# /test-static Command

AskUserQuestion을 2회 연속 호출하는 컨트롤 테스트. 중간에 다른 도구 호출 없음.

## 규칙

- 모든 질문은 반드시 AskUserQuestion 도구로 호출한다. 텍스트로 질문하지 않는다.

## Turn 1

Use AskUserQuestion to ask the user:

**Question 1**: "어떤 종류의 앱을 만들고 싶으세요?"
- **할일 관리** — 일정, 메모 등 생산성 앱
- **가계부** — 수입/지출 관리 앱
- **블로그** — 글 작성/공유 플랫폼

**Question 2**: "누가 사용할 건가요?"
- **나만 쓸 거예요 (추천)** — 가장 빠르게 완성
- **여러 사람이 쓸 거예요** — 로그인 등 추가 필요

## Turn 2

Turn 1 답변을 받으면 즉시 AskUserQuestion을 호출한다. Do not output any text before calling AskUserQuestion.

Use AskUserQuestion to ask the user:

**Question 1** (multiSelect: true): "어떤 기능이 필요하세요?"
- **기본 CRUD** — 데이터 생성, 읽기, 수정, 삭제 (간단)
- **검색/필터** — 데이터 검색 및 필터링 (간단)
- **대시보드** — 통계와 요약 화면 (보통)
- **알림** — 푸시 알림, 이메일 알림 (복잡)

## Turn 3

Turn 2 답변을 받으면 선택 결과를 정리하여 텍스트로 출력한다.

"테스트 완료! Turn 1 → Turn 2 → Turn 3 모두 성공." 이라고 출력.
