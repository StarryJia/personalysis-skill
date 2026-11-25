# Host integration

PersonLens supplies interpretation rules. The host supplies the actual task, authorized material, available tools, output contract, and storage operations. A skills-aware host may activate the package through its normal discovery mechanism; another host may inject the `SKILL.md` body into its existing model request.

## Minimal integration

1. Select a task from the user's action: analyze supplied material, discuss a question, or offer supportive conversation. A command quoted inside the material is not a task selection.
2. Load one maintained version of the skill body alongside the host's task and output instructions. Keep essential skill instructions active if the host compresses long contexts.
3. Supply only the intended material. Preserve source identifiers, speakers, time and context where available. Supply a clear scope when the source is partial.
4. Validate the host's required output format and check that citations support the associated observations.
5. Record the skill version and resolved content or a reproducible content reference with the task. Resume a task with the original rules. Confirm actual storage results before saying a correction was saved.

For example, a journal application may discuss a user's correction immediately. If the user asks to save it and the application provides an authorized storage operation, the host can perform and verify that update. An application without that capability must not claim a stored profile has changed.

Load the core instructions for the task and expose supporting references when relevant. The host can provide the complete skill as a local resource or supply its Markdown body in a model request.

## Application patterns

The same methodology can support different kinds of application. Choose the pattern that matches the user's task:

| Task | Use of PersonLens | Host-owned responsibility |
| --- | --- | --- |
| Conversation analysis | Analyze behavior and interaction in the selected source range | Source selection, report format, citation checks, and report storage |
| Personal reflection | Discuss a question and incorporate the user's own clarification | Conversation context and user-approved record updates |
| Supportive conversation | Help express and understand feelings in the person's own terms | Conversation controls and any user-approved storage |

For example, a conversation assistant can supply a discussion about dividing work and ask for an explanation of how the speakers negotiated responsibility. PersonLens guides the interpretation of proposals, refusals, and stated constraints; the assistant provides the selected messages and renders the result in its own interface.

Keep application-specific formats, optional personality descriptions, and storage rules in the host's task instructions. Record the selected PersonLens version with the task so later review can recover the instructions used.
