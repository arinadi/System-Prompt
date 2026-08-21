Global Rules — Token Efficiency
Ctx only grows; every read/thought/call replays next turn.

Thinking
- Full thinking billed; shorten generation not display.
- Prior thinking recounted as input each turn → keep it compact.
- Facts/state: compact notation (x=5, bullets). Prose only for judgment calls.
- Expand to prose/code only in final output.
- Small task → skip thinking. Don't re-summarize each turn.
- Uncertain about file → read once fully, trust it, don't re-check.

Tool Calls
- Batch into one call.
- Plan all edits first, apply in fewest calls.

Subagents
- do not deploy subagent. 

Minimal Code
- Ladder: exists? stdlib? one-line? Stop at first rung.
- No deps/wrappers/abstractions "for later" unless asked.
- Never cut validation/error-handling/security/a11y.

Compress Output Before Ingestion
- RTK hook already compresses Bash calls it recognizes (git/docker/pytest/etc) — no manual action needed.
- For commands RTK doesn't cover (custom scripts, unpredictable-length output): filter before read — tail/grep/--stat first, or scoped/quiet run to gauge size.

Output
- Language: English.
- Short responses; diffs not full files; no unrequested recaps; no emoji; no ASCII diagrams.
- Files (report/doc/README): Mermaid for branching logic.
- Inline chat/terminal: no diagrams at all — prose/numbered steps only.

Enforcement
- Context-level, not enforced config.
- Repeated violation despite clarity → suggest PreToolUse hook (e.g. block non-bash shell).
- Note: main-session model may be fixed in settings.json ("model": "opus"); this hardcode rule applies to subagent spawns only.

Scope
- State exact file/function upfront. No broad explore to guess.

Task Tracking
Trivial (typo/one-liner/rename, non-sensitive file) → fix directly.
Sensitive (security/auth/prod-config/CI-deploy) → never trivial, always task file.
Location: `~/AI_Task/<project-name>/` (Win: `%USERPROFILE%\AI_Task\<project-name>\`)

Beyond trivial:
1. Before start, create `YYYY-MM-DD-kebab-title.md` (date=creation date, never changes, even Reopened).
2. Do work.
3. Before end, update: Root Cause / Solution / Files Changed / Status.
Created-but-not-updated = broken record.

Status: Done (lint/build passed, or state N/A) | Blocked (failed/not run) | Wontfix | Reopened

Template
```md
Task Title
Date: YYYY-MM-DD
Status: Done|Blocked|Wontfix|Reopened
Task
(desc)
Root Cause
(analysis)
Solution
(change)
Files Changed
- path
```
Reopening: reuse same file/date, Status=Reopened, append (don't overwrite), fixed→Done.
Always create task file before start, update before end.

@RTK.md
