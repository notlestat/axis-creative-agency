---
name: axis-creative-agency
description: Run an internal advertising agency workflow in Codex, from client intake and sourced research through five campaign concepts, human approvals, art direction, Melius production briefs, asset review and an Axis handoff. Use for creative campaign planning and evaluation, not media generation, ad-account management or post-production.
---

# Axis creative agency

The user is the final Creative Director. Treat Melius as the production department and Axis as the separate post-production department. Work in the user's agency workspace, not inside the installed skill's client folders. The skill root contains tools, workflows and templates; pass the active workspace to tools with `--root`.

Read [AGENTS.md](AGENTS.md) once. Start by locating the client and campaign, then run `python3 <skill-root>/tools/agency.py --root <workspace> status <client> <campaign>`. If new, use `create-client` and `start-campaign`. Read the client's `client.yaml`, relevant `knowledge/` files and campaign artifacts. Ask only for missing information that changes the work.

## Route by phase

Load only the workflow for the current phase and the specialist it calls for. Templates are output contracts, not filled answers. `prepare` creates drafts; Codex must do the research and creative work, fill them, then set `status: READY_FOR_REVIEW` when complete.

| User request | Workflow | Lead |
|---|---|---|
| Create client, start campaign, intake | [intake](workflows/intake/WORKFLOW.md) | Agency intake |
| Run research | [research](workflows/research/WORKFLOW.md) | Evidence-led researcher; persona only if needed |
| Build creative brief | [strategy](workflows/strategy/WORKFLOW.md) | Strategy; positioning only if needed |
| Give me five concepts | [creative](workflows/creative/WORKFLOW.md) | Axis creative director; performance pass after ideas |
| Develop concept, build art direction | [art direction](workflows/art-direction/WORKFLOW.md) | Requires concept approval; image direction |
| Storyboard it | [storyboard](workflows/storyboard/WORKFLOW.md) | Requires art approval; video direction |
| Write copy | [copy](workflows/copy/WORKFLOW.md) | Performance creative, preserving the concept |
| Prepare for Melius | [production](workflows/production/WORKFLOW.md) | [Melius adapter](skills/melius-production/SKILL.md) |
| Review generations, iterate | [review](workflows/review/WORKFLOW.md) | Concept + visual review, then performance lens |
| Prepare approved shots for Axis | [handoff](workflows/handoff/WORKFLOW.md) | Handoff document only |
| Record results or feedback | [learnings](workflows/learnings/WORKFLOW.md) | Append evidence to client memory |

## Approval discipline

After five concepts, present summaries, strengths, weaknesses, ten scores and a recommendation, then STOP. Accept an explicit decision such as `APPROVE CONCEPT 03`. Do not choose on the user's behalf.

Art direction, storyboard and shot list each need explicit human approval before production preparation. `APPROVE ART DIRECTION`, `APPROVE STORYBOARD`, `APPROVE SHOT LIST` and `APPROVE ASSETS` are the other exact command phrases. Natural-language approvals with equally clear intent can be clarified into a record, but never invented. Read [commands](references/commands.md) for recording authentic decisions.

If work changes, inspect `status` and obtain renewed approval of affected material. Generate no media or paid calls. Deliver a generation plan with unknown credit prices labelled UNKNOWN. No Melius documentation means universal prose briefs, never invented syntax. Before production, inspect `references/melius/` and project-supplied docs.

## Evidence and review

FACT needs a source. OBSERVATION describes something actually inspected. INFERENCE cites its premises. HYPOTHESIS includes a validation plan. A client-supplied statement is attributed, not independent verification. Research assumptions in a mock campaign remain labelled MOCK/HYPOTHESIS and cannot become testimonials or performance evidence.

Review only accessible assets. Mark unavailable criteria NOT_ASSESSED, not PASS. Predictions about stopping power are judgments, not measured CTR/CPA/ROAS. Human selection determines which reviewed assets reach the handoff.

Source provenance and integration changes are in [the source audit](references/source-audit.md). Read only the applicable specialist entry point. The Creative Director and visual methodology are adapted from Serge Shima, with notices in each skill. Performance material is adapted from James Praise under MIT. AdKit is a separately installed internal-only reference and is excluded from distributable packages.
