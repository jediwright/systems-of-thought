# Systems of Thought

Research program documentation for work at the intersection of local-first software architecture, AI governance, and worker-side data sovereignty.

This repo is the root of the research program — the place where the intellectual direction of the work is tracked across all active workstreams. It's distinct from the [Systems of Thought publication](https://systemsofthought.com), which is where the polished long-form essays go. This is where the program is documented as it runs.

---

## What's here

**[`journal/`](https://github.com/jediwright/systems-of-thought/tree/main/journal)** — Dispatches on the state of the research program. Not field reports (those live in the [build notebook](https://github.com/jediwright/seam-stack/tree/main/notebook)) and not theory essays (those are in the [seam-stack essay directory](https://github.com/jediwright/seam-stack/tree/main/essay)). The journal is where the full program gets a view from altitude.

More directories will appear here as workstreams produce material ready for public placement.

---

## Active repositories

| Repo | What it is |
|---|---|
| [jediwright/seam-stack](https://github.com/jediwright/seam-stack) | The Seam Stack architecture: theory, boundary principles, build notebook, governed schema evolution framework, vocabulary |
| [jediwright/local-first-series](https://github.com/jediwright/local-first-series) | Pattern Commons — reusable seam patterns, including PC#7 (employment seam) and PC#8 (substrate-crossing seam) |
| [jediwright/employment-seam](https://github.com/jediwright/employment-seam) | The employment-seam prototype — local-first document crossing to AT Protocol, built on Automerge + Keyhive |
| [jediwright/governed-pr-framework](https://github.com/jediwright/governed-pr-framework) | GPRF — a governed pull-request framework for AI-assisted development |
| [jediwright/local-first-social-network](https://github.com/jediwright/local-first-social-network) | Local-First Social - a local-first social prototype built on Y.js and IndexedDB, with a stateless WebSocket relay that facilitates peer connection and exits. Seam governance and AT Protocol retrofit in progress. | 

---

## Publication surfaces

- **[systemsofthought.com](https://systemsofthought.com)** — long-form essays (Ghost)
- **[jediwright.com](https://jediwright.com)** — practitioner trade work & more
- **[jediwright.leaflet.pub](https://jediwright.leaflet.pub)** — AT Protocol-native practitioner layer
- **[@jediwright.bsky.social](https://bsky.app/profile/jediwright.bsky.social)** — Bluesky

---

## Full scope of work (not exhaustive)

**Theoretical frameworks**

- **Resonance Architecture (RA)** — A theory that any structured domain runs on a shared seven-tier organizational grammar (Bind → Totalize), prior to and independent of any framework describing it. The RA is both the theory and the testing program: predictions are pre-registered, mapped against fresh domains, and scored under adversarial discipline.
- **Tiered Content Framework (TCF)** — A framework for governing content structure across seven tiers (Quarks → Biomes) with cross-cutting dimensions for intelligence, taxonomy, and machine-legibility. Governs how content objects are structured and tagged with epistemic status.
- **Narrative Content Framework (NCF)** — A derivative of the TCF adapted for the creative domain. Collapses the TCF's three cross-cutting dimensions into a single Constant Layer. NCF development fed back into the TCF, triggering the Quarks amendment.
- **Grammar of Trust** — An argument that language is the infrastructure through which institutional trust transmits across time. Names the term "infrastructure" in the governing vocabulary.

**Architecture and governance**

- **Seam Stack** — A four-layer architectural pattern (Substrate, Governance, Boundary, Evidence) for governing the moment data crosses from a local-first system into something external. Documented in [`THEORY.md`](THEORY.md).
- **Governed Schema Evolution Framework (GSEF)** — Governs how data schemas change over time without breaking downstream dependents. Specifies blast-radius classification, temporal-crossing checks, and lineage obligations across all four Seam Stack layers.
- **Governed PR Framework (GPRF)** — Governance for code changes. Tiers every change by how far a failure could spread and applies scrutiny proportionally, with protected surfaces declared up front. Published at [`jediwright/governed-pr-framework`](https://github.com/jediwright/governed-pr-framework).
- **Form C / Artifact B** — A multi-principle governance manifesto for boundary-crossing architectures. P10 governs lineage; P11 governs agent authority (agents are governed parties, never authors of record); P12 governs longevity commitments.

**Pattern Commons series** — Reusable, versioned pattern entries for governed data crossings. Published at [`jediwright/local-first-series`](https://github.com/jediwright/local-first-series).

- **PC#00 — The Governed Crossing** — The foundational entry. Defines a governed crossing: a state change at a boundary, with a record readable by a party who wasn't there.
- **PC#7 — Employment Seam** — The employment relationship as a governed crossing: entry, exit, agent capability grants, and revocation discipline. Prototype at [`jediwright/employment-seam`](https://github.com/jediwright/employment-seam).
- **PC#8 — Substrate Crossing Seam** — The first crossing pattern built on an authorization-backed substrate (Automerge + Keyhive), with write-before-fire intent records, delayed-release horizons, and TOCTOU integrity controls.
- **PC#9 — Governed Content Production Crossing** — How content moves from a local authoring environment into a publication surface, with chained crossing records and surface validation.

**Essays and long-form arguments**

- **[Full Personhood: The Governance Model AI Requires and Capitalism Never Built](https://www.systemsofthought.com/full-personhood/)** — The central governance argument: information asymmetry between institutions and individuals is architectural before it is political.
- **TaR (Time-as-the-Return)** — An economic model arguing that worker time is the primary unit of value being extracted and that yield attribution should reflect that.
- **AI Governance Window Tracker** — A five-domain signal framework assessing whether the window for binding democratic AI governance is opening or closing.
- **Cultural Antenna** — A spec for tracking and interpreting cultural signals through a structured, governed framework.

---

*J. Wright / UX Minds, LLC — AI-collaborative research; human authorial responsibility and intellectual direction held by the named author.*
