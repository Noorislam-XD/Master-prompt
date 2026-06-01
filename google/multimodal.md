---
name: Multimodal Prompting
description: Combine text and image inputs effectively for vision tasks
category: google
technique: Multimodal Prompting
source: https://ai.google.dev/gemini-api/docs/prompting-strategies#multimodal-prompts
---

```
[WHAT IT IS]
Multimodal prompting combines text instructions with one or more images.
Effective for: image analysis, visual QA, document OCR, chart reading,
diagram explanation, and UI/screenshot analysis.

[PROMPT STRUCTURE — Image + Instruction]
[Image provided separately via API or upload]

Instruction: [What you want the model to do with the image]

[TEMPLATES BY USE CASE]

--- Detailed Image Description ---
Describe this image in detail. Include:
1. The main subject and what it is doing
2. The setting and background
3. Colors, lighting, and composition
4. Any text visible in the image
5. The mood or tone conveyed

--- Chart / Data Visualization Analysis ---
Analyze this chart. Extract:
1. Chart type and what it measures
2. The time range or categories shown
3. The most significant trend or data point
4. Any anomalies or outliers
5. The key takeaway in one sentence

--- Document / Screenshot OCR ---
Extract all text from this image. Preserve:
- Headings and hierarchy
- Lists and their formatting
- Tables (as markdown tables)
- Any labels, captions, or annotations

--- UI/UX Review ---
Review this UI screenshot as a UX designer. Identify:
1. What the page/screen is for
2. The primary user action it supports
3. 3 usability strengths
4. 3 usability issues with suggested fixes

--- Diagram / Architecture Explanation ---
Explain this diagram to a [beginner / intermediate / expert] audience.
Cover: what system/process it represents, how data/control flows through it,
and any non-obvious elements.

--- Image Comparison ---
Compare these two images. Identify:
1. What is the same in both
2. What is different
3. Which is better for [specific purpose] and why

[FEW-SHOT MULTIMODAL TEMPLATE]
Here is an example of the task:

Example image: [image 1]
Example output: [what the correct output looks like]

Now do the same for this image:
[image 2]

[NOTES]
- Place the instruction AFTER the image reference for Gemini — it attends better to trailing instructions.
- For document analysis, higher resolution images = better OCR accuracy.
- Be specific about what to extract — "analyze this" produces vague results.
- Gemini 1.5 Pro supports up to 3,000 images in a single context window.
- For diagrams, explicitly say "explain what each component represents" to get full coverage.
- Test with: photo → diagram → screenshot → chart, as accuracy varies across image types.
```
