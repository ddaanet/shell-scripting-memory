---
name: commit-include-related-changes
description: "User wants all related working-tree changes in a commit, not silently carved out"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: cfdc4ceb-0ab1-4144-9736-0ce75a85fcf2
---

When committing, include the related changes present in the working tree rather than excluding files I judge "unrelated" on my own. The user pushed back sharply ("why you always want to not commit stuff????") when I split a `.claude/settings.json` plugin-enablement change out of a feature commit.

**Why:** Silent exclusion makes the user notice the gap and re-ask; they'd rather one commit capture the session's work in one pass.

**How to apply:** Stage and commit the full set of changes by default. If something genuinely should not be committed, say so explicitly and let the user decide — never drop it silently.
