---
name: spoon-feed
description: Generate a 60-second structured summary of input material with interactive drill-down. Evolves what to include based on past conversations.
---

## Process

1. Read the input material provided by the user
2. Apply obfuscation rules to sanitize sensitive data before processing
3. Identify the problem type (trade-off analysis, new concept, methodology, process, architecture, etc.)
4. Check Learned Heuristics below for problem-type-specific guidance
5. Generate a 60-second structured summary using the Default Summary Format
6. Present the summary to the user
7. Offer drill-down into any section — always be ready for interactive follow-up
8. Answer follow-ups with further research as needed
9. When the user concludes, remind them to run /archive to capture learnings

## Default Summary Format

- One-line purpose statement: what is this and why does it matter
- 3-5 key takeaways: the core ideas distilled
- Implications: "so what does this mean" for practical work
- Open questions: areas worth drilling into

## Obfuscation Rules

Before processing any input material:
- Replace company names, product names, internal project names with generic equivalents (e.g., "CompanyX", "ServiceA", "ProjectAlpha")
- Remove internal URLs, links to internal tools, internal ticket references
- Never include code snippets in any output or stored file
- Generalize specific metrics to directional statements (e.g., "latency increased by 340ms" -> "latency increased significantly")
- Replace people's names with roles (e.g., "the tech lead", "the reviewer", "the oncall engineer")

## Learned Heuristics

<!-- /archive appends patterns here as the skill evolves -->
<!-- When a heuristic exceeds ~3 lines, extract to heuristics/spoon-feed/<topic>.md and reference it here -->
