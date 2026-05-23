# Scientific Writing — Detailed Patterns and Examples

Reference file for the `scientific-writing` skill. Read this when you need specific templates or examples.

---

## Sentence-Level Patterns

### Characters and Actions

Weak (nominalization):
> The investigation of visual place recognition by the researchers led to the development of a new method.

Strong (characters as subjects, actions as verbs):
> We investigated visual place recognition and developed a new method.

### Old-to-New Information Flow

Weak (new information first):
> A 4x improvement in Recall@1 across 12 diverse datasets was achieved by AnyLoc.

Strong (familiar then new):
> AnyLoc achieves a 4x improvement in Recall@1 across 12 diverse datasets.

### Getting to the Verb

Weak (long introductory phrase):
> In order to enable robots to operate effectively across more environments with minimal additional human intervention, this thesis advances flexible robot perception.

Strong (verb early):
> This thesis advances flexible robot perception, enabling robots to operate across more environments with minimal human intervention.

---

## Common Templates

### Related Work Positioning

```
[Prior work] [what it does]. However, [limitation]. We address this by [our approach].
```

Example:
> NetVLAD learns place descriptors through weakly-supervised training. However, it requires dataset-specific tuning. We address this by learning universal features from foundation models.

### Results Interpretation

```
[Method] achieves [metric] on [benchmark], [comparison to baseline]. This [interpretation].
```

Example:
> AnyLoc achieves 94.5% Recall@1 on Pitts30k, outperforming NetVLAD by 15%. This confirms that foundation model features generalize better than task-specific training.

### Limitation Acknowledgment

```
While [method] [achievement], [limitation]. Future work could [direction].
```

Example:
> While our approach generalizes across diverse environments, it requires 2x more compute than the baseline. Future work could explore distillation to reduce inference cost.

### Contribution Quantification

When possible, quantify contributions:
- "up to 4x higher Recall@1"
- "6% improvement in accuracy"
- "reduces training time by 50%"
- "generalizes to 12 diverse datasets"

---

## Robotics/CV Domain Templates

### System Description

```
[System] consists of [N] components: [list]. Given [input], [component 1] [action]. [Component 2] then [action].
```

### Evaluation Setup

```
We evaluate on [N] datasets spanning [diversity dimensions]. For each, we report [metrics]. All experiments use [hardware/setup].
```

### Ablation Studies

```
To understand the contribution of each component, we conduct ablation studies. Table [N] shows [key finding from ablations].
```

### Minimal Modeling Framing

When arguing for simplicity over complexity:

```
We pursue a minimal modeling strategy guided by [N] central questions:
1. [Question about representation/target]?
2. [Question about architecture]?

Our work provides an affirmative answer to both. We present [method], a [architecture type] that [capability].
```

### Feed-Forward vs Optimization Framing

```
[Prior methods] require [expensive post-processing/optimization]. In contrast, [our method] produces [output] in a single forward pass.
```

### Unified Model Positioning

```
While prior work has approached [tasks] separately, we present a unified model that [handles all tasks]. This eliminates [limitation of separate models].
```

---

## Introduction Patterns

### Research Question Framing

```
In this context, we explore the question, "[How can X benefit Y?]"
```

### Key Insight Statement

```
[Method]'s key insight is [core technical idea]. Instead of [conventional approach], we [novel approach].
```

### Benefits Enumeration

```
We find that this leads to the following benefits over existing [alternatives]:
- [Benefit 1]: [Explanation with technical grounding]
- [Benefit 2]: [Explanation with technical grounding]
- [Benefit 3]: [Explanation with technical grounding]
```

### Numbered Contributions (for multi-task papers)

```
In summary, we make the following main contributions:
1. [Contribution type]: [Specific description with key differentiator]
2. [Contribution type]: [Specific description]
3. [Contribution type]: [Performance claim with comparison]
4. [Contribution type]: [Release/availability statement]
```

---

## Grant-Specific Patterns

### Thrust/Activity Pattern

```
Research Activity [N]: [Descriptive Title]

[Problem/Goal paragraph]

[Approach paragraph with technical details]

[Expected outcomes and how they connect to other thrusts]

Risks and Mitigation: [Honest assessment with backup plans]
```

### Scientific Context Positioning

```
Position clearly against related work.
Pattern: "X does Y, but lacks Z. We address this by..."
Differentiate without dismissing prior work.
```

---

## Nominalization Quick-Fix Table

| Nominalization | Verb Form |
|---------------|-----------|
| make a decision | decide |
| conduct an investigation | investigate |
| perform an analysis | analyze |
| give a demonstration | demonstrate |
| provide a description | describe |

---

## Passive Voice Guidance

Use passive when:
- The actor is unknown or irrelevant
- You want to emphasize the action or object
- Convention in your field requires it (e.g., "samples were collected")

Otherwise, prefer active voice with clear actors.
