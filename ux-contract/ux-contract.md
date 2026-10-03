# UX Contract — TTW Session Scout

> **Canonical specification**
> Version: `1.1-frozen`
> Freeze date: `2026-10-03`
> This Markdown file is the canonical UX Contract for the workshop.
> `ux-contract.yaml` is retained temporarily as legacy/reference only.

## 0. Identity

- **Workshop:** UX/AI — De la idea al prototipo digital
- **Product:** TTW Session Scout
- **Type:** mobile-first responsive session recommendation microexperience
- **Prototype scope:** educational demo; does not replace the official agenda
- **Event:** Tarija Tech Week 2026
- **Venue:** Campo Ferial San Jacinto, Tarija
- **Default demo day:** 2026-10-02
- **Allowed rooms:** Main Stage, Sala IA, Sala Blockchain

## 1. Product purpose

Help a Tarija Tech Week attendee quickly choose relevant sessions according to interests and available time, using an agenda whose source and version are visible.

## 2. Users

### Primary user — attendee

Context:
- uses a phone while moving between rooms;
- has little time to compare sessions;
- may have unstable connectivity;
- may not know the speakers;
- event timing may slip or change.

Needs:
- choose a useful session without reading the full agenda;
- understand why a session is recommended;
- know which agenda version is being used;
- save an option locally.

### Secondary user — agenda operator

Needs:
- import an updated schedule from `.md` or `.pdf`;
- review changes before applying them;
- detect conflicts and ambiguous data;
- apply operational delay offsets without editing every session manually.

## 3. Jobs To Be Done

### Primary

> When I have a window of time during the event, I want to quickly choose a session relevant to my interests so I can use my time well without reviewing the whole agenda.

Success outcome: reasonable decision in under 30 seconds.

### Secondary

> When the official schedule changes or the event accumulates delays, I want to update the local agenda in a controlled way so the prototype does not recommend stale or invented data.

Success outcome: no imported change alters the active agenda without human review.

## 4. Inputs

Attendee required:
- one or more interests;
- available-from time;
- available duration.

Interests:
- AI
- UX
- Development
- Product
- Business
- Security

Operator optional:
- `.md` schedule file;
- `.pdf` schedule file;
- delay offsets: +5, +10, +15, or custom minutes.

## 5. Outputs

### Recommendation

Return at most 3 recommendations. Each must show:
- title;
- current time;
- room;
- speaker(s);
- a brief explanation of why it matches.

### Schedule import preview

Before applying an update, show:
- added sessions;
- removed sessions;
- changed times;
- changed rooms;
- conflicts;
- ambiguous or unextracted fields;
- detected source/version when available.

## 6. Product constraints

- Mobile-first.
- Responsive across mobile, tablet, and laptop/desktop.
- Maximum 3 main steps from entry to recommendation.
- No login.
- No backend.
- No external API dependency for the primary flow.
- Use only the confirmed active agenda.
- Never invent speakers, sessions, times, rooms, ratings, or descriptions.
- Core functionality must keep working with locally stored active agenda data.

## 7. Responsive behavior

TTW Session Scout is one responsive product, not three separate products.

### Mobile

Reference width: **375 px**.
- Base layout.
- One-column flow by default.
- Full feature set available.
- Touch targets must be usable.
- No action may require hover.

### Tablet

Reference width: **768 px**.
- May use two columns when that improves comprehension.
- Must preserve the same essential capabilities as mobile.
- Touch interaction must remain usable.

### Laptop / Desktop

Reference width: **1280 px**.
- May use additional horizontal space for filters and results.
- Must not change the product logic.
- Entire flow must remain keyboard-usable.

### Common responsive rules

- No unexpected horizontal overflow.
- No critical content clipped.
- No viewport-exclusive essential feature.
- No hover-only action.
- Same data model, recommendation logic, and schedule rules at all sizes.

## 8. UX constraints

- One clear primary action per screen/state.
- No dark UX patterns.
- No dead ends.
- If no matches exist, provide immediate recovery.
- Explain each recommendation briefly.
- Schedule import must show preview before apply.
- Warnings must not rely on color alone.

## 9. Accessibility

- Keyboard navigable.
- Visible focus.
- Clear labels.
- Adequate touch target size.
- No state communicated by color alone.
- Legible contrast.
- Respect `prefers-reduced-motion`.

## 10. Engineering constraints

- No secrets.
- No telemetry.
- Favorites only in `localStorage`.
- Active agenda and provenance may persist locally for the prototype.
- Offline version must not depend on remote resources.
- Markdown import should be deterministic when structure is recognized.
- PDF import is best-effort and requires human validation.
- `agenda-baseline.json` is never overwritten by import.
- `agenda-current.json` changes only after explicit human confirmation.

## 11. Schedule data model

| Role | File | Rule |
|---|---|---|
| Baseline | `data/agenda-baseline.json` | Immutable snapshot for reference and rollback |
| Current | `data/agenda-current.json` | Only agenda used by the recommendation engine |
| Provenance | `data/provenance.json` | Records source, version, import date, human confirmation, and local adjustments |

Canonical session fields:
- `id`
- `date`
- `start`
- `end`
- `venue`
- `title`
- `speakers`
- `tags`

Allowed venues:
- Main Stage
- Sala IA
- Sala Blockchain

## 12. Schedule ingestion

### Governing principle

> **Parsing does not equal acceptance.**

### Markdown

Preferred mode.

Expected recognizable structure:
- date heading;
- room heading;
- table containing Horario, Tema/Sesión, and Ponentes/Participantes.

Behavior:
- normalize times;
- preserve source text when ambiguous;
- do not infer missing fields.

### PDF

Best-effort mode.

Behavior:
- extract text when possible;
- mark ambiguous data as `UNKNOWN`;
- never auto-apply changes.

Perfect extraction from arbitrary PDFs is explicitly not guaranteed.

### Diff

Required change types:
- `added`
- `removed`
- `time_changed`
- `venue_changed`
- `speaker_changed`
- `ambiguous`

### Conflict detection

Must detect at least:
- `end <= start`;
- room outside allowed venues;
- overlapping sessions in the same date and room;
- possible duplicates;
- missing required fields.

### Human confirmation

Human confirmation is mandatory.

> No import modifies `agenda-current.json` before explicit confirmation.

### Delay adjustment

Support +5, +10, +15, or custom minutes for a selected range of sessions.

The adjustment:
- must remain visible as a local change;
- must not alter baseline;
- must affect the active agenda;
- must be recorded in provenance.

## 13. States

### Attendee

| State | Required | Recovery / behavior |
|---|---:|---|
| `default` | Yes | Initial state |
| `configured` | Yes | Interests/time configured |
| `results` | Yes | Recommendations shown |
| `no_results` | Yes | Change interests, expand time, or view all sessions |
| `saved` | Yes | Session saved locally |
| `offline` | Yes | Core flow works from local `agenda-current` |

### Operator

| State | Required | Recovery / behavior |
|---|---:|---|
| `schedule_import` | Yes | Select file |
| `schedule_parsing` | Yes | Extract / normalize |
| `schedule_preview` | Yes | Preview + diff |
| `schedule_conflicts` | Yes | Show conflicts / ambiguity |
| `schedule_confirmed` | Yes | Update confirmed |
| `schedule_import_error` | Yes | Keep current agenda unchanged; retry/cancel |

## 14. Recommendation logic

Prioritize:
1. thematic match;
2. sessions that fit the available time window.

Never infer:
- popularity;
- speaker quality;
- reputation;
- ratings;
- undeclared preferences.

The recommendation engine uses **only `agenda-current.json`**.

Each recommendation requires a short explanation, e.g.:

> “Coincide con AI + Development y comienza dentro de tu ventana.”

## 15. Success metrics

| ID | Metric | Target |
|---|---|---|
| `SM-01` | `time_to_recommendation` | <= 30 seconds in moderated test |
| `SM-02` | `steps_to_recommendation` | <= 3 main steps |
| `SM-03` | `dead_ends` | 0 |
| `SM-04` | `fabricated_sessions` | 0 |
| `SM-05` | `unconfirmed_schedule_mutations` | 0 |
| `SM-06` | `active_schedule_has_provenance` | 100% |

## 16. Non-goals

The prototype does not aim to:
- create or replace the official agenda;
- guarantee perfect extraction from any PDF;
- predict delays automatically;
- predict which speaker is better;
- use personal profiles or sensitive data;
- provide networking;
- sell tickets;
- sync calendars;
- recommend using unconfirmed data.

## 17. Data provenance

Authoritative source: Tarija Tech Week 2026 official agenda.

Reference snapshot: 02/10/2026.

Supplied source file: `agenda_tarija_tech_week_2026.md`.

Rule:
- show the source/version of the active agenda;
- if local data differs from the official online agenda, the official online agenda takes precedence;
- imported local changes must remain identifiable and require human confirmation.

## 18. Relationship to acceptance tests

This contract defines what must be true about the product.

Executable/verifiable criteria live in:

`evals/acceptance-tests.md`

The contract and acceptance tests must stay aligned.

## 19. Rule for AI agents

An AI using this document must:
1. treat it as a specification, not inspiration;
2. not invent requirements;
3. not expand scope without human authorization;
4. not infer missing schedule data;
5. declare uncertainty when a requirement cannot be guaranteed;
6. use `agenda-current.json` as the only active agenda for recommendations;
7. preserve `agenda-baseline.json` as immutable reference;
8. require human confirmation before changing the active agenda.

## 20. Workshop principle

> **El prompt no es el producto.**

The product is evaluated against:
1. an explicit problem;
2. this UX Contract;
3. controlled data;
4. acceptance tests;
5. Red Team evidence.

```text
PROBLEM
   ↓
UX CONTRACT
   ↓
BUILD
   ↓
RED TEAM
   ↓
CONTROLLED ITERATION
```

Schedule update flow:

```text
.md / .pdf
   ↓
parse / extract
   ↓
normalize
   ↓
diff + conflict detection
   ↓
human preview
   ↓
explicit confirmation
   ↓
agenda-current
```

**Central rule:** parsing does not equal acceptance.
