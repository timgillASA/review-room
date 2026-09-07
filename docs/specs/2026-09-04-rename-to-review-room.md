# Rename: claude-bridge -> review-room

**Status: proposed 2026-09-04, not executed.** Companion to the rename plan;
this holds the detail so the plan can stay short.

## Why

Both halves of the name are now wrong. "Claude" is false in two directions: a
Codex seat has joined a run, and a Claude-only user on one machine should use
native messaging instead. "Bridge" names the transport, which the 1.0 review
called commodity and which now has three shapes (watch, ping, and a git
transport in test). It also sits in a crowd: `michalekz/claude-bridge` (same
name, same category), `msanchezdev/agent-bridge`, `PatilShreyas/claude-code-
session-bridge` (also `/bridge`), and two `claude-bridge` API proxies. Every
one of them is chat. The word that separates this repo from all of them is
"review". See `docs/2026-09-04-prior-art.md`.

`timgillASA/review-room` is free (checked 2026-09-04). Six unrelated repos
elsewhere use the bare name, none in this space, top one at one star.

## Vocabulary map

| Old | New | Where |
|---|---|---|
| repo `claude-bridge` | `review-room` | GitHub (`gh repo rename`, old URL redirects), both manifests, README install lines |
| plugin + marketplace name `claude-bridge` | `review-room` | `plugin.json`, `marketplace.json`; install becomes `review-room@review-room` |
| `commands/bridge.md`, `/bridge` | `commands/room.md`, `/room` | the file, README, CLAUDE.md, CONTRIBUTING, PR template; namespaced form `/review-room:room` |
| "bridge" as the noun for one conversation | "room" (already used informally throughout) | command, README, protocol.md |
| "bridge file", "ping bridge", "watch bridge" | "room file", "ping room", "watch room" | same |
| `BRIDGE_DIR` | `ROOM_DIR` | command |
| `~/.claude/bridge-dir.txt` | `~/.claude/room-dir.txt`, and if absent read `bridge-dir.txt` (one line; three configured machines) | command, README |
| first-run proposal `<drive>:\ClaudeBridge` | `<drive>:\ReviewRooms` | command; README example paths follow |
| `bridge-ping:` | `room-ping:` | command (ping text) |
| `# Bridge: <topic>` header | `# Room: <topic>` | README example only; nothing parses the H1 |
| `.STOP` marker | unchanged | |
| entry header format | unchanged | |
| version | 0.17.0 | the install string changes, so this is the breaking bump |

## What is deliberately NOT rewritten

- The three dated docs under `docs/` (2026-08-19 x2, 2026-08-23) are frozen
  records and keep the old word. `protocol.md` gets one sentence in its intro:
  before 0.17 the project was `claude-bridge` and a room was called a bridge;
  older documents keep that word.
- The entry format, the STOP marker, the ping mechanics, every rule. This is a
  vocabulary change with zero protocol change, and the diff should read that way.
- Existing room directories on configured machines: the path lives in the
  per-machine text file, so `D:\ClaudeBridge` keeps working unrenamed.

## Order of operations

1. Local edits (vocabulary map above), `git mv commands/bridge.md
   commands/room.md`, protocol.md intro sentence, README gets a one-line
   "formerly claude-bridge" under the title for arrivals via the old link.
2. Commit as 0.17.0, push.
3. `gh repo rename review-room` -- GitHub redirects the old URL for git and
   web; the local remote is updated by `gh` automatically.
4. On this machine: uninstall `claude-bridge@claude-bridge`, remove the old
   marketplace, add `timgillASA/review-room`, install `review-room@review-room`.
   Restart the session; `/room` should resolve. Other machines repeat step 4.
5. After this session ends, the user renames `D:\claude-bridge` to
   `D:\review-room` and moves the project memory directory
   (`~/.claude/projects/D--claude-bridge` -> `D--review-room`) so memory
   follows the folder. Not done from inside a session rooted in the folder.
6. Tell the two peer sessions the new name so their notes stop pointing at
   the old one. Tag `v0.17.0` with a release note that says "formerly
   claude-bridge".

## Collapse test

Two situations the rename cannot tell apart: a machine with a stale
`bridge-dir.txt` and a machine that has never run the command. The fallback
read closes it -- the stale file is honoured, the fresh machine gets the
first-run prompt -- and it fails loud in the remaining case (both files
present, disagreeing) only if the command says which wins: `room-dir.txt`.
