# Axis creative agency

An internal Codex workflow for advertising research, strategy, campaign ideas, art direction, Melius briefs and creative review. You make the final creative decisions. Melius makes the assets. Your separate Axis post-production workflow receives the approved handoff.

## Daily use

Open this project in Codex and say:

1. "Create client Acme." Add brand assets under `clients/acme/brand/`.
2. "Start a campaign for Acme's new product." Complete the intake.
3. "Run research." Sources and assumptions are recorded separately.
4. "Build the creative brief." Previous client learnings are read first.
5. "Give me five campaign concepts." Review summaries, scores and tradeoffs.
6. "APPROVE CONCEPT 03." Codex may now develop art direction.
7. "APPROVE ART DIRECTION." Codex may now storyboard it.
8. Review and separately approve the storyboard and shot list.
9. "Prepare it for Melius." Review copy, shot briefs and the generation plan, then generate in Melius yourself.
10. Put outputs in `08_generations/` and say "Review these Melius generations."
11. Select passing assets and say "APPROVE ASSETS."
12. "Prepare the approved shots for Axis." Receive a handoff document.
13. "Record these results and client feedback." The learning history grows without overwriting earlier notes.

"Develop concept 3" means refine it. It does not select a winner. The mock campaign intentionally stops before approval.

## Start here

Read [the fictional mock comparison](examples/fieldnote/clients/fieldnote/projects/one-line/04_concepts/concept-comparison.md). All customer insights and product details in it are declared fictional assumptions, not research findings. No Melius credits were used.

Use `$axis-creative-agency` after installing the skill. The project also works directly from its `AGENTS.md`. The installed package is self-contained; point it at your chosen workspace for client files.

```sh
python3 tools/install_skill.py
python3 tools/agency.py create-client acme --name 'Acme'
python3 tools/agency.py start-campaign acme launch --name 'Product launch'
python3 tools/agency.py status acme launch
```

Requires Python 3.9 or newer. Runtime tools use only the standard library. [Exact commands and approval records](references/commands.md) explain the operational details. [SKILL.md](SKILL.md) routes normal conversation into the relevant phase.

## What lives where

| Location | Purpose |
|---|---|
| `clients/<client>/client.yaml` | Client facts, voice, constraints and preferences |
| `clients/<client>/brand/` | Logos, guidelines, product files, assets and references |
| `clients/<client>/knowledge/` | Brand, audience, positioning, competitors, campaigns and append-only learnings |
| `clients/<client>/projects/<campaign>/` | Intake through approved handoff |
| `workflows/` | One operating guide per phase |
| `templates/` | Complete brief, research, concept, treatment, storyboard, production and review contracts |
| `skills/` | Adapted specialist entry points and attributed source methodology |
| `references/melius/` | Supplied Melius documentation, if available |
| `.local/skills/axis-meta-context/` | Separately installed internal-only AdKit material |

Campaign folders follow the requested 01-10 structure. `07_copy/` and `07_melius/` both exist because the brief names both. Their order is governed by the workflow, not alphabetical sorting.

## Approval and generation limits

The CLI creates drafts and checks files; Codex performs the thinking. It does not claim that a template is completed research. Files must be filled and marked READY_FOR_REVIEW before approval recording. Approval messages, timestamps, reviewer names and hashes are retained. Changed inputs invalidate approvals. This is a local workflow record, not proof of identity or an access-control system.

Melius preparation requires concept, art direction, storyboard and shot-list approvals. A checked JSON shot plan drives the per-shot briefs and planned attempt caps. No Melius docs were supplied, so the adapter uses universal prose and records unknown capabilities/costs. No tool spends credits, launches ads, sends messages or invokes Axis.

## Sources and licensing

Seven bundled specialist adaptations use [Serge Shima's creative director](https://github.com/smixs/creative-director-skill), [Serge Shima's visual skills](https://github.com/smixs/visual-skills) and [James Praise's marketing skills](https://github.com/realjaymes/marketingagentskills). Their licences and notices are retained. See [source audit](references/source-audit.md) and the pinned [source manifest](references/skill-sources.json).

[AdKit's Meta strategy](https://github.com/adkit/ads-skills) is installed separately for internal reference. Its licence restricts redistribution, so its contents are excluded from Git and the skill package. `python3 tools/install_meta_context.py` installs the pinned internal dependency on another machine. Existing local installations are preserved.

Client data is ignored by Git. The distributable package includes only the fictional example. Keep confidential Melius documentation under `.local/melius/`. Existing generic image/video/marketing skills are not overwritten.

## Verification

The runtime has no third-party dependencies. For contributor linting and YAML/skill validation, install `requirements-dev.txt` in an isolated environment.

```sh
python3 -m unittest discover -s tests -v
PYTHONPYCACHEPREFIX=/tmp/axis-agency-pycache python3 -m compileall -q tools tests
ruff check tools tests
ruff format --check tools tests
python3 tools/validate.py
python3 tools/package_skill.py
```

The tests exercise blocked approvals, stale input detection, timing validation, asset checks, learning history and a synthetic handoff. Synthetic fixture approvals never enter the mock campaign. The mock is a worked intake-to-concepts example awaiting your decision.
