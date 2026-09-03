# MVP verification

Verified locally on 2026-09-03.

- 25 unit tests passed with the system Python 3.9. Synthetic fixtures exercised prerequisites, explicit approval messages, changed material, shot duration validation, generation plans, stale packages, asset hashes, incomplete review, final handoff and append-only learning history.
- Compile checks passed for the maintained tools and tests. Cache output was directed to a temporary directory because Apple's system Python defaults to a restricted user cache location.
- Ruff 0.16.5 lint and formatting checks passed. PyYAML 6.0.3 parsed the client profiles and skill UI metadata. These development packages were installed in a temporary environment; the agency runtime uses only the standard library.
- The official Codex skill-creator validator accepted the main skill and all eight bundled specialist/adapter entry points.
- The agency validator checked the nine skill entry points, referenced templates, maintained links, licences/notices and package exclusions.
- A temporary installation ran client creation, campaign creation, status and bundle validation using its own tools/templates outside the repository.
- The fictional Fieldnote campaign contains completed intake, seven research/assumption records, a creative brief, five concepts, comparison and method notes. Concept approval is PENDING. Attempting art direction was blocked. Later campaign phases contain only empty directory markers.
- No Melius generation, paid media execution, outreach or Axis post-production invocation occurred.

These checks verify local workflow behaviour and packaging. They do not establish campaign effectiveness, originality clearance, real customer evidence or Melius API capabilities. The mock contains no measured campaign results. Human approval evidence is a local record, not an authenticated identity system.

AdKit's restricted contents are present only under the ignored .local directory. Runtime client data is ignored. The packaged example is explicitly fictional.
