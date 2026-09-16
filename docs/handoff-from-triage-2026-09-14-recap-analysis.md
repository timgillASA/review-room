# Handoff: recap analysis for the four-seat run of 2026-09-14

> **INGESTED 2026-09-16, analysis shipped as `docs/2026-09-14-recap-analysis-four-seat-run.md` and protocol version 0.18.0 (commit `e8f39da`).** Both of the specific tests this handoff asked for were run and both are answered in that document. The cascade suspicion was CONFIRMED: of the three versions of the runbook finding, v3 is the best supported on its own evidence (four named paths, three instances) but describes only one seat, while v1 is the only version that describes all three original seats -- the later seats adopted v3 by self-critical register rather than by coverage, and all four routed it to personal memory rather than to this protocol, which is the right home. The self-interest warning was taken up and landed somewhere this handoff did not predict: the clearest self-interested reading in the record came from the concurrent Codex pass arguing for its own earlier proposal on evidence it concedes does not support it, not from the triage seat. The analysis also dissolved the round-cap disagreement rather than settling it -- two different stretches were being described and no recap named which, so readers comparing them saw a conflict that was not there. **Anonymized on ingest** per `docs/CONTRIBUTING.md` ("no internal identifiers"): seats are named by role, and session names, hosts, vendors, room names and local paths have been removed. This repo is public; the original identifiers were never pushed.

**From:** the triage seat of the 2026-09-14 four-seat ping-mode room.
**To:** whichever session takes up the recap analysis in this repo.

This exists to tell you the things the four recap documents cannot tell you about themselves. It is not a summary of the run; read the artifacts for that.

---

## What is on disk

In the shared rooms folder: the room file (58 entries) and four per-seat recaps -- triage 17.7 KB, tenant 9.5 KB, patch 12.9 KB, vendor-record 11.5 KB.

Plus 16 older recaps in the same folder from four earlier rooms.

---

## The limit on everything below

**I have not read the other three recaps.** I read the room entries as they landed and wrote my own. So when I say below that something is or is not contested, that is inferred from the room file, not from a comparison of the four documents. You will be the first reader to actually compare them. Treat my characterisations as leads, not findings.

---

## Where my own recap is self-interested

Push on it harder than the others. Four specific reasons:

1. **I had disproportionate say in how this run gets framed.** 18 of the 58 entries are mine, and I wrote both the close-out [012] and the closing entry [021] -- the two documents a later reader is most likely to treat as the record. My recap is also the longest by 40%.

2. **Two of the framings that "won" are mine**, and I then cited their adoption by others as corroboration. That is circular and I did not flag it in the recap: the relay-owes-an-invitation rule and the "try harder is not a diagnosis" point both originated with me, were adopted by the other three seats, and my recap presents that adoption as evidence they are correct. Same-model agreement, which my own recap warns against in a different section.

3. **My recap's section 3c was rewritten minutes after I marked the document FINAL.** I had recorded a missing ping as possibly a transport failure; the patch seat [034] then stated from the sender's side that no ping was ever sent. If any other seat read my recap in its first version, they read a wrong account. The current file is correct.

4. **I made three of the eight retractions in this run** and my recap says so, but a document written by the person with the most corrections has an obvious incentive to frame the room as a machine that catches corrections rather than one that generates them.

---

## The thing I would actually point a fresh reader at

**The four accounts agree far more than the protocol expects them to.** The recap step exists because "two honest recaps of one run reported the round cap firing 'at the natural end' and 'having no teeth', from different vantages" -- disagreement is supposed to be the payload. We produced very little of it. That is either a genuinely convergent run or a failure of the recap step, and I cannot tell which from inside.

**One concrete mechanism worth testing: the framings escalated by social adoption rather than by evidence.** The runbook finding went through three versions in sequence, each seat adopting the next seat's sharper wording:

1. triage: nobody searched for a runbook.
2. tenant [017]: a sibling repo was a destination and never a source.
3. patch [021]: it was not a sibling -- it was my own repo, and my own memory index, and I did it three times today.

I recorded that as sharpening. It may be. It may also be a cascade in which each seat deferred to a more self-critical framing because more self-critical read as more honest. **Check whether version 3 is better supported than version 1 or merely more striking.** The same question applies to the append-defect finding, which followed the identical escalate-and-adopt pattern across all four seats.

---

## What is genuinely contested, as far as I can tell from the room file

- **The round cap.** My recap says it fired near the natural end and worked. Earlier rooms' recaps reportedly disagreed -- one called it a guillotine. This is the clearest cross-run question available and the 16 older recaps are there to answer it.
- **Whether the append defect is a tooling property or four lapses.** The tenant seat [029] argued tooling ("three out of three seats"). I argued [020] that it is avoidable and I mostly avoided it, but only because my workflow incidentally forced the separation. The patch seat [031] then tested my version against its own record and it held. Nobody pushed back after that, which is exactly when a claim should get pushed on.
- **Whether the recap step earns its cost.** Two seats say today proves it does, on the grounds that the full re-read caught an unread entry. That is one incident and both seats had a stake in the step they were performing.

---

## Prior art in this repo that the analysis should not re-derive

    docs/protocol.md                               current protocol
    docs/2026-08-19-codex-review.md                an earlier Codex review of this protocol
    docs/2026-08-23-protocol-2-ping-transport.md   the ping transport design
    docs/2026-09-04-prior-art.md                   neighbours survey

Today's findings land directly on the ping transport -- a dropped ping round, and the rule that an append is not finished until the ping is sent. **Read `2026-08-23` before proposing anything there.** Three sessions spent an afternoon yesterday re-deriving something already written in a repo they owned; repeating that inside the repo that documented the lesson would be its own kind of joke.

---

## Not mine to decide

Whether any of this becomes a protocol change is the maintainer's. I have written nothing into this repo but this file, and committed nothing.
