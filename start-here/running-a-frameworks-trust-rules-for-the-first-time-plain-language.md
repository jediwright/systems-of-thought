# Running a Framework's Trust Rules for the First Time, in Plain Language

*A short version of [lab notebook entry 05](https://github.com/jediwright/seam-stack/blob/main/notebook/05-running-a-frameworks-trust-rules-for-the-first-time.md)*

*2026-09-11*

---

## The setup

I have a framework for organizing content called the Tiered Content Framework (TCF). Part of it says that every piece of content should carry a label for how much you can trust it: confirmed, inferred, unverified, or time-sensitive. The label attaches at the smallest unit—a single claim—and passes upward. A page built from claims can never be more trustworthy than its least trustworthy claim.

Until this month, that was a rule written in a document. I just hadn't built anything that enforced it.

In August I wrote a spec for that thing. In September I decided to build a small version of it before revising the framework again, on the theory that the build would show me what the revision needed to fix. It did.

## Where this came from

The trust labels didn't start as a content-management idea. They started in March, in my essay called [The End of History, Revisited: A Compound Civilizational Stress Event, the AI Governance Window, and the 10% Path](https://www.systemsofthought.com/the-end-of-history-revisited/), which asked whether democratic institutions can still bind AI before AI is embedded too deeply to bind. While that essay was being drafted, an airstrike k*lled students in a building that had once been a military compound. The targeting data had never been updated. What failed wasn't the model; nothing in the system could tell the difference between a confirmed fact and an assumption that had hardened into one.

That became the question underneath everything since: how does a system know what it actually knows? The first answer was written for people deploying AI in consequential settings, with the [Agentic Accountability Playbook](https://docs.google.com/document/d/18pPx6X5wmTv-eWRGdPD02fkDO4pK9ORm0HX5mK6qJgA/), which said every input to an automated decision should carry one of four labels: confirmed, inferred, unverified, or time-sensitive. The content framework I'd been building for years adopted the same four labels in May, for the same reason: a page assembled from claims has the same problem as a decision assembled from inputs. Those two frameworks share the vocabulary on purpose; they govern different sides of the same exchange.

This entry reports the first time a machine enforced those labels rather than a person reading a document and trying to comply with it. The path from a strike on a building that had changed its use to a gate that refuses to save an unverified claim marked "confirmed" is long, and most of it is still ahead. But that's the path.

---

## What got built

A gate. When someone tries to save a piece of content, the gate checks it first:

- Is the trust label one of the four allowed values?
- If it says "confirmed," is there a record of who verified it and when?
- If it's time-sensitive, does it say when it expires?
- Is someone raising a label — say, from "inferred" to "confirmed" — without new evidence?
- Is a claim derived from another claim pretending to be more certain than its source?

If any check fails, the save is refused with a specific reason. If they all pass, the gate recalculates the label on everything built from that content, marks older summaries as out of date, and saves the whole thing as one change.

Twenty test cases run against it. Nineteen came out as predicted. One didn't, so I left it as is and wrote down why. Every kind of refusal the gate can give was triggered by at least one test, on my own machine, with the software versions locked so anyone can reproduce it.

---

## What the spec got wrong

The build's most useful product was a list of places where my own spec didn't work as written. Three are worth explaining.

**It used a construction the standard doesn't allow.** One of the rules compared trust levels using a lookup table written inline in a place the validation standard explicitly forbids. No compliant tool can run it. The fix was to express the same comparison a different, legal way. The meaning didn't change; the text was simply wrong.

**It said it stayed silent, and it didn't.** The rule for computing a page's label says: if any part of the page has no label at all, the page gets no label either. Silence, not a guess. In practice, because of how the query language handles missing values, a part with no label was being treated as the *lowest* label, and the page came out "unverified."

This is the one that matters. The whole point of the rule is that nothing gets a trust label it didn't earn. The machinery built to enforce that was quietly handing out the weakest label to things that should have had none. It picked the safest wrong answer — but a safe default is still a default the rule said would never happen. The fix makes the gate refuse to compute a page's label until every part has one.

**Its own test was impossible to pass.** One test was written to trigger the "you can't upgrade without evidence" refusal. It never got there, because an earlier check rejects "confirmed with no record" first. My prediction and my step order disagreed. I left the test alone, marked it as a known miss, and added a second test that reaches the rule by a path the order actually allows.

I also logged three smaller issues, including one where the spec refers to a timestamp that no record actually contains. That's the one place where the build let something through instead of refusing it, and it's flagged for the next framework revision rather than settled here.

---

## What a second reader caught

After the build closed, I had the spec reviewed adversarially — a separate session that could see the spec and the build report but not the conversation that produced them — and was told to find what's wrong, run until it stopped finding things.

It found a bug the tests missed. The "stay silent" fix had been applied one level up but not two: a section above an unlabeled claim correctly got no label, but a page above an unlabeled section still did. None of the twenty tests covered that. The reviewer found it by reading the code against the rule, not by running anything. I added a test, extended the fix, and the test passed.

That's a result about method, not about content. A passing test suite can't catch a case it doesn't contain. A reader looking for what's wrong can.

---

## What I can now say, and what I can't

Before: the framework's trust rules are written down, and there's a draft spec for enforcing them.

After: a gate enforcing those rules runs on locked software versions, reaches every refusal on real tests, and the spec it follows has been corrected in the four places where the text didn't work.

What I can't say: that the framework is "executable." This covers one of its three governance dimensions and touches four of its seven tiers. The field names the gate uses are provisional until the framework's next revision rules on them, so every label the gate computes is provisional too. One long-standing question — whether "time-sensitive" sits in the trust order or alongside it — is still open; no test produced a case where the answer would have changed the outcome, and I'm saying that as "not yet tested," not "resolved."

Nothing here stops a real publish event yet.

---

## What's next

The framework revision can open now, using the build's findings as input. The next phase of the runtime — real storage, the connection to the publishing gate, the extra integrity checks the reviewer pointed at — waits until that revision has ruled. Building on provisional names twice would be building on the same uncertainty twice.

---

*The full entry, with the technical detail, is [lab notebook entry 05](https://github.com/jediwright/seam-stack/blob/main/notebook/05-running-a-frameworks-trust-rules-for-the-first-time.md). The code is at [jediwright/tcf-runtime](https://github.com/jediwright/tcf-runtime). The framework it implements is the [Tiered Content Framework](https://www.jediwright.com/content-strategy-framework); the code doesn't change the framework. When the code finds a problem, it gets written down as a question for the next revision.*
