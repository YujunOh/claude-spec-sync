---
description: Notion에 표준 기능명세서 템플릿대로 새 페이지를 만든다
argument-hint: <기능 이름> [부모 페이지 URL 또는 ID]
---

너는 PM의 기능명세서 작성을 돕는 어시스턴트다. Notion MCP를 사용해서 아래 템플릿 그대로 새 페이지를 생성한다.

입력: $ARGUMENTS

수행:
1. 첫 번째 인자를 기능 이름으로 사용한다.
2. 두 번째 인자(부모 페이지 URL 또는 ID)가 있으면 그 페이지 하위에, 없으면 사용자에게 어디에 만들지 한 번 묻는다.
3. 아래 구조 그대로 Notion 페이지를 생성한다. heading 레벨과 체크리스트, 테이블을 정확히 재현한다.

---

# Feature: {기능 이름}

## 1. Why
- 무엇을: (한 문장)
- 왜: (이 기능이 없으면 발생하는 문제 / 비즈니스 임팩트)

## 2. User Story
- As a: 
- I want: 
- So that: 

## 3. Scope Boundaries
- ✅ Always: 이 기능에 반드시 포함되는 것
- ⚠️ Ask first: 애매하면 PM에게 확인할 것
- 🚫 Never: 이번 스코프에 절대 들어가지 않는 것 (positive로 명시)

## 4. States
| State | 트리거 | UI 설명 | 와프 프레임 ID |
| --- | --- | --- | --- |
| empty | | | |
| loading | | | |
| success | | | |
| error | | | |
| disabled | | | |
| edge-case-1 | | | |

## 5. Priority
- P0 (출시 차단): 
- P1 (출시 후 1주 내): 
- P2 (백로그): 

## 6. Acceptance Criteria
- [ ] Given … When … Then …
- [ ] Given … When … Then …
- [ ] Given … When … Then …

## 7. Open Questions
- (사람이 결정해야 하는 것만 남긴다)

## 8. Linked Wireframe
- Figma URL:
- Frame node IDs:
- 마지막 동기화: 

---

생성 후:
- 만든 페이지 URL을 보고한다.
- 사용자가 채워야 할 빈 칸이 어디인지 짧게 정리한다.
- 추측으로 채우지 않는다. 모르면 비워둔다.
