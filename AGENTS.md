## Project Purpose

This project is for preparing and refining an article about edge computing
architectures. The initial source document will be produced by other tools and
placed in this directory. Codex should help process, restructure, verify, and
improve that document while preserving the author's intent.

## Workspace Boundaries

- Treat this directory as the full project boundary.
- Do not read, write, move, copy, or inspect files outside this directory unless
  the user explicitly approves it for a specific action.
- Read commands inside this directory are allowed.
- Git read commands are allowed.
- Do not run potentially harmful commands without explicit user approval.
- Do not delete files, reset Git state, clean the working tree, or overwrite
  user changes without explicit user approval.
- Git may be initialized for this directory, but do not commit unless the user
  explicitly approves the commit.

## Command History

- Maintain `command-history.md` at the project root.
- Document every user prompt verbatim in `command-history.md`.
- Document every command executed in this project in `command-history.md`.
- Keep the history as a single chronological log.
- Append each new prompt and command as the next chronological entry.
- Each entry must be one of two types:
  - `User Prompt`: the user's prompt text, copied verbatim.
  - `Executed Command`: shell or tool command run in response to the work.
- Update the history during each turn when commands or prompts are handled.
- Do not remove previous history entries unless the user explicitly requests it.

## Document Workflow

- Expect the main article draft to be added later by other tools.
- Before editing a document, inspect its format, structure, and existing style.
- Preserve the user's terminology unless there is a clear technical or editorial
  reason to change it.
- Keep edits focused on the requested task: structure, clarity, technical
  accuracy, citations, consistency, formatting, or publication readiness.
- Do not introduce unrelated rewrites, new sections, or broad stylistic changes
  unless requested.
- When making substantial edits, explain the editorial intent briefly.
- Prefer small, reviewable changes over large opaque rewrites.

## Article Standards

- Maintain a technically rigorous tone suitable for an article on edge computing
  architectures.
- Distinguish clearly between cloud, edge, fog, device, gateway, and hybrid
  deployment models.
- Watch for ambiguity around latency, bandwidth, data locality, orchestration,
  resilience, security, privacy, and operational cost.
- Flag claims that need evidence instead of silently strengthening them.
- Do not fabricate citations, standards, benchmarks, statistics, or quotes.
- If current facts, product capabilities, standards, or market claims are needed,
  verify them before using them.

## Source And Citation Handling

- Preserve existing citations and bibliography entries unless asked to change
  citation style.
- If citations are missing, mark evidence gaps clearly rather than inventing
  references.
- When adding source-backed claims, include enough citation detail for later
  verification.
- Prefer primary sources for technical claims: standards bodies, official
  documentation, peer-reviewed papers, vendor architecture documents, or
  reputable industry reports.
- Keep direct quotations short and only use them when wording matters.

## File And Format Handling

- Preserve the existing file format unless the user asks for conversion.
- For Markdown, keep headings consistent and avoid unnecessary formatting churn.
- For word-processor exports or generated documents, avoid manual edits that
  corrupt metadata or formatting.
- For structured files, use appropriate parsers or format-aware tools when
  practical.
- Do not rename the main draft or generated assets without asking.

## Collaboration Notes

- The user is preparing the initial document with other tools, so expect new
  files or user edits to appear between turns.
- Treat unexpected changes as user work. Do not revert them.
- When the next step is unclear, make a conservative assumption and state it.
- Ask before making destructive, broad, or irreversible changes.
- Keep final responses concise and include what changed, what was checked, and
  any remaining risks or follow-up options.
