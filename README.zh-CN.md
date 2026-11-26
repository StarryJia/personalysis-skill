# Personalysis

**在处境中理解人。**

[English](README.md) | 简体中文

Personalysis 是一套以心理学理论和人格分析框架为基础的通用方法论，以技能形式提供给人工智能助手。它根据聊天、日记与本人补充，理解行为、目标、情绪及关系互动，区分原文观察、本人体验与可能解释，并随着新信息修订判断。

适用于会话分析、个人反思和支持性交流。例如，分析聊天中的互动模式、结合本人补充重新理解一次冲突，或帮助表达一段难以整理的感受。开发者可以将这些方法接入自己的对话助手或个人记录工具。

## 使用

将完整的 [`skills/personalysis/`](skills/personalysis/SKILL.md) 目录复制到使用工具支持的技能目录，按该工具的说明发现或重新加载技能。仅克隆仓库不会自动启用。

在支持按名称调用技能的工具中，可以这样提问：

```text
请使用 $personalysis 帮我理解下面这段交流，区分原话能支持的观察、
可能的解释以及尚不能确定的部分。
```

随后提供本次希望分析的材料。例如，聊天中同时出现截止日期前帮忙和休息日拒绝，分析会结合两次行为的具体条件，说明这个人如何在不同处境中回应请求。

自行开发的应用也可以把 `SKILL.md` 的 Markdown 正文作为工作指令，再单独提供用户问题和授权材料。应用负责工具权限、输出格式、保存和版本选择。具体接入说明见[应用接入](integrations/host-integration.md)。

## 文件与作用

| 文件 | 作用与使用时机 |
| --- | --- |
| [SKILL.md](skills/personalysis/SKILL.md) | 技能入口；被调用时加载任务判断、证据区分、理论边界和修订规则。 |
| [theory-basis.md](skills/personalysis/references/theory-basis.md) | 理论定义、原始论文、应用例子与限制；需要理论依据或研究结论时查阅。 |
| [openai.yaml](skills/personalysis/agents/openai.yaml) | 供支持该配置的应用显示名称、简介和起始提示。 |
| [技能许可证](skills/personalysis/LICENSE) | 随技能目录复制保留的许可声明。 |
| [host-integration.md](integrations/host-integration.md) | 开发者接入指南，说明材料、权限、输出和保存的职责。 |
| [review-scenarios.md](docs/review-scenarios.md) | 虚构输入及审查标准，用于检查回答。 |
| [validation.md](docs/validation.md) | 格式检查及测试回答记录。 |

可安装的技能包是 `skills/personalysis/` 下的四个文件，其余文件供维护和接入使用。

## 如何约束分析

应用先根据技能名称和描述发现技能，在适用时加载 `SKILL.md`。正文要求助手优先处理安全风险；判断用户需要分析、反思还是倾诉；将结论对应到原始材料；区分观察、自述、他述和推测；把“自恋”“讨好型人格”等流行标签拆成可核对的具体行为；考虑反证与情境；收到补充后只修订受影响的判断。需要研究依据时才加载理论参考。

**虚构示例：**用户问“我说了这件事我来做，是不是说明当时很轻松？”技能要求先保留表达接手意愿这一观察，对当时感受保留不确定性；本人后来补充感到焦虑时，再修订情绪解释。

## 理论基础

Personalysis 用人格心理学区分当场表现与较长期倾向，用人格判断研究审视观察者的证据，再参考动机、情绪及人际关系理论，理解同一经历还可能有哪些解释。以人为中心取向则指导如何回应正在表达或反思的人。

以下整理各理论的核心观点与原始文献。

### 心理学理论分别解决什么问题

| 理论与框架 | 理论作用 | 原始文献 |
| --- | --- | --- |
| **全特质理论（Whole Trait Theory）** | 区分短期人格状态、这些状态随时间出现的分布，以及可能解释它们的心理过程。 | [Fleeson 与 Jayawickreme，2015](https://pmc.ncbi.nlm.nih.gov/articles/PMC4472377/) |
| **人格判断的现实准确性模型（Realistic Accuracy Model）** | 观察者需要取得相关线索、察觉它们，并恰当地使用。 | [Funder，1995](https://rap.ucr.edu/FunderPR1995.pdf) |
| **自我—他人知识不对称模型（Self–Other Knowledge Asymmetry）** | 判断准确性受信息获取差异与动机偏差影响。 | [Vazire，2010](https://www.simine.com/docs/Vazire_JPSP_2010.pdf) |
| **McAdams 人格框架与叙事认同** | 区分特质、处境中的目标与适应方式，以及本人对人生经历的理解。 | [McAdams 与 Pals，2006](https://www.e-stimate.dk/wp-content/uploads/2019/09/McAdams-Fundamental-Principles-for-an-Integrative-Science-of-Personality.pdf)；[McAdams 与 McLean，2013](https://www.psychologicalscience.org/journals/current-directions/0963721413475622/) |
| **自我决定理论（Self-Determination Theory）** | 自主、胜任和联结分别涉及自愿认同、有效行动及与他人的连接。 | [Ryan 与 Deci，2000](https://selfdeterminationtheory.org/SDT/documents/2000_RyanDeci_SDT.pdf) |
| **认知评价与应对（Cognitive appraisal and coping）** | 感受和应对与事件的个人意义、本人认为可用的资源有关。 | [Folkman 等，1986](https://pubmed.ncbi.nlm.nih.gov/3712234/)；[Lazarus，1991](https://pubmed.ncbi.nlm.nih.gov/1928936/) |
| **人际环形模型与互动互补性（Interpersonal circumplex and complementarity）** | 从主导—顺从、亲和—敌意等维度理解双方如何回应。 | [Sadler 等，2009](https://uwaterloo.ca/psychology/sites/default/files/uploads/documents/Sadler_et_al_2009_JPSP_Are_We_On_the_Same_Wavelength.pdf) |
| **以人为中心取向（Person-centered approach）** | 以共情、尊重和允许纠正的态度理解表达者。 | [Rogers，1957](https://larrygmaguire.com/wp-content/uploads/2020/08/The-Necessary-and-Sufficient-Conditions-of-Therapeutic-Personality-Change.pdf) |

### 人格描述体系是可选项

**大五人格（Big Five）**用开放性、尽责性、外向性、宜人性和神经质五个维度描述差异。**迈尔斯–布里格斯性格类型指标（Myers–Briggs Type Indicator，MBTI）**以偏好及类型组织描述。它们与解释行为产生过程、判断观察者是否有依据的理论属于不同层次。

Personalysis 从具体行为与处境开始分析，在用户需要时引入相应的描述体系。**虚构示例：**工作会议中经常发言，先记录为该场景中的参与表现，再结合其他材料讨论人格倾向。全特质理论以大五为研究起点。

Personalysis 支持依据研究建立 MBTI 与大五人格之间的联系。McCrae 与 Costa 发现，四项 MBTI 指标测量了大五中四个维度的部分内容；同一研究未支持真正二分的偏好或性质截然不同的人格类型。统计关联可以帮助比较，不能直接补出某个人缺失的测验分数。**虚构示例：**MBTI 结果偏向内向，大五外向性结果处于中间范围，可以讨论二者的联系，无需直接否定其中一个结果或进行分数换算。详见[框架说明](skills/personalysis/references/theory-basis.md#optional-personality-frameworks)及 [McCrae 与 Costa，1989](https://scholars.duke.edu/publication/1458465/)。

### 理论框架基础

**自动人格识别（Automatic Personality Recognition，APR）**研究如何从资料推断人格；**可解释人格识别（Explainable Personality Recognition）**进一步要求提供支持判断的证据。Personalysis 的材料分析参考这一研究方向，将判断与具体发言、情境及解释过程联系起来。

**人格证据链（Chain-of-Personality-Evidence，CoPE）**是连接具体情境、短期人格状态与较长期特质的推断框架。Personalysis 参考这一思路，先识别某次交流中的表现，再结合不同时间和处境中的材料讨论较稳定的倾向。[Sun、Zhao 与 Jin，2024：*Revealing Personality Traits: A New Benchmark Dataset for Explainable Personality Recognition on Dialogues*](https://aclanthology.org/2024.emnlp-main.1115/)

PersonalityEvd 的人格证据标注和 CaSiNo 的谈判对话研究，为 Personalysis 的证据组织与情境分析提供研究参照。

| 研究材料 | 材料内容 | 方法论参考 |
| --- | --- | --- |
| **PersonalityEvd**，见 [Sun 等，2024](https://aclanthology.org/2024.emnlp-main.1115/) | 电视剧人物对话及大五人格的观察者标注。 | 将人格判断与发言证据对应，区分状态与特质。例如，核对所引发言如何支持报告中的行为描述。 |
| **CaSiNo**，见 [Chawla 等，2021：*A Corpus of Campsite Negotiation Dialogues for Automatic Negotiation Systems*](https://aclanthology.org/2021.naacl-main.254/) | 真人参与的模拟露营物资谈判，包含分配的物资优先级及人格问卷数据。 | 将角色、目标与互动策略一起分析。例如，结合分配的优先级，解释参与者为何争取更多饮用水。 |

各理论的核心观点、分析原则和原始论文，见[理论与参考文献](skills/personalysis/references/theory-basis.md)。

## 许可

原创技能与文档使用 [MIT 许可证](LICENSE)。链接论文、数据集及外部项目保留各自许可，本仓库不打包或重新授权这些材料。
