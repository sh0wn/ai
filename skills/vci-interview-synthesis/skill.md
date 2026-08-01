---
name: vci-interview-synthesis
description: Use this skill to synthesize Veteran Centric Insights stakeholder interview transcripts into a structured research document. Trigger whenever the user says things like "synthesize the interviews," "create a synthesis," "pull together findings from the transcripts," "update the research synthesis," or when new transcripts have been added and the user wants the synthesis updated. Also trigger if the user asks what stakeholders said, what themes emerged, or what the interviews tell us, even if they don't use the word "synthesis."
---

# Veteran Centric Insights Interview Synthesis

This skill produces a structured research synthesis from one or more stakeholder interview transcript in the `transcripts/` folder of the CXDM Stakeholder Interviews project.

## Before you start

Don't assume which transcripts this synthesis should cover, or what format they're in. Ask first, then read. A synthesis silently scoped to the wrong set of interviews, or built on the wrong version of someone's transcript, is a worse failure than spending one extra turn confirming scope.

1. Look at what's actually in `transcripts/` before asking anything, so the question you ask is grounded in what's really there rather than an assumption. Projects vary: some keep a single transcript file per participant, others keep more than one version of the same interview (for example, a raw export alongside a cleaned-up pass, sometimes labeled "polished," sometimes not labeled at all). Note whatever pattern is actually in use. Also check the existing `research-synthesis_*.md`, if one exists, to see which participants have already been covered in a prior round.
2. Ask the user which transcripts this synthesis should cover. Use the AskUserQuestion tool if it's available. Offer the most likely default, everything not yet reflected in an existing synthesis, as one option, but make it easy for the user to instead pick a specific subset or re-run against the full set from scratch. Don't skip this step just because a default seems obvious; the whole point is that it often isn't obvious to the person asking, and it's cheap to confirm.
3. If a participant has more than one version of their transcript available, ask which one to use rather than defaulting to one silently, and note the choice in the synthesis itself. A less-reviewed or unedited version can still be a good source of genuinely exact quotes (useful for the Quotes section), but it hasn't been checked for accuracy the way a cleaned-up version has, so weigh claims sourced from it with the same care given to any single-sourced claim.

Once the transcript set is confirmed, read:
- The confirmed transcripts
- `Product Brief_CXDM.md` — for KPI and goal language to reference throughout
- The existing `research-synthesis_*.md` if it exists — to update rather than overwrite findings from previous interviews. If a `revision_notes` field exists in its frontmatter, read it: it records what a prior quality pass changed and why, and those lessons should carry forward into any new synthesis rather than being re-discovered from scratch.

Also note who the stakeholders are *not*. If every interview so far comes from the same org or team (e.g., all VEO-adjacent), that's a real limitation on how far the findings generalize, and it needs to be said explicitly rather than left implicit.

## Output

Write the synthesis to `research-synthesis_[participant-initials].md` in the `Stakeholder Interviews/` root folder — the same folder where the other `research-synthesis_*.md` files live. Do not write it into the `vci-interview-synthesis/` directory; that folder is where this skill lives, not where output goes. If updating an existing synthesis with new interviews, update the existing file and add the new participants to the filename. If revising an existing synthesis for accuracy or framing (not adding new interviews), save the revision as `_v2`, `_v3`, etc. and add a `revision_notes` line to the frontmatter summarizing what changed and why, so the next person (or the next run of this skill) can see the history at a glance.

## Formatting rules

- **Names:** Use last name + first initial throughout (e.g., A. Moos, D. Borden, L. Waters). Full names appear only in the document header.
- **Headers:** Use natural, conversational language, not jargon. Headers should read like a sentence, not a label.
- **Context sentences:** Each section opens with a short italicized sentence tying it back to the relevant CXDM Product Brief goal.
- **Sources:** Cite by last name + transcript timestamp (e.g., Moos 17:41). Timestamps correspond to section headers in the transcript. Before citing a timestamp, confirm it actually exists as a section header in that participant's transcript, and that the content you're attributing genuinely appears there. A citation that doesn't trace back cleanly is worse than no citation, because it looks verified when it isn't.
- **Citation density:** cite at the level of the specific claim, not the paragraph. A theme or trust-issue entry often makes several distinct claims about several different people in a row, if the citation only appears once (in a topic sentence, or trailing at the very end), a reader can't tell which sentence it actually supports once more than one name is in play. As a concrete check: read each sentence in isolation, if it names what a specific person said, did, or believed, it needs its own `(LastName timestamp)` right there, even if that person or a nearby timestamp was already cited earlier in the same paragraph. Don't rely on a name appearing once at the top of a paragraph to implicitly cover every claim that follows it.
- **Product brief KPIs:** Design implications end with an italicized `*Product brief KPI: [name]*` line.
- **Transcript version record:** If more than one version of a transcript exists for any participant (e.g., a raw export vs. a cleaned-up pass), note in the frontmatter which version was used for each. This determines whether quotes pulled into the Quotes section are exact or paraphrased, and it's the kind of thing that's easy to forget once it's no longer a safe default. If there's only one version per participant, this note isn't needed.

## Rigor rules (read this before writing "all three" anywhere)

These are the rules a careful editor would apply on a second pass, so it's worth applying them on the first pass instead. With only 3-5 stakeholders in a typical round, small wording choices are the difference between an accurate synthesis and one that overstates what was actually said.

- **Consensus language must be earned claim-by-claim, not just topic-by-topic.** Two stakeholders raising the same general subject (e.g., "contact reason accuracy") doesn't mean they made the same specific claim. If Stakeholder A says the data is inaccurate and Stakeholder B says the data can't be compared across centers, those are related but different concerns, don't collapse them into "both said X is unreliable." Say what each person actually said, and only use "all N participants" language when every one of them made the same specific claim, not merely touched the same topic.
- **A pattern needs at least two independent sources to be called a pattern.** If only one stakeholder raised something, however important it sounds, label it that way ("raised by one stakeholder; not yet corroborated") rather than implying it as a shared finding. This is especially true for anything that will drive a build recommendation, single-sourced recommendations should still be included if the evidence is strong, but flagged so the reader can weigh confidence accordingly.
- **Preserve hedges instead of smoothing them into settled facts.** If a stakeholder says "I trust it, but I'll double-check myself this week" or "I'm not fully certain," that hedge is signal, not noise. Carry it into the synthesis rather than stating the underlying claim as fully resolved.
- **When a theme spans multiple participants, check whether they actually agree, or just share a topic.** Three people can all describe the same structural gap (e.g., "the enterprise analytics layer doesn't exist yet") while holding three different postures toward it, optimistic, resigned, neutral. If their tone or framing diverges, name that divergence in the theme rather than averaging it into one flattened voice. The divergence is often more useful to a client than the shared topic is.
- **Look for at least one positive or counter-example, not just gaps.** These interviews tend to surface pain points by design, but a synthesis that is 100% deficit-framed risks reading as more negative than the underlying reality. If a stakeholder describes something that already worked (a metric that improved, a workaround that's actually holding up well), include it. It gives the client a fuller picture and shows the synthesis isn't just pattern-matching for problems.
- **Don't let a synthesizer's own interpretation masquerade as a stakeholder finding.** It's fine to include forward-looking framing like "this is the moment for CXDM to make this real," but write it as your own editorial voice (e.g., in the design implications section), not folded into "what the interviews tell us" as if a stakeholder said it.

## Document structure

Produce these sections in order:

---

### 0. Summary

A leadership-facing opening that stands on its own — no transcript inventory, no org coverage disclaimer, no acronym list. Write it as if a senior stakeholder who hasn't read the rest of the document will make decisions from this section alone.

Structure it in three parts:

1. **A framing paragraph** — one or two sentences describing the overall landscape the interviews reveal. What is the condition of the data, the people, and the organization right now? This should read as a situation assessment, not a list of findings.

2. **Three headline findings** — bold, numbered, written for leadership. Each finding should name a tension, a risk, or an opportunity — not a topic. Support each with one direct quote from a participant that captures the stakes. Choose quotes that a non-technical reader would find striking, not ones that require context to land.

3. **A bottom-line callout** — one or two sentences naming the single highest-priority build recommendation from Section 3 and pointing the reader there. Client readers skim; the most decision-relevant insight in the document shouldn't be something they only reach after several sections.

**Citations in the Summary are required.** Every specific claim — including the supporting quote for each headline finding — must carry a `(LastName timestamp)` citation. The Executive Summary is often the only section leadership reads, and it is also the section most likely to be challenged. If a claim can't be traced to a source, it shouldn't be in the Executive Summary.

---

### 1. Veteran-related business questions surfaced so far, ordered by alignment with product brief KPIs

*Open with an italicized sentence referencing the product brief's goal of identifying and prioritizing the top 5 veteran-related business questions through stakeholder interviews, and note that questions are ordered by how directly each can be addressed by a CXDM semantic model or leadership dashboard.*

For each business question:
- Bold header framed as a question (e.g., **Q1: Why are veterans contacting VA, and is that changing over time?**). Only include a clause like "and is that changing over time" if a stakeholder actually raised that angle, don't extend the scope of a question beyond what was discussed just because it sounds like a natural follow-on. If it's a reasonable next question nobody has raised yet, put it in Follow-up Needs instead.
- One sentence describing what answering it would enable
- Source citations and an accurate count of how many participants actually raised this specific framing, not just the general subject area

Order questions by how directly each can be addressed by a CXDM semantic model or leadership dashboard, using this priority logic:
1. Questions answerable with a semantic model buildable from data already in CXI
2. Questions that would make strong candidates for one of the 2 leadership dashboards the product brief targets
3. Questions that require cross-center CRM linkage or additional data joins
4. Questions that are externally blocked (e.g., dependent on Genesis transcript API access)

---

### 2. What the interviews tell us, taken together

*Open with an italicized sentence framing these as cross-participant patterns, things that showed up across multiple interviews, not just one, and note that with a small number of interviews these are directional signals to prioritize, not statistically validated trends.*

Write 3-4 themes (a 5th is fine if there's a genuine counter-example worth preserving per the rigor rules above). Each theme gets:
- A bold, conversational header that captures the insight (not just a topic label)
- 2-3 sentences of explanation grounded in specific participant observations. Where participants diverge in tone or conclusion on the same topic, say so by name rather than blending them into one voice.
- Name references in last name + first initial format

Good themes name a tension, a gap, or a shift, not just a topic. "Trust in the data layer is fragile and unevenly distributed" is a theme. "Data quality" is not.

---

### 3. Suggested tasks to advance CXDM KPIs

*Open with an italicized sentence framing these as suggested next steps grounded in what stakeholders shared, ordered by how directly each advances an existing CXDM product brief KPI.*

Write no more than 5 tasks. Each task gets:
- A bold header in the format **[KPI name] → [task description using a soft action verb]**. Lead with the KPI so the connection to CXDM's existing mandate is the first thing a reader sees, not the deliverable. Use verbs like `Coordinate`, `Scope`, `Prioritize`, `Validate`, `Prepare` — not `Build` or `Create`, which imply a new project rather than a natural next step.
- A short paragraph explaining why this task is warranted, what it would advance, and what the immediate action is, grounded in participant evidence. When referencing a specific participant, include a timestamp in parentheses so it's traceable: e.g., "D. Borden (06:25) has to manually remind leadership..." If a task rests on a single stakeholder's account, say so explicitly.

Rank tasks by impact on the immediate roadmap, not by difficulty. The highest-ranked task is what the Executive Summary's bottom-line callout should point back to.

---

### 4. Data definitions

*Open with an italicized sentence referencing the product brief's goal of documenting 100% of discovered definitions in a centralized knowledge base.*

For each term that surfaced:
- **Term name** as the bold header
- How it's defined, by whom, and any inconsistencies across teams. If different stakeholders hold genuinely different postures toward a term or concept (not just different definitions), that's worth capturing here too, it's often the same divergence noted in Section 2, restated concisely.
- Source citations

Prioritize terms where different teams define the same concept differently, these are the highest-value entries for the data dictionary.

---

### 5. Manual workarounds

*Open with an italicized sentence referencing the product brief's goal of replacing manual processes with semantic layers and conditioned datasets.*

One bullet per workaround. Format: `**Short label (A. LastName timestamp):** Description of the manual process and why it exists.` Include the timestamp, not just the name, same reasoning as the citation density rule above: a reader should be able to trace the claim back without cross-referencing another section. If a participant mentioned an in-progress fix to a workaround (a migration, an integration being built), note it and cite it too, since it affects how urgently CXDM needs to solve the same problem.

---

### 6. Trust issues

*Open with an italicized sentence referencing the product brief's stakeholder satisfaction KPI.*

One bullet per trust issue, cited with `(LastName timestamp)`. Be specific, name what data, what discrepancy, or what behavior caused the doubt. If the stakeholder who raised the issue still had open uncertainty about it themselves (hadn't personally verified a fix, wasn't sure of a number), keep that uncertainty in the bullet rather than resolving it on their behalf.

---

### 7. Quotes

*Open with: "Candid moments worth preserving."*

Block-quote format, attributed as `— F. LastName` (first initial, last name).

Select quotes that capture a pain point, a success metric, or a moment of candor that numbers alone wouldn't convey.

---

### 8. Follow-up needs

*Open with an italicized sentence referencing the product brief's goal of identifying and prioritizing the top 5 veteran business questions through continued stakeholder interviews.*

Two parts:

**Open questions** — things that came up and need more digging, including any reasonable follow-on question that occurred to you while writing (like "does this shift with policy events?") but that no stakeholder actually raised yet. One bullet per question, noting which participant it came from, or noting that it's a synthesizer-proposed follow-up rather than something a stakeholder said.

**Recommended next contacts** — a table with columns: Name | Role | Why
Use F. LastName format for names. Include email if mentioned in the transcript.

## Quality check before finalizing

Before saving the synthesis, re-read it once specifically looking for these failure modes, they're the ones a careful client-side reviewer would catch first:

1. Every "all N participants" or "both" claim: trace it back to the actual cited timestamps and confirm each source really makes that specific claim, not just a related one.
2. Every sentence anywhere in the document (not just Section 1 and Section 3) that attributes a specific claim, behavior, or quote to a named person: confirm it has its own `(LastName timestamp)` citation, not a citation borrowed from an earlier sentence in the same paragraph or bullet.
3. Every timestamp citation: confirm it matches an actual section header in that participant's transcript.
4. Every claim that started as a hedge in the transcript ("I think," "I'll double-check," "I'm not certain"): confirm the hedge survived into the synthesis.
5. Every theme spanning multiple participants: confirm it doesn't erase a real difference in tone or conclusion between them.
6. The single most decision-relevant recommendation: confirm it's surfaced in the scope note at the top, not just buried in its ranked position in Section 3.