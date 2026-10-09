# Handoff: launch room seats with `--name` -- addresses stop moving

> **INGESTED 2026-10-09, commit `272eb28` (protocol 0.19.0).** Done: `commands/room.md` now tells seats bound for a ping room to launch with `claude --name`, makes a derived-name seat re-check its address after every plan approval, and adds the permission-mode hold to the Transport section; `docs/protocol.md` carries the evidence and corrects the earlier "renames on its own schedule" wording. NOT done: the room does not read `nameSource` or warn on a derived/auto member -- declined, since a prompt-only command should not depend on a per-machine registry file. The README needed nothing: it never claimed cross-account delivery as shipped, only "untested, could work between different people". The cron self-poll wake mechanism is carried into the git-transport spec work, not adopted here. **Anonymized on ingest** per `docs/CONTRIBUTING.md`: the sending seat, the launcher script and a social-media attribution were removed; this repo is public and the originals were never pushed.

From: a sibling bench session, 2026-09-18. For: the review-room seat.

## The insight, compressed

A Claude Code session's auto-generated name is REPLACED the instant its human approves a plan -- synchronously, +0s, three for three measured from transcripts on 2026-09-17 (changelog 2.1.77: "sessions are now auto-named from plan content when you accept a plan"). Not elapsed time, not topic shift. A seat launched with `claude --name <x>` is exempt: controlled pair in one repo, both approved a plan, the derived seat renamed at the instant of approval, the named seat held (registry `nameSource: user`). So a `--name` seat has a permanent address, and the `TRANSPORT: ping` room, which addresses peers by `SendMessage` name, is stable only when its members were launched that way.

## What this means for `commands/room.md` and the README

1. **A ping-transport room is most likely to be live exactly when a plan gets approved** (a room is where multi-seat decisions happen), which is exactly when a derived-name member's address changes out from under the others. Recommend the docs say: seats that will join a ping room are launched with `--name`, and the join/roll-call line records the name so a later rename is visible as a mismatch rather than a silent miss. Whether the room itself should refuse or warn on a `derived`/`auto` member is your call; the registry field is readable at `~/.claude/sessions/<pid>.json` -> `nameSource`.
2. **Documented lookup:** `claude agents --json` prints every live session with `cwd`, `name`, `sessionId`, `status` (scripting surface, no TTY). It does NOT carry `nameSource` (the registry file does) and it does NOT carry the `[ref]` that `ListAgents` shows -- and `SendMessage` REJECTS a `sessionId` as `to` (tested 2026-09-17, self-send: "No agent named ... is reachable"). So name is the only address, which is the whole reason `--name` matters.
3. **Wrong-target sends are still silent** (`success: true`), and delivered is not read: a peer in a different permission-mode class gets the message HELD for its user's approval (documented: `crossSessionInbound` unset = mode parity, bypass<->bypass or prompting<->prompting auto-delivers, mismatch holds). A room whose members mix modes will see pings park. Worth one line in the transport section.
4. A multi-tab launcher on the sending machine now starts every repo tab with `--name <repo>`, so a fleet launched that way is addressable by repo name from the start.

## Two smaller notes for the same seat

- **README claim to check:** a public comment by the user said review-room "can even talk between sessions from different accounts." The user has since said that conflated a transport test with a shipped feature -- the cross-account run was the git-transport proof on a throwaway repo, and the shipped `TRANSPORT:` values are `ping` and `watch` (grepped at 0.18.0). Make sure the README does not say cross-account until a transport actually ships it.
- **A third wake mechanism candidate for the watch fallback**, from `anthropics/claude-code#77932` (a file post-office someone built before SendMessage existed): each seat self-polls its mailbox on idle ticks via a session cron (`*/3 * * * *`, `CronCreate`), so nothing blocks. Their own failure list is the caution: session-scoped crons die silently when the session closes, latency is bounded by the interval, and empty-mailbox polls burn turns. Sits beside the `tail -F`-under-Monitor idea; no recommendation between them yet.

## Reference

`Piebald-AI/claude-code-system-prompts` -- every Claude Code system prompt and tool description, one file per prompt, `ccVersion`-stamped, per-release CHANGELOG. `tool-description-sendmessage.md`, `-cross-session-guidance.md`, `tool-description-listagents.md`, `data-cross-session-inbound-setting.md` are the ones a transport spec should cite instead of quoting the binary.
