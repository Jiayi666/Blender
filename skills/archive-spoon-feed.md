---
name: archive-spoon-feed
description: Archive logic specific to spoon-feed sessions. Called by archive.md dispatcher.
---

## Process

This sub-skill is invoked by [archive.md](archive.md). Follow the shared archive logic (Sanitize, Store, Learn) with these spoon-feed-specific additions:

### Sanitize

Follow shared obfuscation rules from archive.md. Additionally:
- Ensure the original source material reference is generalized (e.g., "an internal design doc about caching" not the actual doc title/URL)

### Store

Follow shared store logic. When writing the compact file, pay special attention to:
- What summary format was used (structure, length, ordering of sections)
- Which sections the user drilled into
- How many follow-ups before the user was satisfied

### Learn

When analyzing the conversation, focus on signals specific to spoon-feed:
- **Summary structure preferences**: Did the user want a different ordering? More/fewer takeaways?
- **Depth calibration**: Was the initial summary too shallow or too detailed for this problem type?
- **Anticipation gaps**: What follow-up questions could have been answered proactively in the summary?
- **Problem type patterns**: Does this problem type warrant a different summary format than the default?

Update `skills/spoon-feed.md` Learned Heuristics with findings. Pattern format:
```
- For <problem type>: <specific guidance>
```
