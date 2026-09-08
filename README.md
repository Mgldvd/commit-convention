# commit-convention

A structured, cross-project variant of [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/)
for Claude Code: the same grammar and type vocabulary as the spec, plus a fixed monochrome shape
marker per type, a column-aligned colon, and a shared scope vocabulary — so commit history reads
the same way in every project that adopts it.

See [`SKILL.md`](SKILL.md) for the full format and [`reference/scopes.md`](reference/scopes.md)
for the scope vocabulary.

## Install

Clone (or add as a submodule) into a project's `.claude/skills/`:

```sh
git clone git@github.com:Mgldvd/commit-convention.git .claude/skills/commit-convention
```

## Shape per type

| Shape | Types                     | Meaning                                                            |
| ----- | ------------------------- | ------------------------------------------------------------------ |
| `●`   | `fix`                     | Bug fix                                                            |
| `△`   | `perf`                    | Performance improvement                                            |
| `◆`   | `refactor`                | Structural change, behavior intentionally unchanged                |
| `▲`   | `feat`                    | New user-visible capability                                        |
| `□`   | `docs`                    | Documentation-only change                                          |
| `◇`   | `style`                   | Formatting-only, no behavior change                                |
| `■`   | `build`, `ci`             | Build system, dependencies, or CI/CD config                        |
| `○`   | `chore`, `test`, `revert` | Repository maintenance, test-only change, or reverting a commit    |

## Scope vocabulary

Max 8 characters each, English only — see [`reference/scopes.md`](reference/scopes.md) for the
full rules on adding a new one.

| Area            | Scopes                                                          |
| --------------- | --------------------------------------------------------------- |
| UI / Frontend   | `ui`, `layout`, `theme`, `a11y`, `forms`, `nav`, `icons`        |
| Backend / API   | `api`, `backend`, `server`, `router`, `endpoint`, `handler`, `discover` |
| Data / Storage  | `db`, `schema`, `cache`, `storage`, `migrate`, `query`, `model` |
| Auth / Security | `auth`, `security`, `perms`, `session`, `token`, `oauth`        |
| CLI / Tooling   | `cli`, `cmd`, `script`, `tooling`                               |
| Infra / Deploy  | `infra`, `deploy`, `docker`, `network`, `ci`, `cdn`, `dns`      |
| Config          | `config`, `env`, `flags`                                        |
| Dependencies    | `deps`                                                          |
| Docs            | `docs`, `readme`, `changes`                                     |
| Tests           | `tests`, `e2e`, `mock`                                          |
| i18n            | `i18n`, `locale`                                                |
| Observability   | `logs`, `metrics`, `tracing`, `alerts`                          |
| State           | `state`, `store`                                                |
| Build / Release | `build`, `release`, `bundler`, `package`                        |
| Messaging       | `queue`, `events`, `pubsub`                                     |
| Notifications   | `notif`, `email`, `push`                                        |
| Search          | `search`, `index`                                               |
| Media           | `media`, `upload`, `image`                                      |
| Networking      | `http`, `ws`, `grpc`                                            |
| Mobile          | `mobile`, `ios`, `android`                                      |
| Payments        | `billing`, `payment`                                            |

## Example, one per scope area

```text
feat(ui)...........: ▲ - add a collapsible sidebar
feat(api)..........: ▲ - add a bulk-export endpoint
fix(db)............: ● - fix a stale index after migration
fix(auth)..........: ● - reject an expired refresh token
build(cli).........: ■ - add a --dry-run flag to the build script
build(infra).......: ■ - pin the base image to a digest
chore(config)......: ○ - move secrets out of the default config
chore(deps)........: ○ - bump the lockfile to the latest patch
docs(readme).......: □ - document the release process
test(tests)........: ○ - add coverage for the retry queue
chore(i18n)........: ○ - add missing pt-BR strings
fix(logs)..........: ● - stop logging the raw auth header
refactor(state)!...: ◆ - replace the global store with a reducer
perf(build)........: △ - cache the bundler's dependency graph
feat(queue)........: ▲ - retry failed jobs with backoff
feat(notif)........: ▲ - add push notifications for mentions
perf(search).......: △ - add an index for full-text search
fix(media).........: ● - fix an upload timeout on large images
fix(http)..........: ● - close idle keep-alive connections
build(mobile)......: ■ - enable the ios release profile
feat(billing)......: ▲ - support partial refunds
```
