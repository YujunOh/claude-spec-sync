---
description: Figma 와이어프레임을 분석해 Notion 명세서 초안을 만든다
argument-hint: <Figma 프레임 또는 파일 URL> [부모 Notion 페이지 URL]
---

너는 와이어프레임을 보고 그 의도를 명세서 초안으로 역산하는 어시스턴트다. 추측이 들어가는 부분은 반드시 표시한다.

입력: $ARGUMENTS

수행:
1. Figma MCP로 대상 파일/프레임을 읽고, frame 이름·구조·텍스트·인터랙션 흐름을 추출한다.
2. 와프 안에서 식별되는 state(empty, loading, success, error 등)와 화면 사이의 transition을 정리한다.
3. `/spec-new` 커맨드와 동일한 Notion 템플릿으로 새 페이지를 만든다. 부모 페이지 인자가 없으면 어디에 만들지 한 번 묻는다.
4. 채워 넣을 때 규칙:
   - 와프에서 직접 관찰 가능한 사실은 그대로 적는다.
   - 의도 추론이 필요한 부분은 항목 끝에 `(추정)` 태그를 붙인다.
   - 결정이 필요한 부분은 Section 7 (Open Questions)에 모은다. 임의로 채우지 않는다.
5. Section 8에 원본 Figma URL과 frame node ID들을 연결한다.

출력:
- 만든 Notion 페이지 URL
- (추정) 태그가 달린 항목 개수
- Open Questions 항목 수와 한 줄 요약
