---
name: amplify-ai-explain
version: 1.0.0
display_name: 把知识讲明白
display_name_en: Explain Clearly
description_zh: 根据理解目标选择文字、图表、交互网页或视频，把知识讲清楚。
description_en: Explain a topic clearly using writing, diagrams, interactive pages, or video suited to the learning goal.
description: >
  Use when a user wants to understand or explain a topic and needs help choosing
  between clear writing, diagrams/images, interactive web pages, and explainer
  videos, or wants a reusable prompt for one of these formats. Also applies to
  “把知识讲明白”, “讲解”, “图解”, “交互网页”, “讲解视频”. Not for standalone fact
  lookup, revising an existing draft, or planning execution after a choice is settled.
---

# 把知识讲明白（Make Knowledge Clear）

Turn a learning goal into a suitable output format and the deliverable the user requests. Generate a ready-to-use prompt by default when no deliverable is specified. When the user asks for an explanation, diagram, page, or video itself, create that artifact using the available tools; do not stop at a prompt or require a separate production request. Treat follow-ups such as “make it” as requests to execute the previously agreed prompt. If a required capability is unavailable, explain the specific limitation and clearly label any partial deliverable, such as source or a storyboard instead of a rendered video.

## Source and scope

Inspired by [Andrej Karpathy's original post](https://x.com/karpathy/status/2105819303471976479) about understanding language-model outputs through writing, diagrams/images, interactive web pages, and bespoke explainer videos.

Karpathy presents these media progressively, mentions ASD-STE100 and 3b1b-style explainers, and advocates custom, discardable software artifacts. The name “Understanding-First Output Ladder,” L1–L4 labels, selection rules, and templates below are this project's extensions, not a named methodology from the original post.

Use this framework for personal learning, concept demonstrations, and explanation prototypes. For authoritative documentation or maintained teaching material, use the required format and sourcing process; this framework can supplement them.

## Inputs

Accept natural-language requests; these fields are convenient shorthand, not a required parser:

- `topic`: Concept, system, or algorithm to understand. Required; ask if absent and not inferable.
- `audience`: Beginner, intermediate, or expert. Default to intermediate when no context indicates otherwise.
- `preference`: L1–L4, writing, diagram/image, web, or video. Honor an explicit choice.
- `constraints`: Such as offline, no API keys, frontend only, duration, budget, or accessibility requirements.

Use the user's language for explanations and prompts unless requested otherwise. Resolve a material conflict between preference and constraints before producing an incompatible prompt. Otherwise proceed with reasonable assumptions and include those that affect correctness in the prompt.

## Select the medium

Identify the learning outcome: what should the learner be able to explain, predict, compare, or do? Consider structure, change over time, interaction, narrative, and audience knowledge.

| Level | Medium | Choose when |
| --- | --- | --- |
| L1 | Clear writing | Definitions, distinctions, rules, or reasoning benefit mainly from precise language. |
| L2 | Diagrams / images | Spatial structure, relationships, flows, or comparisons are the main bottleneck. |
| L3 | Interactive web | The learner benefits from changing inputs, stepping through a process, or comparing outcomes. |
| L4 | Explainer video | A guided sequence, coordinated animation, or narrative helps explain change or build an argument. Interaction is not required. |

Choose the simplest medium that meets the learning outcome and constraints. Higher levels offer richer media, not guaranteed deeper understanding. A dynamic topic may suit either L3 or L4: use L3 for learner-controlled exploration and L4 for guided exposition. Recommend a combination only when the parts serve distinct learning needs.

If the user specifies a medium, use it and explain how to make it effective instead of reopening format selection.

## Build the prompt

For prompt requests, produce a self-contained, copyable prompt with the elements below. For artifact requests, apply these elements as an internal production brief and deliver the artifact; include the prompt only if the user also asks for it.

1. Topic, audience, prerequisites, and a concrete learning outcome.
2. Output medium and deliverable, including technical constraints where relevant.
3. The core content and the particular structure, interaction, or narrative that supports understanding.
4. Assumptions, simplifications, and checks needed for subject accuracy.
5. Observable success criteria: for example, predict the next state or explain why two outcomes differ.

Apply the user's constraints to the main prompt, alternative prompts, and practical tips alike.

### Medium-specific guidance

- **L1:** Use plain, precise language and define unfamiliar terms. ASD-STE100-inspired writing is an option, especially for technical English. Do not claim formal compliance without checking the applicable vocabulary and rules; a sentence-length limit alone is insufficient. For other languages, use their own clear-writing conventions.
- **L2:** Specify the diagram type, labels, relationships, and legend. Prefer Mermaid for supported logical diagrams; use another format when spatial or pictorial content requires it. Include a text explanation of the essential relationships.
- **L3:** Specify meaningful controls, visible feedback, initial conditions, reset behavior, and informative edge cases. For lightweight prototypes, prefer a self-contained HTML/CSS/JS page unless the user's stack requires otherwise. Include labels and keyboard-operable controls; avoid relying on color alone.
- **L4:** Specify duration, audience, narrative sequence, storyboard, animation, captions, and narration requirements. For executable output, request source plus rendering instructions and name the toolchain. Treat a script or storyboard as a separate deliverable from a rendered video. If no rendering tool is available, state what can be delivered. Describe desired visual qualities; “3b1b-inspired” can be a reference, but do not imply affiliation or copy branded assets.

### Accuracy and feasibility

Disposable artifacts reduce maintenance needs, not factual standards. Require checks of key facts, equations, transitions, and simulated behavior. Name algorithm variants when behavior differs between them, label approximations, and distinguish illustrative models from real-world implementations. Request sources when claims need verification; never invent citations.

For `offline`, exclude runtime network calls, CDNs, remote fonts, and cloud speech services. State any one-time installation or download requirements separately; if setup must also be offline, use only locally available dependencies. gTTS uses an online service and is not an offline narration option. Use an available local TTS engine, supplied audio, or captions without narration as appropriate.

For `no API keys`, select tools that do not require credentials; this does not imply offline operation. Suggest tools only when relevant and do not guarantee current pricing or availability. Mermaid, D2, or Graphviz can serve diagrams; native web code can serve interactions; Manim or Remotion can serve video source. These are optional choices, not required dependencies of this skill.

## Response contract

Match the response to the requested deliverable and level of detail. The following elements are optional structure, not mandatory headings. For a prompt-only request, return just the complete prompt. For a simple request, omit analysis, alternatives, and tips that add no useful information.

**Topic analysis:** When useful, briefly identify the learning bottleneck and audience assumptions that affect the result.

**Recommended level:** When format selection is part of the request, give L1–L4, the medium, and a short rationale. Use **Selected level** when explaining an explicit preference; do not repeat a selection already established in the conversation. Prompt-only requests still select a level: put the level and a one-line rationale inside the prompt's opening line, not as outside commentary, so the response stays a single copyable prompt.

**Requested deliverable:** For prompt requests, provide the complete prompt in one copyable block using the host's supported format. For artifact requests, provide the actual explanation, diagram, page, or video, with access or usage instructions where needed and a brief account of relevant verification and remaining limitations. If both are requested, deliver both.

**Alternative options:** Include up to two only when the user requests alternatives or is still choosing a medium. Use only L1–L4 and explain each option's distinct benefit. Each alternative prompt must stand alone: restate the topic, audience, learning outcome, necessary model assumptions, and all applicable constraints without referring to “the same model” or earlier text. Adapt medium-specific requirements explicitly. Do not create extra artifacts unless requested.

**Practical tips:** Include only actionable, topic-specific verification or iteration advice that is not already covered in the deliverable and respects all constraints.

## Example

Input: “Give me a prompt for teaching TCP congestion control to beginners through an interactive web page, offline with no external dependencies. Also include a diagram alternative.”

**Topic analysis:** The main bottleneck is connecting packet-loss signals to changes in the congestion window. A simplified TCP Reno model can show these changes while keeping the assumptions visible.

**Selected level:** L3 — Interactive web. Adjustable loss events let the learner compare timeout and duplicate-ACK responses.

**Ready-to-use prompt:**

```text
Create a self-contained HTML/CSS/JS page teaching simplified TCP Reno congestion control to beginners. It must work offline with no external dependencies or network requests.

Learning outcome: The learner can predict how cwnd and ssthresh change after a timeout or three duplicate ACKs and explain how slow start differs from congestion avoidance.

Show a cwnd-over-time chart with labeled units and the current phase. Provide step, play/pause, reset, initial-ssthresh controls, and separate buttons for timeout and three duplicate ACKs. Include fast recovery and annotate important transitions. Make controls keyboard-operable and explain events in text as well as color.

State the model's update rules and assumptions, including discrete RTT steps, the chosen Reno fast-recovery behavior, and omissions such as receiver-window limits. Distinguish this teaching model from a production TCP implementation.

Check phase transitions and loss responses against the stated Reno rules. Include two worked traces, one per loss event, and a short prediction exercise with an explanation of the answer. Deliver the complete HTML file and instructions to open it locally.
```

**Alternative option:** L2 — A static diagram lets beginners inspect phase transitions together.

```text
Create a self-contained SVG state diagram with a plain-text explanation teaching simplified TCP Reno congestion control to beginners. Deliver the complete SVG file, viewable locally in a browser, with no external dependencies, scripts, remote fonts, or network requests. Embed all styling and use text labels as well as color.

Learning outcome: The learner can predict how cwnd and ssthresh change after a timeout or three duplicate ACKs and explain how slow start differs from congestion avoidance. Define cwnd and ssthresh and their units. Show slow start, congestion avoidance, and fast recovery; label transitions with triggers and variable updates, including recovery exit.

State the model's update rules and assumptions, including discrete RTT steps, the chosen Reno fast-recovery behavior, and omissions such as receiver-window limits. Distinguish this teaching model from a production TCP implementation. Check the diagram against the stated Reno rules and provide two worked traces, one for each loss event, plus a prediction exercise with an explained answer.
```

**Practical tip:** Verify both worked traces before adding visual polish; the diagram and simulator should use the same update rules.
