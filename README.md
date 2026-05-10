# claude-spec-sync

Bidirectional **Notion ↔ Figma** spec/wireframe sync for Claude Code.

A small Claude Code plugin that ships four slash commands wrapping the official
[Notion MCP](https://developers.notion.com/guides/mcp/get-started-with-mcp) and
[Figma MCP](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Figma-MCP-server)
servers — so a PM can keep a functional spec in Notion and wireframes in Figma
in sync without exporting PNGs/CSVs to a chat tool.

## What it does

| Command | Direction | Use it when |
| --- | --- | --- |
| `/spec-new <name> [parent]` | — | You want a fresh PRD page in Notion using a standardized template (Why / Story / Boundaries / States / Priority / Acceptance / Open Q / Linked Wireframe). |
| `/spec-audit <notion> <figma>` | Notion ⇆ Figma | You want to know which states/criteria exist in one side but not the other. Reports diffs only — never auto-edits. |
| `/wireframe-from-spec <notion> <figma> [page]` | Notion → Figma | You have a filled-in spec and want lo-fi wireframe frames per state, written directly to the Figma canvas. Frame node IDs are written back into the spec's States table. |
| `/spec-from-wireframe <figma> [parent]` | Figma → Notion | You have wireframes already and want a Notion spec draft reverse-engineered from them. Inferred items are tagged `(추정)`; decisions land in Open Questions. |

## Why this template

Built around three rules that keep AI agents predictable on spec work:

1. **Boundaries stated positively** — `✅ Always / ⚠️ Ask first / 🚫 Never`. AI agents tend to "helpfully" add scope unless you forbid it explicitly.
2. **States table is mandatory** — `empty / loading / success / error / disabled` plus edge cases. Missing states are the #1 cause of spec/wireframe drift.
3. **Living document** — every command can write back to Notion (frame IDs, sync timestamp, audit comments) so the spec is never frozen.

References: [GitHub Spec Kit](https://github.com/github/spec-kit), [Addy Osmani — How to write a good spec for AI agents](https://addyosmani.com/blog/good-spec/), [ChatPRD — How Notion designs with AI](https://www.chatprd.ai/how-i-ai/how-notion-designs-with-ai-brian-lovins-prototype-playground-and-claude-code-workflows).

## Install

### Prerequisites

Install and authenticate the two MCP servers this plugin drives:

```bash
claude mcp add --transport http notion https://mcp.notion.com/mcp
claude plugin marketplace add anthropics/claude-plugins-official
claude plugin install figma@claude-plugins-official
```

Restart Claude Code, run `/mcp`, and complete OAuth for both `notion` and `plugin:figma:figma`. The Figma plugin auto-registers a remote MCP that works on every Figma plan (free included). The desktop MCP at `127.0.0.1:3845` is optional and requires a paid Figma seat.

### Install this plugin

```bash
claude plugin marketplace add YujunOh/claude-spec-sync
claude plugin install spec-sync@claude-spec-sync
```

The four commands appear under `/spec-new`, `/spec-audit`, `/wireframe-from-spec`, `/spec-from-wireframe`.

### Or copy the commands manually

```bash
git clone https://github.com/YujunOh/claude-spec-sync
cp claude-spec-sync/commands/*.md ~/.claude/commands/
```

## Spec template (what `/spec-new` writes to Notion)

```
# Feature: <name>

## 1. Why
- 무엇을: (한 문장)
- 왜: (이 기능이 없으면 발생하는 문제 / 비즈니스 임팩트)

## 2. User Story
- As a / I want / So that

## 3. Scope Boundaries
- ✅ Always / ⚠️ Ask first / 🚫 Never

## 4. States                       ← required
| State       | 트리거 | UI 설명 | 와프 프레임 ID |
| empty / loading / success / error / disabled / edge cases |

## 5. Priority
- P0 (출시 차단) / P1 (출시 후 1주) / P2 (백로그)

## 6. Acceptance Criteria
- Given / When / Then  (3~5개)

## 7. Open Questions

## 8. Linked Wireframe
- Figma URL / Frame node IDs / 마지막 동기화
```

## Workflow

```
       ┌──────────────────┐                  ┌──────────────────┐
       │  Notion (spec)   │ ◀── /spec-audit ─▶│  Figma (wires)  │
       │                  │                   │                  │
       │  /spec-new       │ ── /wireframe-from-spec ──▶          │
       │                  │ ◀── /spec-from-wireframe ──          │
       └──────────────────┘                  └──────────────────┘
```

- **Greenfield**: `/spec-new` → fill it in → `/wireframe-from-spec` → review on canvas.
- **Wireframe-first**: `/spec-from-wireframe` → patch Open Questions → `/spec-audit` to verify.
- **Maintenance**: run `/spec-audit` whenever either side changes; let it propose drift fixes, apply them yourself.

## Design choices

- Commands never auto-edit unless explicitly told to. They report diffs and propose actions.
- They never invent acceptance criteria, copy text, or states absent from the source. Inferred fields are tagged `(추정)`.
- Lo-fi only on the wireframe side: 360×800 mobile frames, boxes + placeholder text. Visual design is out of scope.

## License

MIT — see [LICENSE](LICENSE).
