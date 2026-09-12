# Example run: auditing the tenant usage dashboard

A worked example of this skill's output, on a fictional surface: the wave-2 usage panel from the
governed-build-loop skill's
[example contract](https://github.com/FortunaTerra-Group/goal-contract/blob/main/plugin/examples/example-run.md)
("add per-tenant rate limiting to the public API", Acme Metrics API). The contract's slice (d) is
a read-only panel showing each tenant's current usage against their limit; limits are changed
through the separate admin API in slice (c), not on this panel.

**Persona source.** The contract and the product's own docs contain no persona for this panel.
That absence is finding 0 below. The walk assumes the customer's own engineering lead, checking
whether their integration is close to being throttled, and every finding that depends on that
assumption says so.

## Executive read (top 5 by severity)

0. **[0 · Help and documentation] Whole surface.** No documented target user. Every persona
   judgment below is an assumption; the product should say who this panel is for.
1. **[3 · Error prevention] Usage panel, unlimited-tier tenants.** A tenant on the unlimited
   tier is rendered against a limit of `0`: the bar reads full, the figure reads `NaN%`, and the
   copy says "over limit." The one question the panel exists to answer comes back wrong for the
   customers least likely to expect it. Severity 3 because the task's answer is wrong, not
   merely hard to find.
2. **[2 · Visibility of system status] Usage panel.** The usage bar is a snapshot fetched on
   page load; nothing indicates the data's age, so a lead watching it during an actual traffic
   spike sees a graph that looks calm because it is minutes stale.
3. **[2 · Match to the real world] Usage panel.** The limit is shown as a bare number, no unit
   and no window length; a reader cannot tell requests per second from requests per minute
   without the documentation. (Persona-dependent: an engineering lead will look for the unit
   first.)
4. **[2 · Consistency and standards] Usage panel vs. admin API.** The panel calls the number
   "Rate limit"; the admin API in slice (c), its docs, and its error message call the same field
   `throughput_cap`. A lead who reads the panel and then calls the API has to work out that they
   are the same number.
5. **[1 · Recognition over recall] Usage panel.** The "% of limit used" figure requires the
   reader to already know their raw request volume to sanity-check it; showing the raw count
   next to the percentage removes that recall burden.

## Full findings

| Heuristic | Screen | What a user experiences | Severity |
|---|---|---|---|
| Help and documentation | Whole surface | No stated target user; persona judgments are assumptions | 0 |
| Error prevention | Usage panel, unlimited tier | Full bar, `NaN%`, "over limit" for a tenant with no limit | 3 |
| Visibility of system status | Usage panel, usage bar | No timestamp or "as of" marker on a page-load snapshot | 2 |
| Match to the real world | Usage panel, limit figure | No unit or time window on the limit | 2 |
| Consistency and standards | Usage panel vs. admin API | Same field named "Rate limit" here and `throughput_cap` there | 2 |
| Recognition over recall | Usage panel, usage bar | Percentage shown without the raw numbers it is computed from | 1 |
| Help and documentation | Usage panel | Nothing says what happens at the limit (which status code, when the window resets) | 1 |

## Quick-win vs. structural split

**Quick wins** (copy, label, or UI-state changes, no new data flow):
- Add the unit and window length to the limit figure (finding 3).
- Use one name for the field across the panel, the admin API, and its docs (finding 4).
- Show the raw request count next to the usage percentage (finding 5).
- Add one line of copy stating the status code at the limit and when the window resets.

**Structural** (need a data or state change):
- A distinct "no limit" state for unlimited-tier tenants, driven by the tier, not by a `0`
  (finding 1). This is the severity-3 item and it needs a decision about what the panel shows
  such a tenant, not just a copy change.
- A "last updated" indicator wired to the actual fetch timestamp, or live refresh if the data
  supports it (finding 2).
- A written target user for the surface (finding 0).

## Handoff pointers

- Finding 1 (unlimited-tier state): design plus engineering, since it needs both a decision
  about the display and a data path that carries the tier.
- Findings 3, 4, 5 and the status-code copy: a one-sprint engineering fix, no design review needed.
- Finding 2 (staleness indicator): engineering, contingent on whether the data pipeline can
  report a freshness timestamp at all.
- Finding 0: product, before the next audit of this surface.

---

This report is advisory input only. It names the violations and their severity; the fix for
each belongs to whoever owns that surface.
