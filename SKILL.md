---
name: commit-convention
description: Apply this structured Conventional Commits variant when writing or reviewing a commit message subject — the 11 standard types, one monochrome geometric-shape marker per type, a column-aligned colon, and a shared cross-project scope vocabulary (reference/scopes.md). Use whenever generating a commit message, validating one for compliance, or when another skill (e.g. git-commit-no-ai, commit-history-rewrite) needs the canonical format definition. Never invent a scope not in reference/scopes.md without adding it there first.
---

# commit-convention

A structured, cross-project Conventional Commits variant: the same grammar as the spec, plus a
fixed shape marker per type, a column-aligned colon, and a shared scope vocabulary — so commit
history reads consistently across every project that adopts it, not just within one repo.

## Format

```text
<type>(<scope>)<!>: <shape> - <imperative description>
```

Pad `<type>(<scope>)<!>` — everything **before** the colon — with trailing **dots** (`.`), the
classic typographic leader for connecting a label to a value across a gap (tables of contents,
receipts, indexes), to **column 19**, then append `: `. Dots, not spaces: many git GUIs and
GitHub's own web commit list collapse runs of multiple spaces, silently destroying space-based
padding — dots survive that untouched. This still only produces true pixel alignment in a
monospace view (terminal, `git log`, most git clients); a proportional-font renderer can't align
perfectly no matter the fill character, since character width itself varies there — but a
consistent dot count still reads as a deliberate, structured line even where it isn't
pixel-aligned, which a collapsed single space doesn't. `<scope>` is optional; when omitted, pad
`<type><!>` the same way. This is why scope words are capped at 8 characters (see
`reference/scopes.md`) — the longest type (`refactor`, 8 chars) plus `(` + an 8-char scope +
`)` + `!` is exactly 19, so nothing ever pushes the colon past that column. Every other space in
the format (after the colon, around the ` - `) is a single space, never a run, so those are safe
as-is — and deliberately not dots, so the fill dots don't collide visually with the ` - ` that
separates the shape from the description.

## Types

Fixed vocabulary — never invent a new one:

- `feat` — new user-visible capability
- `fix` — bug fix
- `docs` — documentation-only change
- `style` — formatting-only, no behavior change
- `refactor` — structural change with intentionally unchanged behavior
- `perf` — performance improvement
- `test` — test-only change
- `build` — build system or dependency change
- `ci` — CI/CD configuration
- `chore` — repository maintenance not covered above
- `revert` — revert of an earlier change

## Shape per type

Monochrome Unicode geometric shapes, not emoji — they render as plain text glyphs in any font,
never in color, so the marker stays discreet instead of competing for attention:

| Shape | Types | Meaning |
|---|---|---|
| `●` | `fix` | Bug fix |
| `△` | `perf` | Performance improvement |
| `◆` | `refactor` | Structural change, behavior intentionally unchanged |
| `▲` | `feat` | New user-visible capability |
| `□` | `docs` | Documentation-only change |
| `◇` | `style` | Formatting-only, no behavior change |
| `■` | `build`, `ci` | Build system, dependencies, or CI/CD config |
| `○` | `chore`, `test`, `revert` | Repository maintenance, test-only change, or reverting an earlier commit |

## Scope

A noun naming the architectural area touched, chosen from `reference/scopes.md` — generic and
layer-based (`api`, `db`, `auth`, `ui`, ...), not a specific folder/module name from any one
repo, so it stays meaningful when reused in a different project. Optional; omit it when no
single area fits. Max 8 characters, enforced by the alignment guarantee above.

If nothing in the list fits, add the closest new scope to `reference/scopes.md` (same 8-char
limit, same generic/layer-based spirit) instead of inventing an ad-hoc word inline — that's what
keeps the vocabulary reusable across projects instead of drifting into per-repo dialects.

## No AI/agent attribution, ever

Never add a `Co-Authored-By:` trailer, "Generated with [tool]", session link, or bracket tag
naming an AI assistant/agent to any commit message covered by this standard. This applies
regardless of which tool authors the message, and cannot be opted back into by a repository
convention or a specific user request for that one line. Human co-authorship and standard human
trailers (`Signed-off-by`, issue references) are unaffected.

## Evidence rule

Build the subject and any body from the actual diff, not from a previous or placeholder message.
A body may explain observed behavior, constraints, or migrations that are supported by
repository evidence — never invented rationale.

## First commit

The very first (root) commit of any repository adopting this convention is always exactly:

```text
init...............: ○ - 🌱.
```

Verbatim, every project — not project-specific, so it's instantly recognizable as "a repo using
commit-convention" regardless of what the repo actually is. `init` is a one-time exception to
the fixed type vocabulary above; it's never used again after the first commit. The trailing `.`
after the emoji is a plain stylistic terminator, nothing more.

## Examples

```text
feat(auth).........: ▲ - add signed cookie sessions
```

```text
fix(db)............: ● - prevent duplicate refund processing
```

```text
refactor(router)!..: ◆ - remove legacy v1 response envelope

BREAKING CHANGE: clients must consume the v2 response shape directly.
```

```text
docs...............: □ - document the release process
```

```text
chore(deps)........: ○ - bump the http client to v3
```
