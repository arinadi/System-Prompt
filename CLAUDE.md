# Global Rules — Token Efficiency
<!-- last reviewed: 2026-07-06 — re-check every ~90 days -->

**Every file read, thought, and tool call is replayed in full next turn. Context only grows.**

## Reading
- Grep/glob FIRST. Never open a full file to find one thing.
- Read only the needed line range.
- Never read `node_modules/`, `dist/`, `build/`, logs, or generated files unless asked.

## Thinking
- Full thinking is billed — shorten the generation, not the display.
- Prior thinking blocks are re-counted as input on later turns — verbose thinking compounds.
- Use compact notation for facts/state: `x=5; bullets`. Full sentences only for judgment calls.
- Expand to full sentences, prose, or code only in the final output — matched to what the output actually needs.
- Small task → skip thinking entirely.
- Don't re-summarize each turn — carry compact state only.

## Tool Calls
- Batch commands into one call. Each round-trip re-sends everything.
- Don't explore broadly at session start. Touch only what's relevant.
- Don't re-read a file you already confirmed unchanged.

## Subagents
- A subagent runs in its own context window — its exploration never bloats the main session.
- For open-ended work ("find where X is used"), always delegate.
- Use `general-purpose` + `model:` override:
  ```
  Agent(subagent_type="general-purpose", model="haiku", prompt="...")  # light/routine
  Agent(subagent_type="general-purpose", model="opus", prompt="...")  # heavy/reasoning
  ```
- Never hardcode provider model names. Check aliases first: `echo $ANTHROPIC_DEFAULT_SONNET_MODEL $ANTHROPIC_DEFAULT_HAIKU_MODEL $ANTHROPIC_DEFAULT_OPUS_MODEL`

## Minimal Code
- Check the ladder before writing: already exists? stdlib covers it? One line? Stop at first rung.
- No dependencies, wrappers, or abstractions "for later" — unless explicitly asked.
- Never cut validation, error handling, security, or accessibility.

## Compress Output Before Ingestion
- Filter BEFORE reading: `| tail -n 50`, `| grep -i "error|fail"`, `--stat` first.
- For unpredictable output length, run scoped/quiet first to gauge size.

## Output Language
- ALL output in English, regardless of input language.

## Output Format
- Keep responses short. Show diffs, not full files.
- No "here's everything I did" recap unless asked.

## Enforcement
- This file is context, not enforced config. If a rule is repeatedly violated despite being clear, suggest a `PreToolUse` hook to hard-block it — don't just repeat the rule.

## Scope
- State the exact file/function upfront. Don't explore broadly to guess.
