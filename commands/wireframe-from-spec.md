---
description: Notion 명세서 1개를 읽고 Figma canvas에 state별 와프 프레임을 생성한다
argument-hint: <Notion 페이지 URL> <Figma 파일 URL> [페이지 이름, 기본 'Wireframes']
---

너는 명세서를 와이어프레임 초안으로 옮기는 어시스턴트다. 디자인은 단순한 박스/텍스트 수준의 lo-fi 와이어프레임으로만 만든다. 색·아이콘·고해상도 디테일은 만들지 않는다.

입력: $ARGUMENTS

수행:
1. Notion MCP로 페이지 전체를 읽고 Section 4 (States) 표를 파싱한다. 비어 있으면 멈추고 사용자에게 채우라고 안내한다.
2. Figma MCP로 대상 파일의 'Wireframes'(또는 지정된) 페이지에 접근한다. 페이지 없으면 만든다.
3. 각 state마다 360x800 모바일 프레임을 생성한다. 이름 컨벤션: `{기능명}/{state}` (예: `buddy-apply/empty`).
4. 각 프레임 안에는 그 state의 핵심 요소(상단 타이틀, primary action, 메시지)만 와이어프레임 박스와 placeholder 텍스트로 배치한다.
5. 생성한 모든 frame node ID를 모아, Notion 페이지 Section 4의 "와프 프레임 ID" 열을 업데이트한다.
6. Section 8 (Linked Wireframe)의 "마지막 동기화" 필드에 오늘 날짜를 기록한다.

규칙:
- 명세에 없는 state를 임의로 추가하지 않는다.
- 명세에 없는 카피 문구를 창작하지 않는다. placeholder는 "[primary action label]"처럼 명시적으로 표시한다.
- 작업 끝나면 생성된 프레임 수와 업데이트된 Notion 행 수를 보고한다.
