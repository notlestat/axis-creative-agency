# Campaign planning and review

A file-based Codex workflow for advertising research, strategy, campaign concepts, art direction, production briefs, and creative review. You make the creative decisions. The CLI creates project files and checks workflow state.

## Open the workflow

Download or clone this repository using GitHub's **Code** menu, then open the checkout in Codex. Use Python 3.9+ for the CLI; its runtime uses the standard library.

Read [AGENTS.md](AGENTS.md), [SKILL.md](SKILL.md), and [the command reference](references/commands.md). From the checkout, inspect the available commands:

```sh
python3 tools/agency.py --help
```

To keep client work in a separate workspace, pass its path explicitly:

```sh
python3 tools/agency.py --root /path/to/workspace create-client acme --name 'Acme'
python3 tools/agency.py --root /path/to/workspace start-campaign acme launch --name 'Product launch'
python3 tools/agency.py --root /path/to/workspace status acme launch
```

Replace the sample workspace and client details before use. The tool creates drafts; filling a template does not establish completed research or approval.

## Develop a campaign

1. Supply the client facts, brief, assets, and constraints.
2. Research the audience and market, with sources and assumptions recorded separately.
3. Review the brief and five concept options.
4. Make an explicit concept decision before developing art direction.
5. Review art direction, storyboard, and shot list as separate decisions.
6. Review the production plan before generating assets.
7. Inspect generated assets, select approved work, and request the required handoff.
8. Record feedback and results in the append-only learning history.

Use [the fictional demonstration](examples/fieldnote/README.md) to inspect an intake-to-concepts example. Its customer insights and product details are labelled fictional assumptions. It has no approval ledger and is not evidence of client results.

## Project records

| Location | Purpose |
| --- | --- |
| `clients/<client>/client.yaml` | Client facts, voice, and constraints |
| `clients/<client>/brand/` | Supplied brand and product assets |
| `clients/<client>/knowledge/` | Research and append-only learnings |
| `clients/<client>/projects/<campaign>/` | Intake through handoff |
| `workflows/` | Phase instructions |
| `templates/` | Output contracts |
| `skills/` | Adapted specialist guidance |
| [Melius documentation](references/melius/README.md) | Production documentation boundary |

Approval records retain the message, reviewer, timestamp, and input hashes. Changed inputs invalidate affected approvals. The ledger is a local workflow record, not identity verification or access control.

The tools do not spend production credits, launch ads, send messages, or run post-production. Production preparation requires the recorded concept, art direction, storyboard, and shot-list approvals. Generation needs separate authority.

## Check a change

Install contributor dependencies in an isolated environment:

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements-dev.txt
```

Then check the local tools and package contracts:

```sh
python3 -m unittest discover -s tests -v
python3 -m compileall -q tools tests
ruff check tools tests
ruff format --check tools tests
python3 tools/validate.py
```

The suite uses synthetic approvals and handoffs. It does not approve a real campaign or verify a production-provider account.

## Sources and licensing

Adapted guidance comes from [Serge Shima's creative director](https://github.com/smixs/creative-director-skill), [Serge Shima's visual skills](https://github.com/smixs/visual-skills), and [James Praise's marketing skills](https://github.com/realjaymes/marketingagentskills). Preserve their notices and licenses. [The source audit](references/source-audit.md) and [source manifest](references/skill-sources.json) record provenance.

The separate [AdKit reference](https://github.com/adkit/ads-skills) has redistribution restrictions and is excluded from Git and packaged copies. Keep client data and confidential provider documents outside distributable files.
