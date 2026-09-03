# Daily commands

Use `python3 tools/agency.py` from the repository. From an installed skill use its absolute script path and `--root /path/to/agency-workspace` before the subcommand.

```sh
python3 tools/agency.py create-client acme --name 'Acme'
python3 tools/agency.py start-campaign acme launch --name 'Product launch'
python3 tools/agency.py prepare acme launch research
python3 tools/agency.py prepare acme launch strategy
python3 tools/agency.py prepare acme launch concepts
python3 tools/agency.py status acme launch
```

Preparation creates the appropriate draft files without overwriting existing work. Codex fills the drafts using the phase workflow. DRAFT means unfinished. READY_FOR_REVIEW means the work is ready for human review, not approved. Required sections must be substantive. Optional unknowns stay UNKNOWN with a reason.

After a real user decision, save the exact message to a text file and record it:

```sh
python3 tools/agency.py approve acme launch concept --choice 03 --by Corey --evidence-file /path/to/actual-user-message.txt
python3 tools/agency.py prepare acme launch art-direction
python3 tools/agency.py approve acme launch art-direction --by Corey --evidence-file /path/to/art-approval.txt
python3 tools/agency.py prepare acme launch storyboard
python3 tools/agency.py approve acme launch storyboard --by Corey --evidence-file /path/to/storyboard-approval.txt
python3 tools/agency.py approve acme launch shot-list --by Corey --evidence-file /path/to/shot-list-approval.txt
python3 tools/agency.py prepare acme launch copy
python3 tools/agency.py prepare acme launch production
```

Approval phrases are `APPROVE CONCEPT 03`, `APPROVE ART DIRECTION`, `APPROVE STORYBOARD`, `APPROVE SHOT LIST`, `APPROVE ASSETS`. The tool stores the message, reviewer, time and hashes of the reviewed files. It cannot authenticate who typed the message. Agents must never manufacture the evidence file.

Complete `06_storyboard/shot-plan.json` alongside the human-readable storyboard and shot list. It is the checked source for shot durations and generated Melius shot briefs. Populate every field, keep shot IDs unique, and make durations sum to campaign duration. `prepare production` blocks on incomplete data and stale approvals.

```sh
python3 tools/agency.py prepare acme launch review
python3 tools/agency.py approve acme launch assets --by Corey --evidence-file /path/to/assets-approval.txt
python3 tools/agency.py prepare acme launch handoff
python3 tools/agency.py learn acme launch --file /path/to/results-or-feedback.md
```

For asset review, fill `09_review/asset-reviews.json`. Use relative paths beneath `08_generations/`. Every reviewed asset must exist; capture its SHA-256 using `python3 tools/agency.py asset-hash <path>`. Human-selected assets must have PASS and assessed scores on every criterion. PASS WITH CHANGES needs a new reviewed file before handoff. Handoff never invokes Axis.

Client learnings are append-only and include the campaign and time. For metrics, record platform, dates, attribution window, denominators, source and sample limitations. Reimporting the same text for the same campaign is idempotent.
