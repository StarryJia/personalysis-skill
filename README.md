# Personalysis

**Understanding people in context.**

English | [Chinese](README.zh-CN.md)

Personalysis is a general methodology for understanding people in context, packaged as an AI assistant skill. It supports interpreting conversations, journals, and personal accounts, as well as personal reflection and supportive conversation. It helps an assistant distinguish observable behavior, a person's own account, and possible explanations by drawing on personality, motivation, appraisal, interpersonal behavior, and reflective dialogue.

Use it directly in a skill-enabled assistant or integrate it into a reflection tool or conversation application. The methodology starts with the person's question and available material; personality descriptions are optional.

## Try the skill

The complete skill package is [`skills/personalysis/`](skills/personalysis/SKILL.md). Copy that directory, including `references/` and `agents/`, into the skill directory supported by your host. Repository cloning alone does not activate a skill. Follow your host's instructions to discover or reload it.

In a host that supports named skill invocation, a starting request is:

```text
Use $personalysis to help me understand these exchanges. Distinguish what I
actually said, possible explanations, and what cannot be inferred yet.
```

Then supply the material you want considered. **Example:** You share messages accepting a deadline-related request and declining a weekend request. The assistant can compare the circumstances, identify what you agreed to or declined, and help you explore how urgency and rest affected your choices.

For an application without skill discovery, load the frontmatter-stripped Markdown body of `SKILL.md` in full or slice it by its two fixed task headings (`core + Task: Material analysis` for batch/offline material analysis, or `core + Task: Interactive dialogue` for multi-turn dialogue) as trusted task instructions, and provide the user's material separately. See [host integration](integrations/host-integration.md) for the exact section boundaries and SHA-256 verification rules. The application retains control of permissions, tools, output structure, persistence, and version selection. The optional reference documents need not be loaded on every call. See the [Agent Skills format](https://agentskills.io/specification) and [integration guidance](https://agentskills.io/client-implementation/adding-skills-support).

## What is included

| File | Purpose |
| --- | --- |
| [SKILL.md](skills/personalysis/SKILL.md) | Self-contained reasoning and response guidance for material analysis, interactive reflection, and supportive conversation |
| [Theory and references](skills/personalysis/references/theory-basis.md) | Primary sources, their scope, and the interpretation rules derived from them |
| [Agent metadata](skills/personalysis/agents/openai.yaml) | Display name, short description, and starting prompt for hosts that support this metadata |
| [Skill license](skills/personalysis/LICENSE) | License notice retained when the skill directory is copied |
| [Host integration](integrations/host-integration.md) | Guidance for connecting the skill to an application's inputs, permissions, outputs, and storage |
| [Review scenarios](docs/review-scenarios.md) | Fictional inputs and review criteria for checking responses |
| [Validation record](docs/validation.md) | Package checks and recorded test answers |

The installable package is the four files under `skills/personalysis/`; everything else is for maintainers and integrators.

## How the instructions guide analysis

The host discovers the skill from its name and description, then loads `SKILL.md` when it applies. After the YAML frontmatter, the body is organized into three fixed regions—the shared `core` section followed by the final two level-2 headings, `## Task: Material analysis` and `## Task: Interactive dialogue`—so `SKILL.md` works both as a standalone skill file and via task-scoped host injection. The core directs the assistant to identify risk signals in the material objectively without speculating about current status or offering advice, trace claims to supplied material, distinguish observations from reports and interpretations, consider contrary evidence and context, revise only claims affected by new information, and apply personality frameworks only on request. The two task sections separate offline/batch analysis rules (following host format, no follow-up questions) from interactive dialogue rules (mode matching, live clarifications, absent-person and popular-label breakdown, and the 1–4 step response shape). The theory reference (`references/theory-basis.md`) is consulted on demand only in environments that expose local reference files.

**Fictional example:** Someone asks whether saying “I'll take this task” proves they were relaxed. The skill calls for recording the expressed willingness, leaving the feeling uncertain, and revising that interpretation if the person later reports anxiety.

## Theoretical foundations

Personalysis uses personality psychology to distinguish a person's behavior in one situation from a broader tendency, personality-judgment research to examine the evidence, and theories of motivation, emotion, and relationships to consider what else may explain the experience. A person-centered approach guides how to respond when someone wants to reflect or express feelings.

Each perspective contributes a different part of the method: organizing observations, considering explanations, or guiding the conversation. The table summarizes each theory's role and primary sources.

### Psychological perspectives and their roles

| Theory or framework | Role | Primary sources |
| --- | --- | --- |
| **Whole Trait Theory** | Distinguishes momentary states, their distribution over time, and the processes that may explain them. | [Fleeson and Jayawickreme, 2015](https://pmc.ncbi.nlm.nih.gov/articles/PMC4472377/) |
| **Realistic Accuracy Model** | Examines whether relevant cues are available, detected, and appropriately used by an observer. | [Funder, 1995](https://rap.ucr.edu/FunderPR1995.pdf) |
| **Self–Other Knowledge Asymmetry** | Relates judgment accuracy to differences in information access and motivational biases. | [Vazire, 2010](https://www.simine.com/docs/Vazire_JPSP_2010.pdf) |
| **McAdams's personality framework and narrative identity** | Separates dispositions, situated goals and adaptations, and a person's own account of their life. | [McAdams and Pals, 2006](https://www.e-stimate.dk/wp-content/uploads/2019/09/McAdams-Fundamental-Principles-for-an-Integrative-Science-of-Personality.pdf); [McAdams and McLean, 2013](https://www.psychologicalscience.org/journals/current-directions/0963721413475622/) |
| **Self-Determination Theory** | Describes autonomy, competence, and relatedness: volition, effectiveness, and connection. | [Ryan and Deci, 2000](https://selfdeterminationtheory.org/SDT/documents/2000_RyanDeci_SDT.pdf) |
| **Cognitive appraisal and coping** | Relates feelings and responses to an event's meaning and perceived coping resources. | [Folkman et al., 1986](https://pubmed.ncbi.nlm.nih.gov/3712234/); [Lazarus, 1991](https://pubmed.ncbi.nlm.nih.gov/1928936/) |
| **Interpersonal circumplex and complementarity** | Organizes interaction around dominance–submission and warmth–hostility, including how partners respond to each other. | [Sadler et al., 2009](https://uwaterloo.ca/psychology/sites/default/files/uploads/documents/Sadler_et_al_2009_JPSP_Are_We_On_the_Same_Wavelength.pdf) |
| **Person-centered approach** | Contributes an empathic, respectful stance that allows the person to correct the understanding. | [Rogers, 1957](https://larrygmaguire.com/wp-content/uploads/2020/08/The-Necessary-and-Sufficient-Conditions-of-Therapeutic-Personality-Change.pdf) |

### Personality descriptions are optional

The **Big Five** describes openness, conscientiousness, extraversion, agreeableness, and neuroticism as dimensions. The **Myers–Briggs Type Indicator (MBTI)** organizes personality preferences into a type framework. These are descriptive choices, distinct from theories about how behavior arises or how an observer can judge it.

**Fictional example:** Someone who frequently speaks in work meetings can explore when they contribute and what helps them speak up. A personality description can be added if it serves their question. Whole Trait Theory uses the Big Five as a starting point.

Personalysis permits evidence-based connections between MBTI and the Big Five. McCrae and Costa found that the four MBTI indices measured aspects of four Big Five dimensions, while finding no support for truly dichotomous preferences or qualitatively distinct types. A statistical relationship can inform comparison without supplying an individual's missing test scores. **Fictional example:** An introverted MBTI preference and a middle-range Big Five extraversion result can be discussed together without automatically rejecting either result or converting one score into the other. See the [framework reference](skills/personalysis/references/theory-basis.md#optional-personality-frameworks) and [McCrae and Costa, 1989](https://scholars.duke.edu/publication/1458465/).

### Theoretical framework foundations

**Automatic Personality Recognition (APR)** is the research task of inferring personality from data. **Explainable Personality Recognition** additionally asks for supporting evidence. These tasks inform how Personalysis approaches evidence-based personality descriptions. In reflective and supportive conversation, the focus can instead be the person's experience, feelings, or choices.

The **Chain-of-Personality-Evidence (CoPE)** framework links concrete context to short-term personality states and then to longer-term traits. It serves as a computational reference for organizing that reasoning in Personalysis's language instructions. **Example:** Begin with what a speaker did during a deadline discussion, describe the state suggested by that exchange, and consider a broader tendency only in light of evidence across situations. [Sun, Zhao, and Jin, 2024: *Revealing Personality Traits: A New Benchmark Dataset for Explainable Personality Recognition on Dialogues*](https://aclanthology.org/2024.emnlp-main.1115/)

PersonalityEvd's personality evidence annotations and CaSiNo's research on negotiation dialogue inform Personalysis's approach to organizing evidence and interpreting behavior in context.

| Source | Research material | Methodological relevance |
| --- | --- | --- |
| [Sun et al., 2024](https://aclanthology.org/2024.emnlp-main.1115/) | **PersonalityEvd**: fictional television dialogue with Big Five observer annotations. | Evidence selection and distinctions between states and traits. **Example:** Check whether a cited utterance supports the reported behavior, using the observer annotation as a reference for comparison. |
| [Chawla et al., 2021: *A Corpus of Campsite Negotiation Dialogues for Automatic Negotiation Systems*](https://aclanthology.org/2021.naacl-main.254/) | **CaSiNo**: simulated campsite negotiations conducted by real participants. | Interpreting behavior in light of situational constraints. **Example:** Interpret a request for more water in light of the participant's assigned priorities and compare whether the explanation retains that context. |

## License

Original Personalysis instructions and documentation are provided under the [MIT License](LICENSE). Linked papers, datasets, and external implementations remain subject to their own licenses.
