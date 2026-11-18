# Codex research and evidence

[Back to the OUTLANDS profile](../README.md#codex-research)

This record keeps the detailed findings and the dated maintainer observations behind the profile highlights. The linked issues contain the public evidence and subsequent discussion.

## OpenAI repository contributions

- [Codex Action run manifest (PR #194)](https://github.com/openai/codex-action/pull/194): submitted an optional, machine-readable manifest for a Codex Action run. The PR is open for review. The fork's four Linux CI jobs passed; the candidate has not been tested in a GitHub-hosted composite Action job or on macOS or Windows.
- [Codex Security compatibility proxy review (PR #2707)](https://github.com/openai/codex-security/pull/2707#issuecomment-6968962697): reproduced a custom-tool streaming failure in the proposed patch with a synthetic local Responses endpoint. The [PR author confirmed and fixed it](https://github.com/openai/codex-security/pull/2707#issuecomment-6971394981); my original synthetic fixture passed against the updated files, as did the focused Bun suite (16/16). The PR remains open; I did not test a live provider or a released build.
- [Codex Security Deep Scan review (PR #2710)](https://github.com/openai/codex-security/pull/2710#issuecomment-6969692290): identified a local-versus-persisted terminal-state mismatch when a parent-turn refusal arrives after finish commits. The [PR author confirmed and patched it](https://github.com/openai/codex-security/pull/2710#issuecomment-6972522659). A synthetic real-Workbench check established the persistence rule, and focused local coordinator/error tests with the updated PR files passed 138/138. The PR remains open; Desktop timing and a full real-store coordinator race remain unverified.
- [Codex Security ArmorCode import review (PR #2728)](https://github.com/openai/codex-security/pull/2728#issuecomment-6994142981): an exact PR-head, three-row synthetic importer test found that a nonempty array of unusable locations suppresses a valid `filePath` fallback. The finding remains included; full CLI import and security impact were not tested.
- [Codex Action usage telemetry contract (#178)](https://github.com/openai/codex-action/issues/178#issuecomment-6968258571): asked whether a validated usage-only output would meet the issue's requirements before proposing code that could expose raw JSONL content. This is a design question; no patch or security finding was submitted.

## Investigations

I independently investigate Codex reliability and security behavior using source review and isolated, synthetic tests. My public issue work includes:

- [Git-backed plugin refresh latency (#58885)](https://github.com/openai/codex/issues/58885): measured the delay and compared a local Linux candidate fix with unpatched current main.
- [Loaded-thread MCP endpoint retention (#58060)](https://github.com/openai/codex/issues/58060): reproduced stale and missing `codex_tui` registrations in offline Codex 0.167.0 tests, with explicit recovery limits.
- [CLA workflow pagination (#58461)](https://github.com/openai/codex/issues/58461): documented contributors missed beyond the first 100 PR commits and shared tested reference-fix guidance.
- [Plugin refresh cleanup (#55068)](https://github.com/openai/codex/issues/55068): added independent reproductions for duplicate refresh work and app-server shutdown behavior.
- [Loaded-thread sandbox override (#59730)](https://github.com/openai/codex/issues/59730): reproduced on Codex 0.167.0 that a same-server resume ignores an override while a fresh-server resume applies it; no sandbox bypass was demonstrated.
- [AgentPlugin hook loading (#59516)](https://github.com/openai/codex/issues/59516): reproduced missing declared hooks and tested a local candidate fix through synthetic installation, discovery, and hook execution.
- [Marketplace removal visibility (#59689)](https://github.com/openai/codex/issues/59689): reproduced a plugin disappearing from the list while its synthetic skill remained active, and tested recovery and an install/removal race in a local candidate fix.
- **Thread and command lifecycle:** [cold pagination (#60529)](https://github.com/openai/codex/issues/60529#issuecomment-6779929404): tested tied-timestamp and partial-index cases; [missing app-server command events (#60470)](https://github.com/openai/codex/issues/60470#issuecomment-6784343061): reproduced model-visible output without command notifications on official Linux 0.167.1.
- **CLI input and startup cleanup:** [comma-named image paths (#60587)](https://github.com/openai/codex/issues/60587#issuecomment-6784707188): confirmed an existing PNG was omitted while Codex exited 0; [Git temporary directories (#60615)](https://github.com/openai/codex/issues/60615#issuecomment-6785215617): confirmed one survived SIGTERM and a successful restart. Both used network-disabled synthetic Linux controls.
- **Review and marketplace configuration:** [branch/tag review base (#60919)](https://github.com/openai/codex/issues/60919#issuecomment-6811094704): `--base main` selected a same-named tag; [inline marketplace entries (#60940)](https://github.com/openai/codex/issues/60940#issuecomment-6811088519): adding one marketplace removed another configuration entry. Both were reproduced on official Linux 0.167.1 with synthetic controls, and private candidate fixes were tested locally. No security impact was demonstrated.
- **CLI configuration:** [local marketplace `#` paths (#60896)](https://github.com/openai/codex/issues/60896#issuecomment-6811318196): an explicit local path registered its sibling; [MCP same-name re-add (#60927)](https://github.com/openai/codex/issues/60927#issuecomment-6811437468): a repeat add removed `enabled = false` and two timeouts. Both reproduced on official Linux 0.167.1 with isolated synthetic configuration; a private candidate fix was tested for #60896 only. No security impact was demonstrated.
- **File-search API reliability:** [Unicode highlight offsets (#60588)](https://github.com/openai/codex/issues/60588#issuecomment-6785662704): incorrect indices after combining marks and ZWJ emoji; [overlapping-root duplicates (#60591)](https://github.com/openai/codex/issues/60591#issuecomment-6785874541): 50 result rows held only 25 distinct files and omitted five valid matches. Both used synthetic files with official Linux 0.167.1 app-server; GUI rendering and session-based search were not tested.
- **Thread search:** [Greek final sigma occurrences (#60589)](https://github.com/openai/codex/issues/60589#issuecomment-6787044063): reproduced an exact-substring miss through the official Linux 0.167.1 app-server with synthetic text and tested a private candidate fix locally.
- **Additional CLI/MCP reliability checks:** [oversized MCP replies (#60383)](https://github.com/openai/codex/issues/60383#issuecomment-6756989945), [headless elicitation reporting (#60400)](https://github.com/openai/codex/issues/60400#issuecomment-6766198171), and [installer PATH quoting (#60494)](https://github.com/openai/codex/issues/60494#issuecomment-6757620856), each reproduced with synthetic local controls and stated limits.
- **Remote compaction diagnostics:** [proxy-dropped trigger context (#62177)](https://github.com/openai/codex/issues/62177#issuecomment-6981024676): an official Linux 0.168.0 synthetic relay reproduced the count-only failure; a private candidate added type-only context and a hint in focused Rust and app-server checks. This experimental-path diagnostic is not a bounty finding, and no live provider or Desktop run was tested.

- **TUI prompt rendering:** [shell-prompt tildes (#62296)](https://github.com/openai/codex/issues/62296#issuecomment-6992608280): reproduced the typed-message styling bug in a pinned current-main component test. A private candidate passed synthetic transcript, mixed Markdown, link, and copy controls; I did not independently validate the released Linux TUI.

- **TUI math design:** [underbrace annotations (#61792)](https://github.com/openai/codex/issues/61792#issuecomment-6936878768): a focused offline renderer test confirmed the missing display path in a local checkout; I proposed a bounded terminal layout. Released TUI behavior and a fix remain untested.

**Maintainer issue status recorded November 17, 2026.** Release status is tracked separately.

| Issue | What the research covered | Status |
| --- | --- | --- |
| [#60494](https://github.com/openai/codex/issues/60494) | A literal `$` in the install directory broke the generated shell-profile PATH. | Closed, `completed`; maintainer said an upcoming release would address it. |
| [#60589](https://github.com/openai/codex/issues/60589) | Thread occurrence search missed a Greek final-sigma substring. | Closed, `completed`; maintainer said an upcoming release would address it. |
| [#60591](https://github.com/openai/codex/issues/60591) | Overlapping file-search roots produced duplicate results and displaced valid matches. | Closed, `completed`. |
| [#60615](https://github.com/openai/codex/issues/60615) | Terminating app-server during startup left temporary Git directories behind. | Closed, `completed`. |
| [#60529](https://github.com/openai/codex/issues/60529) | Cold descending thread pagination skipped synthetic rollouts sharing a file timestamp. | **Current status unknown:** our November 12 check recorded `closed/completed`, but the issue now returns 404, so I cannot verify its present state or why it is unavailable. |
| [#61271](https://github.com/openai/codex/issues/61271) | A failed `codex exec -o` run left an empty output file. | Closed, `not_planned`; a maintainer said early file binding is intentional. |

I document what each test proves and route validated security vulnerabilities through [OpenAI's private Bugcrowd program](https://bugcrowd.com/engagements/openai).
