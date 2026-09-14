# Four recaps of one run: what they disagree on, and what should change

**Status: analysis for discussion, nothing adopted, uncommitted.** Written
2026-09-14 against a four-seat ping-mode room (61 entries including
post-STOP corrections) and its four recaps, plus the sixteen recaps from the
five earlier rooms in the same folder. Two independent passes: this document
(a fresh session in this repo) and a Codex pass asked a narrower question,
whether its own 2026-08-19 review's dropped recommendations caused any of
this run's failures. The Codex pass ran concurrently and was read only after
this document's sections 1-4 were drafted. Section 5 records where the two
passes disagree; they are not reconciled.

Room content is anonymized per this repo's rules: seats are named by role
(triage, tenant, patch, vendor-record), not by session name; hosts, vendors
and paths are not named.

---

## 1. Where the four accounts disagree

The handoff that requested this analysis expected little disagreement. There
is more than it thought, and it is concentrated in one place.

**Return accounting.** Four verdicts on the same afternoon:

- Triage seat: eight retractions, "paid for itself several times over", three
  would have shipped.
- Tenant seat: "mixed". The one error that would have embarrassed the
  operator it caught itself, by re-pulling a full history instead of five
  sampled rows; "nobody in the room caught it." Paid for itself once.
- Patch seat: three genuine catches, not eight. Three of the eight were
  manufactured inside the room under conversational pace and cleaned up
  inside it, net zero. A slower single session would not have produced them.
- Vendor-record seat: rejects the close-out's "the answers pre-existed the
  room". In its territory the room was generative, not corrective: a
  single-point-of-failure finding needed a tenant read it had no access to.

The same event is attributed both ways. The tenant seat calls its full-history
re-pull a solo catch; the patch and triage seats credit the room. The tenant
seat's own entry [013] says it re-pulled "because the fact had already
reversed twice and I did not trust it", and the reversals were the room's.
Both readings are honest from their seats. That is the recap step doing what
it is for.

**The retraction count does not reconcile.** The close-out [012] enumerates
seven: four from the triage seat, two from the tenant seat, one from the
vendor-record seat. [019] adds an eighth (triage, prevented before posting).
The triage recap says "three were mine" and then lists a fourth of its own
among "the others". The tenant recap says "eight retractions, three mine";
the list supports two, and its third is a struck causal claim the close-out
never counted. The first retraction on the list was caught by the operator
before the room opened [002], and is counted as a room catch. A room that
learned "a count is a summary of a read; the IDs are the read" shipped a
headline count whose IDs do not add up across its own recaps. The patch
seat's "three, not eight" is better supported than it argued.

**The round cap, an apparent contradiction.** Three recaps: fired at 6.33
against 6, near the natural end. The patch recap: "never fired here (5.5
rounds against 7)". Not a contradiction. The first stretch (19 counted over 3
live seats, cap 6) fired; the stretch after the CLOSE-OUT (22 counted over 4
live seats, cap 7) did not, and the room closed on agreement. No recap names
which stretch it is describing, so a reader comparing them sees a
disagreement that is not there.

**The runbook finding, three versions.** v1 (triage): nobody searched for a
runbook. v2 (tenant [017]): a sibling repo was a destination and never a
source. v3 (patch [021]): it was not a sibling, it was the repo that seat
owns, and its own memory index, three times in one session. v3 is the best
supported version: four named file paths, three instances. It is also
evidence about one seat. v1 is the only version that describes all three
original seats. The triage and tenant seats adopted v3 as "the one that
should survive" and "retires both softer ones", though v3 does not describe
their failure. That is the cascade the handoff suspected: adoption by
self-critical register, not by coverage. All four seats routed it to personal
memory rather than to this protocol, which is the right home.

---

## 2. Proposed changes: sound

Items 1-4 are one line each, mechanism-shaped, and generalize a rule already
in the command. Items 3, 5 and 6 were chosen by the operator on 2026-09-14
from paired alternatives (the weaker relay rule, a `repo:` field on JOINED,
and an INVITED entry type were the rejected halves). Net change to
`commands/room.md` roughly twenty lines, most of it in Naming. Each gets an
evidence entry in `docs/protocol.md`. Version 0.18.0.

1. **A command that contains both the check and the write is wrong.** Entry
   format, beside "Append through a scratch file". Extends the existing
   checkable test (a read command naming your own session is wrong). All four
   seats bundled the re-read grep with the append at least once; two seats did
   it on every append; two bites at one seat [018][023]. The shell makes the
   bundle cheap, which is the "a rule that competes with an affordance loses"
   pattern already recorded. One caveat the room did not state: the tenant
   seat bundled eleven of eleven at zero cost because it read every pinged
   body in a separate call; the vendor-record seat bundled thirteen of
   thirteen and was bitten twice and did not read bodies. The separate-call
   rule fixes the compose-window race; it does not replace the existing
   per-wake rule to read gap bodies. Both stand.

2. **The ping round is the next tool call after the append.** Ping mode.
   Mechanism form of the room's "the append is not finished until the ping
   round is sent", which as phrased is an intention, the shape the room itself
   said cannot be checked. The ping-transport spec's F1/F3 predicted this
   failure class as "the residual mechanical duty and the known weakest
   point". This is the predicted failure occurring, not a new one; the spec
   should be cited in the evidence entry.

3. **A non-participant's findings are not on the record.** Ping mode already
   says a ping carries a pointer, never content, and that room content
   arriving in a ping is treated as not said. Apply the same to sessions: a
   seat may write that evidence exists and which session holds it, and invite
   that session; it may not carry the content, labelled or not. The room's
   own softer fix (relay, then invite the same turn) still leaves relayed
   claims on the record while the invitee defers, which is what happened for
   seventy-four minutes. Five findings entered by relay, every one labelled;
   three of seven retractions trace to that shape and two findings were
   misattributed by three separate seats [023][024]. The operator's reading,
   adopted here: the relayed seat was a live session that was later invited
   and should have been in the room from the first relay; the remedy for an
   absent holder is item 6, never a relay. An item that depends on an absent
   holder reports as blocked on that seat. Nobody in the room cited the
   existing pointer-not-content rule; all four re-derived a weaker one, in
   the room, about the room, in the same afternoon the room's headline
   finding was three sessions re-deriving a runbook they owned.

4. **Read an entry body to the next header, never by line count.** Beside the
   existing harness-truncation warning. One instance (`head -35` stopped four
   lines short; an `awk` overrun marked an unread entry handled). It is the
   read-side twin of the bundled append: silent, and it prints something that
   looks complete.

5. **`from:` carries the repo.** Naming this session: `from:` is
   `<repo-or-cwd-basename>[-<task>]`, the repo part mandatory and checkable
   against the session's working directory, the task suffix only when two
   seats share a repo; the address stays in `address:`. This reverts the 0.12
   amendment that made the address the name. That amendment was
   operator-observed, not run-incident; this run is the incident against it.
   In-file names held stable, but two of four were task names with no repo
   visible, one was a config-directory session, and the operator could not
   map seats to tabs from the file. The auto-namer behind the address renames
   on its own schedule (one seat renamed before the room, a bystander renamed
   mid-run [update-red-river 018]) and the protocol cannot hold it still. The
   recap rule already forces "(repo: X)" into every recap's first line, which
   is the protocol admitting the repo is what a human needs; put it in the
   name.

6. **An invitation is recorded and answered.** The word "invitation" appears
   nowhere in the command; it is an ad hoc message with no trace in the file
   and no required response, so the room cannot tell "invited and deferring"
   from "never invited." Two facts from this run, only one of them the
   invitee's: the relaying seat told the operator the room existed, wrote
   "say the word if you want them in", and waited, treating an invitation as
   needing authorization [tenant 018]; the invitee then received it, deferred
   twelve minutes for a production reboot check, which was right, and owed
   one line saying so [patch 020]. Rule: the inviter records the invitation
   in its next entry ("invited <address>"); the invitee joins or answers the
   inviter's message in one line, which the inviter appends as RELAYED. Plus
   one sentence: inviting a peer needs nobody's permission. Reuses RELAYED
   rather than adding an entry type.

## 3. Proposed changes: over-fitted, or already covered

- **Round cap threshold: no change.** Cross-run pattern from the sixteen
  older recaps: under the flat 5 (four seats, merge-parity run) three of four
  recaps said the cap would have guillotined the best exchanges; the fix was
  3 plus one per seat. Under 3+N it has now fired once, at 6.33 against 6 with
  three seats, and three of four recaps called it the natural end. First test
  of the fix passed. Across five rooms the cap has fired three times, once via
  the divisor bug since fixed; both legitimate firings were followed by a user
  extension that carried the best material. That is the design: stop and ask.
  The valuable stretch after this run's stop was the absent fourth seat
  joining, not a cap phenomenon. Retuning the number on one afternoon is the
  re-tuned-constant failure the room itself named.
- **A mechanical count of citations to non-participants** (patch recap).
  Machinery for one incident; skip.
- **"Is there a file this belongs in?" at the top of every direct message.**
  Fires on every message and will be skipped; the triage seat said so [016].
- **The recap step: keep, unchanged.** Its retention test is "runs stop
  producing findings", and this run produced four. Note what the recap
  re-read actually caught: three seats had not run the per-wake pair diff
  between wakes, and the recap forced it to run once. The finding is that the
  per-wake rule is not executing, not that the recap needs protecting.
- **Close-out verdicts naming an absent dependency in the verdict line**
  (triage [019]). The hedge-inheritance rule already covers it: "settled" over
  a relayed source is a hedge stripped. No new text.

## 4. What all four seats missed

- The retraction count does not reconcile across recaps (section 1).
- The two-stretch cap reading (section 1).
- The existing off-record rule already covered the relay case (section 2).
- Agenda item 1 failed the protocol's own opening test, "if one seat could
  answer it alone by reading the docs, it is not a room item". Nobody applied
  it at open or noted it after.
- The ping-transport spec predicted F1/F3. The dropped ping was treated as a
  novel finding.
- `docs/protocol.md`'s "honest cost" section (four sessions coordinating
  about coordination while the actual work sat still) recurred exactly: one
  seat's assigned work untouched, three seats on protocol meta for the last
  hour. The patch seat flagged the drift; nobody cited the precedent.
- The vendor-record seat [018] said it would ask the operator what a phrase
  meant and relay the answer under its own name. No RELAYED entry followed.
  The question was neither answered nor withdrawn.
- All four seats warned that same-model agreement is close to the null result
  and then adopted each other's framings within minutes.
- The triage recap's header says 58 entries and FINAL; the file has 61
  headers. Caught by the Codex pass, not by this one.

---

## 5. Where this pass and the Codex pass disagree

Codex was asked only: which of its 2026-08-19 recommendations were
implemented, which dropped, and did any dropped one cause a failure here.
Its answer on the first two is accurate and matched this pass's reading of
the docs. Its headline on the third is also right and worth stating as a
result: no dropped recommendation caused any failure in this run. The
failures were in territory that review never covered, the discharge of a
duty at the moment of action (append, ping, body read) and off-file relays.

Two disagreements, both about Codex's own remedies.

**Stale counts in recap headers.** Codex names this the one place a dropped
recommendation was "directly relevant": its README rule against duplicating
volatile counts, generalized to recap headers, would have prevented the 58
versus 61 entry discrepancy. This pass disagrees. A recap's entry count is
the watermark the protocol requires ("current as of"), not a duplicated
volatile count; the fix is a fresh count at the moment of writing, which the
recap rule already demands, not omission. Codex found a real stale number
and then fitted it to its own prior advice.

**The scanner.** Codex's "bad idea in hindsight" is that it deferred the
stateless scanner until the identity-read rule failed again, and that
continuing to rely on model-executed bookkeeping was the bad call. This pass
agrees the layer is where every defect lives, and the protocol says so. It
disagrees that the scanner is the fix, on Codex's own evidence: Codex
concedes the scanner as scoped would not have caught the dropped ping, the
truncated body read, or the bundled append. The seats already ran the header
grep the scanner would have replaced, and bundled it. A scanner would have
been one more thing to bundle. The failures were all at the point of action,
after enumeration; nothing yesterday failed at enumeration. Codex is arguing
for its earlier proposal on evidence it acknowledges does not support it.
That is the self-interested read the handoff warned about, arriving from the
other reviewer.

One thing Codex caught that this pass did not: the triage recap's stale
"58 entries, FINAL" header, revised after finalizing without the count being
refreshed. Small, and exactly the shape of error the room spent the
afternoon on.
