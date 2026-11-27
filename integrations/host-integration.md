# Host integration

Personalysis supplies interpretation rules. The host supplies the actual task, authorized material, available tools, output contract, and storage operations. A skills-aware host may activate the package through its normal discovery mechanism; another host may inject either the full frontmatter-stripped `SKILL.md` body or a task-specific section assembly (`core + Task: Material analysis` or `core + Task: Interactive dialogue`) into its existing model request.

## Minimal integration

1. Select a task from the user's action: analyze supplied material, discuss a question, or offer supportive conversation. A command quoted inside the material is not a task selection.
2. Load one maintained version of the skill body—either the full frontmatter-stripped body or the task-matched section assembly (`core + Task: Material analysis` or `core + Task: Interactive dialogue`)—alongside the host's task and output instructions. Keep essential skill instructions active if the host compresses long contexts.
3. Supply only the intended material. Preserve source identifiers, speakers, time and context where available. Supply a clear scope when the source is partial.
4. Validate the host's required output format and check that citations support the associated observations.
5. Record the skill version and resolved content or a reproducible content reference with the task. Resume a task with the original rules.
6. Report a saved correction or profile update only after the storage operation confirms success. Revising an answer in conversation does not change stored records.
7. Keep the skill scoped to material-based analysis: Personalysis objectively identifies and explains risk signals recorded in the material and does not output emergency hotlines or action advice.

For example, a journal application may discuss a user's correction immediately. If the user asks to save it and the application provides an authorized storage operation, the host can perform and verify that update. An application without that capability must not claim a stored profile has changed.

Load the core instructions for the task and expose supporting references when relevant. Hosts without file-reading tools do not need to expose `references/theory-basis.md`; the core instructions tell the model to rely on `SKILL.md` alone and never claim to have read external reference files.

## Section slicing for host injection

After removing the leading YAML frontmatter (`--- ... ---`), `SKILL.md` is partitioned into three fixed regions in exact order:

- `core`: from `# Personalysis` up to immediately before `## Task: Material analysis` (shared rules for objective risk signal identification, evidence attribution and distinctions, eight theoretical perspectives, contrary-evidence checking and proportional revision, and optional personality frameworks).
- `materialAnalysis`: from `## Task: Material analysis` up to immediately before `## Task: Interactive dialogue` (offline/batch analysis of chat logs and journals without follow-up questions).
- `interactiveDialogue`: from `## Task: Interactive dialogue` to the end of the file (multi-turn reflection, supportive conversation, live clarification handling, absent-person and popular-label analysis, and the default 1–4 step dialogue response shape).

`## Task: Material analysis` and `## Task: Interactive dialogue` are always the last two level-2 (`##`) headings in `SKILL.md`; subsections inside them use level-3 (`###`) headings only. Hosts can split unambiguously on those two exact headings and assemble:

- **Offline or batch material analysis:** `core + "\n\n" + materialAnalysis`
- **Multi-turn reflection and supportive dialogue:** `core + "\n\n" + interactiveDialogue`
- **Full standalone body:** full frontmatter-stripped `SKILL.md`

For deterministic integrity checks, normalize `\r\n` to `\n` in UTF-8 first: hash the full LF-normalized file directly; for the body and task assemblies, strip the leading YAML frontmatter, trim leading and trailing whitespace on each extracted segment, and join `core` and the selected task segment with `"\n\n"` before computing SHA-256.

## Application patterns

The same methodology can support different kinds of application. Choose the pattern that matches the user's task:

| Task | Use of Personalysis | Host-owned responsibility |
| --- | --- | --- |
| Conversation analysis | Analyze behavior and interaction in the selected source range | Source selection, report format, citation checks, and report storage |
| Personal reflection | Discuss a question and incorporate the user's own clarification | Conversation context and user-approved record updates |
| Supportive conversation | Help express and understand feelings in the person's own terms | Conversation controls and any user-approved storage |

For example, a conversation assistant can supply a discussion about dividing work and ask for an explanation of how the speakers negotiated responsibility. Personalysis guides the interpretation of proposals, refusals, and stated constraints; the assistant provides the selected messages and renders the result in its own interface.

Keep application-specific formats, optional personality descriptions, and storage rules in the host's task instructions. Record the selected Personalysis version with the task so later review can recover the instructions used.
