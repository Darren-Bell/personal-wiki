# Agent Instructions — Darren's Portent Vault

This is a Portent knowledge base. Use these rules to read, create, and maintain notes.

## Core Rules

- Model reality first. Do not use folders as the main source of meaning.
- Every durable object should answer: what is this?
- Every organized object should answer: what will this be useful for?
- Prefer Portent defaults before creating custom types or relationships.
- Keep captured material easy to record, then organize it later.
- Keep archived material searchable, but hidden from active work by default.

## Object Shape

Every note is a Markdown file with YAML frontmatter at the vault root.

Required frontmatter:

```yaml
---
type: <one of the 8 Portent types>
_organized: true   # or omit if still captured/inbox
---
```

Title comes from the first `# H1` heading in the body. Filename is a slug of the title.

## Types

### PORT (actionable)

| Type | Definition | Use When |
|------|-----------|----------|
| **Project** | Bounded effort, has start/end, produces output | Work that can't be done in one sitting but has a clear finish |
| **Operation** | Recurring work, completable in one sitting | Repeatable routines, checklists, maintenance |
| **Responsibility** | Long-running area of accountability, no end date | Outcomes measured by KPIs or standards |
| **Task** | One-off work, completable in one sitting | Prefer external task manager (Todoist, etc.) |

### ENTP (context)

| Type | Definition | Use When |
|------|-----------|----------|
| **Event** | Something that happened, date-anchored | Meetings, decisions, achievements, milestones |
| **Note** | Durable knowledge artifact | Documents, resources, references, checklists |
| **Topic** | Area of interest, no action expectation | Concepts, domains, areas of curiosity |
| **Person** | Real person or AI agent | Contacts, collaborators, stakeholders |

## Relationships

Use only two default relationships:

- **`belongs_to`** — strong ownership, composition. Usually one parent.
  - Operation → Responsibility
  - Project → Responsibility
  - Event → Project
  - Task → Project

- **`related_to`** — loose association, many-to-many.
  - Note → Topic
  - Event → Person
  - Project → Topic

```yaml
belongs_to: "[[stay-organized]]"
related_to:
  - "[[manage-email]]"
  - "[[darren]]"
```

## Lifecycle

Three states. Represent with `_organized` and `archived` frontmatter fields:

| State | Meaning | Frontmatter |
|-------|---------|-------------|
| **Captured** | Recorded but not yet structured. Needs triage. | (no `_organized` field) |
| **Organized** | Has type, title, relationships. Ready for use. | `_organized: true` |
| **Archived** | No longer active but kept as memory. | `archived: true` |

**Capture optimistically.** Save first, decide later.
**Organize pessimistically.** If you can't attach it to anything, consider deleting.

## Inbox

Notes without `_organized: true` are in the inbox. Goal: process inbox regularly.

When organizing a note:
1. Give it a clear title (first `# H1`)
2. Assign a `type`
3. Add `belongs_to` and/or `related_to` relationships
4. Set `_organized: true`

## Creating Notes

When creating a new note:

1. Choose a descriptive slug filename: `my-note-title.md`
2. Add YAML frontmatter with at least `type:`
3. Start body with `# Title`
4. Add relationships if the note connects to existing objects
5. Set `_organized: true` if the note is ready; omit if it needs further triage

```yaml
---
type: Note
belongs_to: "[[some-project]]"
related_to:
  - "[[some-topic]]"
_organized: true
---
# My Note Title

Content here.
```

## Extension Rules

- Add a custom type only when the object needs different behavior, templates, or workflows
- Use properties (e.g., `Kind:`, `Status:`, `Cadence:`) before creating new root types
- Add custom relationships only when `belongs_to`/`related_to` hides important meaning

## Vault Conventions

- All notes live at the vault root (flat structure, no subdirectories)
- Type definitions are in type documents (e.g., `project.md`, `operation.md`)
- Attachments go in `attachments/`
- Use `[[wikilinks]]` to reference other notes in body text
- Filename = slug of title, lowercase, hyphens for spaces

## Owner Context

- **Darren** — GMT+1, Europe/London
- Prefers Telegram for communication
- Needs persistent reminders
- Tends to miss appointments — calendar management is critical
- Wants proactive email management across multiple accounts
- Work domains: nanthealth, optiva, qvantel, centric, myworkday
