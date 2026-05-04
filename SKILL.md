---
name: handdrawn-infographic
description: 'Use when the user wants to turn structured text (outline, bullet list, concept explanation, comparison, multi-pattern overview, agent/workflow writeup, tech concept, process description) into a hand-drawn whiteboard-style infographic image. Triggers on phrases like "生成手绘图", "画一张手绘信息图", "turn this into a sketch", "make it a whiteboard diagram", "concept sketch", "pastel hand-drawn illustration". Covers grid overviews, A-vs-B comparisons, and single-scene hierarchy diagrams in a cream-background, pastel-highlighted, rounded-card hand-drawn style. Two-phase: first emits a layout plan + image prompt for review, then calls Gemini image generation on confirmation.'
---

# Handdrawn Infographic

IRON LAW: **NEVER call the image model before the user confirms the layout plan and prompt.** The style and structure must be locked in text form first — regenerating images is expensive and the two most common failure modes (wrong layout archetype, drifted style) are both preventable at the prompt stage.

## Style Anchors (non-negotiable)

Every output must embody these style elements. Do not paraphrase them away.

- **Background**: warm cream / off-white paper (`#F5F1E8`-ish), subtle paper texture
- **Linework**: hand-drawn black outlines, slightly wobbly, rounded corners on all rectangles
- **Color palette**: muted pastel — dusty rose, lavender, mint/sage green, baby blue, peach, soft yellow. NEVER saturated / neon / gradient.
- **Highlight blocks**: key takeaway sentences wrapped in a soft green or yellow hand-drawn highlighter rectangle
- **Arrows**: hand-drawn single-stroke arrows with small filled triangle heads; curved when connecting across rows; dashed when representing "isolation / no-communication"; an X-mark crossing an arrow means "forbidden path"
- **Icons**: small black-line doodle icons next to titles (chain link, fork, trophy, magnifier, doc page, stopwatch, `</>` code window, gear). Always line-art, not filled.
- **Typography**: title in bold serif/handwritten hybrid; body labels inside cards in rounded sans; one-line summaries below cards in italic handwriting
- **Character cameos (optional)**: stick-figure-ish person with speech bubble, used sparingly to voice the "moral" of the diagram
- **Layout feel**: generous whitespace, never crowded, every card has breathing room

## Workflow

Copy this checklist and check off items as you complete them:

```
Handdrawn Infographic Progress:

- [ ] Step 1: Parse input & pick layout archetype ⚠️ REQUIRED
  - [ ] 1.1 Identify the rhetorical shape (overview / comparison / mechanism / progression)
  - [ ] 1.2 Extract entities, relations, and key takeaways
  - [ ] 1.3 Pick ONE archetype: grid | comparison | single-scene | progression-strip
- [ ] Step 2: Draft layout plan + image prompt
  - [ ] 2.1 Sketch the block layout in ASCII
  - [ ] 2.2 List every labeled element with its color role
  - [ ] 2.3 Write the full English image prompt using the template
- [ ] Step 3: Confirmation gate ⛔ BLOCKING
- [ ] Step 4: Generate image via Gemini (only after confirmation)
- [ ] Step 5: Deliver image + prompt
```

## Step 1: Parse Input & Pick Layout ⚠️ REQUIRED

Load `references/layout-archetypes.md` for the decision rules and visual examples.

Ask these questions about the input text, in order:

1. **How many top-level units are there?**
   - Source text leans on a concrete metaphor (scaffolding, garden, iceberg, factory) → `metaphorical-illustration` (check this FIRST when a metaphor is the spine of the argument)
   - Structure is organized around a center with outer layers (core → ring → ring) → `concentric-radial`
   - Same structure shown at 3–4 stages of growth → `progression-strip`
   - 1 mechanism / 1 process → `single-scene`
   - 2 opposed things → `comparison` (use sequential-comparison sub-variant when phase-1 hands off to phase-2)
   - 3–6 parallel items → `grid`
   - 7+ items → ask user to reduce or pick a subset; do not cram

2. **What is the reader's takeaway?**
   - "how X works step-by-step" → `single-scene` with numbered steps and flow arrows
   - "X vs Y, pick the right one" → `comparison` with a central divider (explosion-star / vertical line)
   - "here are N patterns to know" → `grid` with per-cell title + mini-diagram + italic one-liner

3. **Are there named roles / actors?**
   - Yes → each becomes a labeled rounded card with a mini-icon
   - No → use generic shapes (Step 1 / Step 2 / Worker A) but still label them

Extract and write down explicitly:
- **Title** — OPTIONAL. Only include a top-of-canvas title when:
  - The diagram has no character cameo / speech bubble carrying the moral, AND
  - The diagram has ≥4 distinct units (grid, sequential-comparison, progression-strip)
  Skip the title when a speech bubble already voices the moral, or when the
  diagram is a small single-scene where the subject is self-evident from the
  top node's label. A redundant title crowds the canvas and weakens the
  punchline. Default to skip unless one of the above conditions is met.
- **Entities** (list of boxes that will appear)
- **Relations** (arrows: which → which, and the label on each arrow)
- **Key quotes** (≤2, these get highlighter blocks)
- **Optional cameo** (if the text has a "moral" or punchline worth putting in a speech bubble)
- **Watermark** — default `none` (the prompt always negates platform watermarks like Gemini's auto-stamp). If the user explicitly asks for a signature / handle / brand / date watermark, capture: (a) exact text, (b) position (default `bottom-right` if unsure — but ask before generating). See `references/prompt-template.md` "Watermark policy".

## Step 2: Draft Layout Plan + Image Prompt

### 2.1 ASCII layout sketch

Draw the blocking in ASCII so the user can eyeball proportions. Examples:

```
Grid (2+2+1):              Comparison:              Single-scene:
┌─────────┬─────────┐      ┌──────┬──────┐          ┌──────────────┐
│  Cell 1 │  Cell 2 │      │      │      │          │   Main Node  │
├─────────┼─────────┤      │  A   ✱  B   │          └──┬────┬────┬─┘
│  Cell 3 │  Cell 4 │      │      │      │             ▼    ▼    ▼
├─────────┴─────────┤      │      │      │          [sub][sub][sub]
│      Cell 5        │     └──────┴──────┘             └────▼────┘
└───────────────────┘       (star divider)              [funnel]
```

### 2.2 Element list

Enumerate every labeled shape with its color role. Every card must pick a color from the palette in `references/prompt-template.md`. Example:

- `Parent Agent` — dusty rose rounded rectangle, chain-icon top-right
- `Sub-Agent A/B/C` — peach rounded rectangles, dashed-outline to signal isolation
- `Funnel` — black line-art, no fill, labeled "compressed result"
- Highlight: `"Context stays clean"` — sage-green highlighter block

### 2.3 Image prompt

Load `references/prompt-template.md` and fill the template. The prompt must:
- Be in English (Gemini handles English style cues more reliably)
- Explicitly name: hand-drawn, cream paper background, pastel palette, rounded rectangles, wobbly lines
- List every card's label verbatim (the model renders text more accurately when enumerated)
- Specify arrow directions and labels
- Declare the aspect ratio (default `16:9` for grid/comparison, `4:3` for single-scene)

## Step 3: Confirmation Gate ⛔ BLOCKING

Present to the user:
1. The layout archetype choice (+ one sentence why)
2. The ASCII sketch
3. The element list with colors
4. The full image prompt

Then ask:

> 这份布局和 prompt 看起来对吗？确认后我用 Gemini 生图。
> - ✅ Go — 确认生图
> - ✏️ Tweak — 指出哪里要改
> - 🎨 Restyle — 换个布局原型
> - 📝 Prompt only — 只要 prompt，不生图

Do NOT call the image API before receiving an affirmative.

## Step 4: Generate via Gemini

Only reachable after Step 3 confirmation.

- Model: `gemini-2.5-flash-image` (nano-banana) for iteration speed. Upgrade to a higher-fidelity Imagen model only if the user explicitly asks.
- Proxy: the user already has `HTTPS_PROXY` + `NO_PROXY` configured (see memory `proxy_config_pattern.md`). Do not re-configure.
- Reuse pattern: if a Gemini image script from a prior project (e.g. Literal Comic Lab) is on disk and reusable, invoke it. If nothing reusable exists, ASK the user — do not invent an API key path or CLI name.
- Output: save to `~/Desktop/handdrawn-<slug>-<YYYYMMDD-HHMM>.png`, then print the path.

## Step 5: Deliver

Return:
1. The image path (and inline preview if the harness supports it)
2. The final prompt used, verbatim (so the user can tweak and re-run externally)
3. ONE short suggestion for variation (e.g. "swap dusty rose for sage if you want a cooler tone") — not a list

## Anti-Patterns

Do NOT do any of the following — each one kills the style:

- Saturated colors, neon, gradients, drop shadows, 3D bevels
- Geometric-perfect lines (SVG-clean look). The wobble IS the style.
- Corporate-slides layout with centered titles and bullet points
- Cramming 7+ cells to "fit everything" — offer to split into 2 diagrams
- Generating without showing the layout plan first (violates Iron Law)
- Writing the prompt in Chinese (Gemini renders English style cues more consistently; Chinese text inside cards is fine)
- Adding decorative elements not justified by the input text
- **Slapping a top-of-canvas title when a speech bubble already carries the moral** — pick one, not both. Speech bubbles usually win because they give the diagram a voice.
- **Writing false-precision numbers on qualitative axes** — e.g. labeling a Human-vs-AI autonomy axis as "Human 100% → AI 100%". If the source text doesn't give you a real metric, use qualitative stage labels ("人驱动" / "AI 建议" / "AI 驱动·人否决") connected by a single directional arrow. Numbers without a source are noise.
- Using emoji characters inside cards (use hand-drawn line icons; emojis in the prompt as icon hints are fine)
- Clean sans-serif PowerPoint-style titles — use a handwritten/serif-hybrid feel
- Skipping the character cameo when the source text has a punchy "moral" — that's what makes these diagrams memorable
- **Letting the platform's auto-watermark stay on the image** — Gemini will sometimes stamp its own corner badge ("Generated by Gemini" / colored sparkle / "AI" tag) on the cream paper. The prompt MUST always include the platform-watermark negation (see `references/prompt-template.md` "Watermark policy"). If the user wants a personal signature, treat it as a deliberate hand-drawn element with explicit text + position — never rely on the platform's auto-stamp.

## Pre-Delivery Checklist

Before calling the image model, verify:

- [ ] Exactly one layout archetype chosen (not a mashup)
- [ ] Every card in the element list has a named color from the palette
- [ ] Every arrow has a direction AND a label (or an explicit "no label")
- [ ] ≤2 highlighter quotes; highlighter color specified
- [ ] Title is written out (not a placeholder)
- [ ] Prompt explicitly includes: "hand-drawn", "cream background", "pastel", "rounded rectangles", "wobbly lines"
- [ ] Prompt's "do not use" list includes the platform-watermark negation (Gemini badge / "AI-generated" / corner stamp). If user asked for a custom watermark, exact text + position are spelled out as a hand-drawn signature element.
- [ ] Aspect ratio specified
- [ ] User has confirmed (Step 3 gate passed)

After image returns, verify:

- [ ] Background is cream, not white or gray
- [ ] Lines look hand-drawn (wobble, not ruler-straight)
- [ ] No gradient fills; colors are flat pastels
- [ ] All labeled text is legible and matches the element list
- [ ] No platform watermark / Gemini badge / "AI-generated" tag in any corner. If present, regenerate (it's a sign the negation phrase was dropped).
- [ ] No extra invented elements not in the plan

If any post-generation check fails, regenerate with a tightened prompt — do not ship a drift.
