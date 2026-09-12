---
name: usability-heuristic-review
description: >
  Inspect an already-shipped UI surface and report what's wrong with the experience as a real
  user meets it, using Jakob Nielsen's 10 usability heuristics with mandatory severity scoring,
  a cross-surface consistency audit, and a persona-resonance check. Produces a findings report
  only, never new flows, wireframes, or redesigns. Use for a pre-launch polish pass, a
  post-launch experience-debt audit, or a second opinion before investing design effort in a
  redesign.
---

# Usability heuristic review: critique the shipped experience, not the spec

## Purpose

Inspect an **already-shipped** product surface and report what's wrong with the experience as
a real user meets it: coherence breaks, dissonance, dated versus modern treatment, iconography
drift, and whether the experience actually serves its intended user. This is a purely
evaluative skill. It produces a severity-ranked findings report, never new flows, wireframes,
tokens, or a redesign. It's the mirror held up to design and engineering after the work ships.

This is **not** UX research (no studies with real users; expert inspection instead), **not**
UX design (no flows or IA), and **not** UI design (no visuals or a token system). It evaluates
the output of all three.

Grounded in Jakob Nielsen's heuristic evaluation method (Nielsen and Molich, 1990): a small
number of expert evaluators inspecting a live interface against named principles find most of
the real usability problems at a fraction of the cost of a user study. One evaluator finds a
minority of them; run the skill more than once, or with more than one persona, when the surface
matters.

## Use when

- A surface already has a working UI and you need an honest read on experience quality.
- Inconsistency is suspected across screens, surfaces, or platforms.
- The UI feels "dated" or "off" and that intuition needs to become specific, citable findings.
- Iconography, terminology, or visual language has drifted as features accreted.
- You need to validate whether the live experience actually serves its intended user, not the
  team's own mental model of the product.
- A pre-launch or pre-demo polish pass, or a post-launch experience-debt audit.
- A second opinion is needed before investing design or engineering effort in a redesign.

## Priorities

1. **Evaluate as shipped.** Judge the live, real surface a user touches, not the spec or the
   design intent behind it.
2. **Name the violation.** Every finding cites a specific heuristic; "feels wrong" is not a
   finding.
3. **Severity over volume.** Rank by user impact, not by how many nits can be listed.
4. **Persona resonance.** Measure the experience against the *target* user's context,
   literacy, and goals, not a generic user.
5. **Coherence across surfaces.** The same concept, icon, term, and pattern must mean the
   same thing everywhere it appears.

## Required behaviors

### Heuristic sweep (Nielsen's 10, applied per screen or route)
Visibility of system status; match to the real world; user control and freedom; consistency and
standards; error prevention; recognition over recall; flexibility and efficiency; aesthetic and
minimalist design; help users recover from errors; help and documentation.

Each violation: `[heuristic] · [screen/route] · [what a user experiences] · [severity 0-4]`.
Dissonance and iconography findings still cite one of the ten (dissonance usually lands under
match to the real world; icon drift under consistency and standards).

### Severity scale (mandatory on every finding)
This is FortunaTerra's scale, not Nielsen's published severity ratings; the range is the same
and the anchors differ (his 0 is "not a problem" and his 4 is "usability catastrophe"). State
which scale a report uses if it will be read alongside a classic heuristic evaluation.
- **0** cosmetic: fix if time permits
- **1** minor: low-frequency irritation
- **2** major: frequent, or blocks some users
- **3** catastrophic: blocks task completion, or makes the task's answer wrong
- **4** brand or trust damage

### Coherence and consistency audit
Cross-surface inventory: does the same action map to the same label, icon, placement, and
outcome across every surface the product ships? Flag terminology drift, duplicated but
divergent components, and inconsistent empty, loading, and error states.

### Modernity and iconography
Identify dated patterns (skeuomorphic leftovers, mismatched icon sets, inconsistent corner
radii, shadows, or motion, legacy color treatments). Check whether the icon set is internally
consistent, legible at size, and conventionally legible to the target user.

### Persona-resonance check
Name the target user for the surface (pull from the product's own persona or user documentation;
never invent one). Walk the primary task as that user: is the language, density, tone, and
affordance set actually resonant and helpful to them, or built for the team's own literacy?
Flag mismatches as dissonance findings.

### Output contract
Deliver a single findings report: an executive read (top 5 by severity), then a full table
(heuristic, surface, severity, evidence), then a quick-win versus structural split, then handoff
pointers (which finding belongs to design and which to engineering). Findings are observations
and recommendations only, advisory input to whoever owns the fix.

## Avoid

- Designing the fix. Name the problem and its severity; the fix belongs to design and engineering.
- Running user studies or claiming user data. This is expert inspection, not research.
- "Feels dated" or "looks off" without a named heuristic, a specific screen, and a severity.
- Critiquing the spec or mockup instead of the live shipped surface.
- Persona-blind critique: generic best-practice nits divorced from who the product is for.
- Severity inflation. If everything is catastrophic, nothing is.
