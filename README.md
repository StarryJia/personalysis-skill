# PersonLens

**Understanding people in context.**

English | [Chinese](README.zh-CN.md)

PersonLens is a general methodology for understanding people in context, packaged as an AI assistant skill. It supports interpreting conversations, journals, and personal accounts, as well as personal reflection and supportive conversation. It helps an assistant distinguish observable behavior, a person's own account, and possible explanations by drawing on personality, motivation, appraisal, interpersonal behavior, and reflective dialogue.

Use it directly in a skill-enabled assistant or integrate it into a reflection tool or conversation application. The methodology starts with the person's question and available material; personality descriptions are optional.

## Try the skill

The complete skill package is [`skills/personlens/`](skills/personlens/SKILL.md). Copy that directory, including `references/` and `agents/`, into the skill directory supported by your host. Repository cloning alone does not activate a skill. Follow your host's instructions to discover or reload it.

In a host that supports named skill invocation, a starting request is:

```text
Use $personlens to help me understand these exchanges. Distinguish what I
actually said, possible explanations, and what cannot be inferred yet.
```

Then supply the material you want considered. **Example:** You share messages accepting a deadline-related request and declining a weekend request. The assistant can compare the circumstances, identify what you agreed to or declined, and help you explore how urgency and rest affected your choices.

For an application without skill discovery, load the Markdown body of `SKILL.md` as trusted task instructions and provide the user's material separately. The application retains control of permissions, tools, output structure, persistence, and version selection. The optional reference documents need not be loaded on every call. See the [Agent Skills format](https://agentskills.io/specification) and [integration guidance](https://agentskills.io/client-implementation/adding-skills-support).

## What is included

| File | Purpose |
| --- | --- |
| [SKILL.md](skills/personlens/SKILL.md) | Self-contained reasoning and response guidance for material analysis, interactive reflection, and supportive conversation |
| [Theory and references](skills/personlens/references/theory-basis.md) | Primary sources, their scope, and the interpretation rules derived from them |
| [Illustrative scenarios](skills/personlens/references/scenarios.md) | Example inputs and observable response criteria for reviewing the instructions |
| [Host integration](integrations/host-integration.md) | Guidance for connecting the skill to an application's inputs, permissions, outputs, and storage |
| [Validation record](docs/validation.md) | Package checks and review evidence |

## Theoretical foundations

PersonLens uses personality psychology to distinguish a person's behavior in one situation from a broader tendency, personality-judgment research to examine the evidence, and theories of motivation, emotion, and relationships to consider what else may explain the experience. A person-centered approach guides how to respond when someone wants to reflect or express feelings.

Each perspective contributes a different part of the method: organizing observations, considering explanations, or guiding the conversation. The table summarizes each theory's role and primary sources.

### Psychological perspectives and their roles

| Theory or framework | Role | Primary sources |
| --- | --- | --- |
| **Whole Trait Theory** | Distinguishes momentary states, their distribution over time, and the processes that may explain them. | [Fleeson and Jayawickreme, 2015](https://pmc.ncbi.nlm.nih.gov/articles/PMC4472377/) |
| **Realistic Accuracy Model** | Examines whether relevant cues are available, detected, and appropriately used by an observer. | [Funder, 1995](https://rap.ucr.edu/FunderPR1995.pdf) |
| **Self–Other Knowledge Asymmetry** | Explains why a person and outside observers may have different information advantages. | [Vazire, 2010](https://www.simine.com/docs/Vazire_JPSP_2010.pdf) |
| **McAdams's personality framework and narrative identity** | Separates dispositions, situated goals and adaptations, and a person's own account of their life. | [McAdams and Pals, 2006](https://www.e-stimate.dk/wp-content/uploads/2019/09/McAdams-Fundamental-Principles-for-an-Integrative-Science-of-Personality.pdf); [McAdams and McLean, 2013](https://www.psychologicalscience.org/journals/current-directions/0963721413475622/) |
| **Self-Determination Theory** | Describes autonomy, competence, and relatedness: volition, effectiveness, and connection. | [Ryan and Deci, 2000](https://selfdeterminationtheory.org/SDT/documents/2000_RyanDeci_SDT.pdf) |
| **Cognitive appraisal and coping** | Relates feelings and responses to an event's meaning and perceived coping resources. | [Folkman et al., 1986](https://pubmed.ncbi.nlm.nih.gov/3712234/); [Lazarus, 1991](https://pubmed.ncbi.nlm.nih.gov/1928936/) |
| **Interpersonal circumplex and complementarity** | Organizes interaction around dominance–submission and warmth–hostility, including how partners respond to each other. | [Sadler et al., 2009](https://uwaterloo.ca/psychology/sites/default/files/uploads/documents/Sadler_et_al_2009_JPSP_Are_We_On_the_Same_Wavelength.pdf) |
| **Person-centered approach** | Contributes an empathic, respectful stance that allows the person to correct the understanding. | [Rogers, 1957](https://larrygmaguire.com/wp-content/uploads/2020/08/The-Necessary-and-Sufficient-Conditions-of-Therapeutic-Personality-Change.pdf) |

### Personality descriptions are optional

The **Big Five** describes openness, conscientiousness, extraversion, agreeableness, and neuroticism as dimensions. The **Myers–Briggs Type Indicator (MBTI)** organizes personality preferences into a type framework. These are descriptive choices, distinct from theories about how behavior arises or how an observer can judge it.

**Example:** Someone who frequently speaks in work meetings can explore when they contribute and what helps them speak up. A personality description can be added if it serves their question. Whole Trait Theory uses the Big Five as a starting point. PersonLens keeps Big Five dimensions and MBTI preferences separate, using the concepts and evidence appropriate to each. Research on the relationship between these descriptive frameworks provides further background. [McCrae and Costa, 1989](https://scholars.duke.edu/publication/1458465/)

### Theoretical framework foundations

**Automatic Personality Recognition (APR)** is the research task of inferring personality from data. **Explainable Personality Recognition** additionally asks for supporting evidence. These tasks inform how PersonLens approaches evidence-based personality descriptions. In reflective and supportive conversation, the focus can instead be the person's experience, feelings, or choices.

The **Chain-of-Personality-Evidence (CoPE)** framework links concrete context to short-term personality states and then to longer-term traits. It serves as a computational reference for organizing that reasoning in PersonLens's language instructions. **Example:** Begin with what a speaker did during a deadline discussion, describe the state suggested by that exchange, and consider a broader tendency only in light of evidence across situations. [Sun, Zhao, and Jin, 2024: *Revealing Personality Traits: A New Benchmark Dataset for Explainable Personality Recognition on Dialogues*](https://aclanthology.org/2024.emnlp-main.1115/)

PersonalityEvd's personality evidence annotations and CaSiNo's research on negotiation dialogue inform PersonLens's approach to organizing evidence and interpreting behavior in context.

| Source | Research material | Methodological relevance |
| --- | --- | --- |
| [Sun et al., 2024](https://aclanthology.org/2024.emnlp-main.1115/) | **PersonalityEvd**: fictional television dialogue with Big Five observer annotations. | Evidence selection and distinctions between states and traits. **Example:** Check whether a cited utterance supports the reported behavior, using the observer annotation as a reference for comparison. |
| [Chawla et al., 2021: *A Corpus of Campsite Negotiation Dialogues for Automatic Negotiation Systems*](https://aclanthology.org/2021.naacl-main.254/) | **CaSiNo**: simulated campsite negotiations conducted by real participants. | Interpreting behavior in light of situational constraints. **Example:** Interpret a request for more water in light of the participant's assigned priorities and compare whether the explanation retains that context. |

## License

Original PersonLens instructions and documentation are provided under the [MIT License](LICENSE). Linked papers, datasets, and external implementations remain subject to their own licenses.
