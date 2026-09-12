# usability-heuristic-review

**Critique the surface that shipped, not the one that was designed.**

> A Claude Code skill, Apache-2.0. The procedure is in
> [`skills/usability-heuristic-review/SKILL.md`](skills/usability-heuristic-review/SKILL.md); a
> worked findings report on a fictional dashboard is in
> [`examples/example-run.md`](examples/example-run.md). This is the public form of the Experience
> Critic role FortunaTerra runs on its own shipped products. The rest of this page is why it exists
> and how to install it.

---

Surfaces built with coding agents accrete fast, and the seams show in the same places: a label
lifted from an API field name, a loading state nobody designed, the same concept spelled three
ways across three screens. Nobody planned any of it and nothing in the plan will find it. Only
inspecting the live surface will.

This skill is an agentic application of Jakob Nielsen's heuristic evaluation method. It inspects
an already-shipped UI surface (not the spec, not the mockup) and reports what is wrong with the
experience a real user meets: violations of the ten heuristics with a mandatory severity on each,
a cross-surface coherence audit, and a check that the surface serves its documented target user
rather than the team that built it. The output is a findings report. It never proposes a
redesign.

## Install

Copy the skill into your project:

```bash
git clone https://github.com/FortunaTerra-Group/usability-heuristic-review-skill
cp -r usability-heuristic-review-skill/skills/usability-heuristic-review .claude/skills/
```

Or install it as a plugin from FortunaTerra's marketplace:

```bash
claude plugin marketplace add FortunaTerra-Group/claude-plugins
claude plugin install usability-heuristic-review@fortunaterra
```

Then invoke `/usability-heuristic-review` with the surface (URL, build, or screenshots) and a
pointer to the product's persona documentation.

## Where it fits

This is the after-the-fact lens: it looks at what shipped, not at what was planned. It pairs with
a pre-PR [review panel](https://github.com/FortunaTerra-Group/multi-persona-review-panel-skill),
which catches defects in a diff, and with a
[goal contract](https://github.com/FortunaTerra-Group/goal-contract), which says up front what done
was supposed to mean. When the three disagree, the shipped surface is the one the user met.

## Provenance and license

This is the public form of the Experience Critic role FortunaTerra runs on its own shipped
products. The method is Nielsen's; the severity scale (which differs from his published ratings,
and says so), the cross-surface coherence audit, and the persona-resonance check are how
FortunaTerra applies it. First drafted 2026-09-05 under MIT by the same author; relicensed to
Apache-2.0 and assigned to FortunaTerra Technologies Inc. 2026-09-12. Copyright 2026 FortunaTerra
Technologies Inc. Written and maintained by Vivek Iyer
([FortunaTerra-Group](https://github.com/FortunaTerra-Group)). Released under
[Apache-2.0](./LICENSE). If a finding format here let a real usability defect go unnamed, open an
issue with the surface and the heuristic it should have cited.
