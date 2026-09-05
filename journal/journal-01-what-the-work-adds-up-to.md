# What the Work Adds Up To

*September 2026*

---

There's a moment in any research project where the accumulation of pieces — prototypes, specs, adversarial passes, a theory document, a handful of notebook entries — reaches a mass where it's worth stepping back and asking what it actually adds up to. Not what each piece does individually. What the whole thing is for.

This is another one of those moments.

The work is running on at least three tracks simultaneously. They're related, but they're not the same argument, and conflating them would misrepresent all three. So I'll describe them separately, then say what I think the combination establishes and what it honestly doesn't.

---

## Track one: the prototype

The employment-seam prototype is the most concrete thing. It builds a local-first system — documents live on your device, access is governed by cryptographic capabilities, no server owns the state — and implements a series of governed crossings from that local substrate into the AT Protocol public feed.

Four phases of the prototype have run. The first two establish the mechanism: a crossing-intent record is written before anything is published, a gate checks the grant, and a completion record is written afterward. A back-pointer travels with the intent record. The basic discipline — write before fire, verify before cross, record after — is live.

Phase 3 tested whether that discipline holds under pressure. Three scenarios: a crossing assembled from multiple governed source documents, a delayed-release crossing with a not-before constraint, and a content-integrity check that deliberately introduced tampered content between authorization and fire.

All three held. But holding isn't the same as being unqualified. Two findings narrowed the claim.

The content-integrity scenario names a structural limit: the window between when content is authorized and when the crossing fires cannot be zero in any system that separates authorization from execution. You can bound it — and this implementation does, to the duration of a single pipeline run — but bounding is not closing. That limit is now named in the work as a first-class finding, not as a deficiency to be fixed later.

The delayed-release scenario raised the more interesting open question. What happens when the grant authority behind a crossing expires *before* the release horizon passes? The seam enforced the not-before constraint correctly; the grant didn't lapse in any run. That combination — delayed release with a lapsing grant — was not exercised. It's a scenario to consider if you're building anything where time-delayed crossings matter.

The [notebook](https://github.com/jediwright/seam-stack/tree/main/notebook) is the field report record for this track. Entry 04 is the Phase 3 report. Three territories named in entry 03 as honest open questions — the Update Framework, W3C Verifiable Credentials, and decentralized attestation systems like EAS — remain unswept. Whether those systems occupy the same space as this architecture, or leave this specific combination of constraints unoccupied, is genuinely unknown.

---

## Track two: the boundary theory

In parallel with the prototype work, the theoretical framework the prototype demonstrates was written out and subjected to adversarial review. The result is an essay — [Local-First at the Edge](https://github.com/jediwright/seam-stack/blob/main/essay/local-first-at-the-edge.md) — that names seven boundary principles derived from studying where local-first's interior theory runs out.

The short version: local-first got the interior right. The seven ideals that Kleppmann, van Hardenberg, McGranaghan, and Wiggins published in 2019 are a complete theory of what a local-first system should be *inside* — data on your device, offline operation, real-time collaboration, long-term preservation. Every one of those ideals is an interior claim. None of them says what happens at the edge.

The essay argues that this is a structural consequence, not a deficiency: any strong interior discipline generates a boundary shadow. The governed-crossing architecture starts where the interior theory ends.

Seven boundary principles are stated. I won't restate them here — the essay does that. What's worth saying in this context is where each principle stands:

P8 (every crossing is explicit, minimal, and designed) and P9 (exposure claims are upper bounds) are the most heavily worked on. The prototype demonstrates both, and the second substrate — AT Protocol — required P9 to be stated more precisely than the first substrate did. The honest floor value for post-crossing exposure isn't "you've lost control" — it's a named vocabulary item, `exposure-unbounded`, that travels in the crossing record rather than being disclaimed in prose.

P11 (agents are governed parties, never the authors of record) is where the prototype does its most novel work. The employment-seam prototype is, on current evidence, the first worked example of an agent-as-governed-party principle operating on a local-first data floor at the spec and prototype levels — with contact-class taxonomy and act-time capability-currency checks. That's a scoped claim. It doesn't say no one has thought about agent governance on local-first systems; it says no prior demonstration has been found at this specificity.

P10 (data shapes carry lineage and horizons) has a companion spec in the [governed-schema-evolution](https://github.com/jediwright/seam-stack/tree/main/governed-schema-evolution) directory — the Governed Schema Evolution Framework. The GSEF's questions about schema change governance are sub-questions of this principle.

P13 (governance composes beyond the individual) is the most honestly incomplete. The evidence plane is built: amendment records, objection records, consent records, and resolution records — the governance trail is a prototype-level implementation. The decision-plane machinery for n≥3 parties reaching contested amendments without a finality arbiter is not. That's named in the essay as a Known Limit, not papered over.

P14 (relay boundaries are governed crossings) is specified but not fully designed. Relays are in scope; the three open items from the chained-crossing observation are inputs to future work.

The principles survived adversarial review before publication. That's not a claim that they're settled — it's a claim that they held against a structured challenge that was trying to overturn them.

---

## Track three: the formal grammar

This is the track no public reader has seen yet.

The pattern specification — what's in the [local-first-series](https://github.com/jediwright/local-first-series) repo — describes the seam architecture as a pattern. The notebook and the essay demonstrate and argue for it. But a description and a demonstration aren't a formal grammar. A formal grammar is something you can instantiate, run against, and verify. It's what lets you say "this implementation satisfies these rules" rather than "this implementation seems to match the description."

There's a grammar in progress. It operates at rung 2 — above the level of individual field types, at the level of structural derivation: given a seam's regime (what access model it crosses between, what the vocabulary of its exposure claims is, what the phases of its ceremony are), derive whether a specific crossing record matches what the grammar predicts.

That grammar has been run against two fixtures from the employment-seam prototype at two different commits. It passed both. More precisely: it passed both with a defined pass rule that checked field set, required/optional partition, and fixed-literal values. The emitter — the thing that generates crossing records from the prototype's TypeScript source — didn't need to change to satisfy either fixture. That's a meaningful result: the grammar was predictive, not retrofitted.

The grammar is currently in adversarial review. Every claim it makes — about what it predicts, what it generalizes to, what its known limits are — has been challenged by an independent context, and the producer has either amended the claim, narrowed it, or registered a Known Limit that the challenger accepted as honestly stated. Thirteen objections, all resolved, every surviving claim narrower than it started. That process is not done — the grammar issues are cleaned up once the r-amendment session closes and a second adversarial pass runs.

What does the grammar track add that the prototype track doesn't? The prototype shows the mechanism working. The grammar asks: working according to what rules, exactly? And: do those rules hold for a second seam instance — one that uses a different access model, a different vocabulary, different ceremony phases — without the grammar needing to change? That's the second-seam question. It hasn't been answered yet. The employment-seam prototype runs on Keyhive, which uses a revocable capability model. A second seam running on a different access model would either satisfy the grammar with the same rules, require vocabulary changes while leaving the structure intact, or expose a place where the current grammar's rules are publication-substrate-shaped rather than genuinely general. Any of those three outcomes is informative.

---

## What the combination establishes

Three tracks running simultaneously produce an argument at a different scale than any one track alone.

The prototype shows a worked implementation of the boundary principles. The boundary theory names and argues for those principles with honest limits. The grammar asks whether the principles are precise enough to be formally stated and checked — whether "seam" means something specific enough that you could write a rule for it.

Together: this is an architecture for governing what happens at the edge of local-first systems, demonstrated at the prototype level on two substrates, stated as a theory, and currently being formalized. That's the honest description of where things stand.

What it doesn't establish yet: whether the grammar generalizes beyond the current two substrates; whether the three unswept falsifier territories leave this specific combination of constraints unoccupied; whether the collective governance machinery works at non-bilateral scale. Those are the honest open questions. They appear here because the work takes P9 seriously — exposure claims are upper bounds — and that principle applies to claims about the work itself as much as to anything the work governs.

---

## What comes next, and why it matters

The second-seam work is the most important near-term test. The employment-seam prototype runs on Automerge with Keyhive for access control. A second seam, on the same codebase, would cross between two parties both using revocable capabilities — a fundamentally different access model than crossing from a revocable local substrate to a public, non-revocable feed. If the grammar's rules hold unchanged, that's evidence of generality. If vocabulary changes but structure holds, that's evidence of a different kind — the grammar is structural, not vocabulary-specific. If structure breaks, that's the most interesting result: the current grammar is publication-shaped, and a more general grammar requires more work.

The unswept territories matter for the same reason any honest accounting of prior art matters. The Update Framework governs software update metadata with time-bounded validity assertions and a client-verifiable integrity anchor. The structural overlap with what this prototype does is sufficient to warrant a proper comparison. If TUF or W3C Verifiable Credentials or EAS exhibits the same composition of constraints, the claim needs to be updated. If they don't, the architecture's position in the space is clearer.

The GSEF work and the P13 decision-plane work are the longer-horizon open questions. Schema governance and collective governance at scale are both real problems; both have partial answers here; neither has a complete one.

None of this is a complaint about the state of the work. A program that knows its open questions and is building toward answering them is exactly what research is supposed to look like. The open questions here are specific and answerable. That's the thing worth saying publicly.

---

*Developed with AI assistance; human authorial responsibility and intellectual direction held by Jedi Wright / Systems of Thought / UX Minds, LLC. [MIT license]*
