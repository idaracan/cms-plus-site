---
name: remember
description: Capture learnings into .claude/knowledge/ using Narrative Anchors
---

# Remember

Use after any non-trivial task to persist what was learned.

## Steps

1. Identify which category the learning belongs to:
   - Tripwire or incident-driven → `knowledge/gotchas.md`
   - Established pattern or convention → `knowledge/patterns.md`
   - Locked decision with rationale → `knowledge/decisions.md`
   - Hard rule for writing code → `knowledge/contribution-rules.md`
   - Domain-specific knowledge → `knowledge/domains/<topic>.md`

2. Write the entry using a Narrative Anchor:
   ```
   [LABEL:value] Complete sentence explaining the finding in context.
   ```
   Example: `[DOCKER:cms-node-modules] The vet_cms_node_modules named volume must be dropped explicitly when apps/cms/package.json changes — a plain container restart reuses the stale volume.`

3. Append to the correct file. Keep `gotchas.md` under 50 lines — overflow to a domain file.

## Rules

- Never write learnings as inline code comments — they belong here
- Every entry must be a complete sentence with a Narrative Anchor
- If the entry references a specific file path or command, include it verbatim
