# Layout Archetypes

Six archetypes cover the vast majority of "structured text → hand-drawn infographic" requests. Pick exactly one per image. Do not mash them up.

## Table of Contents
1. [Decision tree](#decision-tree)
2. [Archetype A: Grid](#archetype-a-grid)
3. [Archetype B: Comparison](#archetype-b-comparison)
4. [Archetype C: Single-scene](#archetype-c-single-scene)
5. [Archetype D: Progression strip](#archetype-d-progression-strip)
6. [Archetype E: Metaphorical illustration](#archetype-e-metaphorical-illustration)
7. [Archetype F: Concentric radial](#archetype-f-concentric-radial)
8. [Handling edge cases](#handling-edge-cases)

## Decision tree

```
Does the text lean on a CONCRETE METAPHOR (scaffolding, garden, iceberg,
bridge, tree-of-life, factory) to carry the concept?
├─ Yes → Metaphorical illustration (one drawn scene, labels attached to parts)
└─ No → Does the text describe structure arranged AROUND A CENTER, with
        progressive outer layers (core → inner ring → outer ring)?
        ├─ Yes → Concentric radial
        └─ No → Does the text describe the SAME structure at different points
                in time / scale, showing it growing or degrading?
                ├─ Yes → Progression strip (3–4 panels of same thing evolving)
                └─ No → ask: how many top-level units?
                        ├─ 1 → Single-scene (explaining ONE thing in depth)
                        ├─ 2 → Comparison (only if contrasted)
                        ├─ 3–6 → Grid (siblings at same level of abstraction)
                        └─ 7+ → Tell user to reduce. Offer to:
                                (a) pick the top N
                                (b) group into 2–3 meta-buckets
                                (c) produce a series of diagrams
```

Secondary question: does the text have **sequential flow** (step 1 → step 2 → ...)?
- Yes, and sequence is the point → single-scene with numbered step pills
- Yes, but only incidentally → whatever archetype the unit-count suggests
- No → archetype by unit count

Key disambiguation — `progression strip` vs `grid` vs `comparison`:
- **Grid** = N distinct things side-by-side (different patterns, different categories)
- **Comparison** = 2 contrasted things (A vs B, pick one)
- **Progression strip** = the SAME thing shown at 3–4 stages — turn 1 → turn 2 → turn 3, or small → medium → large. The panels share internal vocabulary; what changes is the quantity or state.

## Archetype A: Grid

**When**: Text lists N parallel patterns / options / principles, all at the same level.

**Signal phrases in input**: "here are the N X", "five patterns", "seven principles", "four types of Y".

**Structure**:
- Uniform cell size (2×2, 2×3, 3×2, or 2+2+1 with the last cell spanning full width)
- Each cell contains: title + tiny icon (top-left) + mini-diagram (3–5 shapes) + italic one-line summary
- Shared header above the grid with the overall title
- Optional: a highlighter block on ONE cell to mark "most important" or "most common"

**Mini-diagram conventions inside cells**:
- Use simple flow shapes: `[A]→[B]→[C]` or `[Input]→[fork]→[A/B/C]→[merge]`
- Keep it to ≤5 shapes per cell — more won't read at grid size
- Label every arrow (or leave deliberately unlabeled with a note)

**Cell-count layouts**:
- 4 items → 2×2
- 5 items → 2+2+1 (last cell full width, good for the "synthesis" pattern)
- 6 items → 3×2 or 2×3

## Archetype B: Comparison

**When**: Text explicitly contrasts two approaches / paradigms / options.

**Signal phrases**: "X vs Y", "use X when / use Y when", "two paradigms", "old way / new way".

**Structure**:
- Canvas split vertically in two columns of equal width
- Each side has its own title at the top
- Middle divider: a hand-drawn vertical line OR an explosion/star shape (the "vs" marker)
- Both sides should have parallel internal structure (same kind of diagram, same number of sub-elements) — this is what makes the comparison read instantly
- Optional footer row across the bottom: a single highlighter-block summarizing "choose X when ...; choose Y when ..."

**Color convention**: the two sides use two different pastel primaries to reinforce the split. E.g. dusty rose (left) vs sage green (right).

**Common failure**: making the two sides have different internal shapes. Don't — if one side has 3 sub-cards, the other should too.

**Sub-variant — Sequential comparison (Phase 1 → Phase 2)**: When the two sides represent consecutive stages that hand off state to each other (not alternatives to choose between), use a *dashed vertical divider* (not a solid line or explosion star) and add a clear horizontal **handoff arrow** crossing the divider with a label like "KV Cache handed off" or "state passed to next phase". Titles become "Phase 1: X" / "Phase 2: Y" rather than neutral "X" / "Y". Inside each phase, feel free to use domain visualizations like **tensor/matrix grids** (3×5 array of small colored squares to represent Q/K/V tensors — pastel gray/orange/green fills). Add a compute-mode icon at the bottom of each phase: 🔥 line-art flame for compute-heavy, 💾 floppy/disk for memory-bound.

## Archetype C: Single-scene

**When**: Text explains ONE mechanism, process, or workflow in depth.

**Signal phrases**: "how X works", "the steps are", "first... then... finally", "the parent does A, which causes B".

**Structure**:
- One dominant central node at the top (the "protagonist")
- Arrows radiating down to sub-nodes (children, workers, steps)
- Optional funnel / merge at the bottom to show "results converge"
- Step-number pills on arrows: small circles with "1", "2", "3" and a label
- Character cameo (optional but encouraged): a stick-figure in the top-right or bottom-left with a speech bubble voicing the moral
- Dashed outlines to mark "isolated" contexts; X-marks to mark "forbidden" paths

**Flow directions (pick one, stick to it)**:
- Top-down (most common for hierarchy)
- Left-to-right (for linear sequences of 3–5 steps)
- Circular (for feedback loops — generator ↔ evaluator; avoid otherwise)

**Density budget**: 5–9 labeled shapes total. More than that → split into two diagrams or switch to grid.

## Archetype D: Progression strip

**When**: Text shows the **same structure evolving across time / scale**. Each panel shares internal vocabulary; what changes is size, quantity, or state. Classic use cases: "turn 1 vs turn 2 vs turn 3 of an agent conversation", "small / medium / large dataset", "before / during / after an incident", "iteration 1 → 2 → 3 of a loop".

**Signal phrases in input**: "on turn N", "first... then... then...", "three consecutive X", "after 50 turns", "redundant computation billed every turn", "over time", "as X grows".

**Structure**:
- Canvas split horizontally into **3 or 4 panels of equal width** (2 is a comparison, not progression)
- Each panel contains the **same diagram vocabulary** (same card shapes, same color scheme for matching roles)
- What changes panel-to-panel: number of cards, cumulative stack, or state annotations
- Small annotation above/beside each panel naming the stage (e.g. "Turn 1", "Turn 2", "Turn 3")
- A side-annotation with a vertical bracket `{` labeling a cumulative region (e.g. "Re-processed from scratch", "Redundant computation") — this is the archetype's signature move
- Optional callout arrow from one panel to a thought-bubble or note ("I've seen most of this before...")

**Color convention**: roles that persist across panels keep the SAME color. If `System Prompt` is baby-blue in panel 1, it must be baby-blue in panel 2 and 3. This is what makes the "growing" effect legible.

**Panel-count guidance**:
- 3 panels = standard (first / middle / accumulated)
- 4 panels = only if each stage introduces a genuinely new element; otherwise 3 is cleaner

**Common failures**:
- Changing the order or style of shared cards between panels (breaks visual continuity)
- Letting one panel get much denser than the others (keep visual weight balanced even though content grows — use whitespace)
- Forgetting the vertical bracket annotation — it's what turns "3 pictures" into "one argument about accumulation"

## Archetype E: Metaphorical illustration

**When**: The source text leans on a concrete metaphor — scaffolding, garden, iceberg, factory, bridge, ladder, construction site, tree, body/anatomy — to carry the abstract concept. The metaphor itself is the argument; stripping it to abstract boxes kills the point.

**Signal phrases**: "like a scaffolding", "think of it as a X", "imagine X", "X is like a Y", explicit analogies, metaphorical titles.

**Structure**:
- ONE drawn scene depicting the metaphor literally (the scaffolding, the garden, etc.) taking up most of the canvas
- Labels attached to parts of the scene with hand-drawn leader lines pointing from label box to the part being labeled
- Label boxes are small rounded rectangles in pastel fills, placed in the whitespace around the scene — NOT overlapping the illustration
- 1 optional stick-figure character interacting with the scene (worker on scaffolding, gardener in garden) to humanize it
- Optional highlighter block at the bottom with the one-sentence moral

**Scene conventions**:
- Draw the metaphor in the same wobbly hand-drawn ink style — no photorealism
- Use 1–2 pastel fills within the scene (e.g. scaffolding planks in peach, tool belt in sage); keep the rest black line-art
- Leader lines are thin wobbly black strokes; arrowheads optional
- 4–8 labels max — beyond that the scene gets noisy; split into 2 diagrams

**Common failures**:
- Making the scene photorealistic or too detailed — defeats the hand-drawn feel
- Labeling every tiny element — pick the parts that map to concepts in the text
- Using the metaphor as just a small icon inside a grid cell (that's a grid, not this archetype)

## Archetype F: Concentric radial

**When**: Text describes a structure organized around a center with progressive outer layers — core mission → inner practices → outer effects, or nucleus → mechanisms → manifestations. The "by-the-layer" reading order is the point.

**Signal phrases**: "at the core / at the center", "surrounding it", "the outer layer", "built around", "radiates out from", "inside out", "三层/四层结构".

**Structure**:
- Concentric rings (2–4 layers) centered on the canvas, OR a radial petal/flower layout with a central hub
- Innermost shape is the "core" — usually dusty rose or sage-green filled rounded circle with bold title
- Each outer ring is a ring-shaped band (hand-drawn, wobbly) with its own pastel fill; different from neighbors for legibility
- Each ring is segmented into 3–6 sector labels (like a pie) — each sector contains a short label and optional icon
- OR: the outermost layer fans out as separate "petal" rounded rectangles anchored by short arrows to the core
- Generous whitespace OUTSIDE the outermost ring — don't push to canvas edges
- Optional stick-figure cameo outside the rings with a speech bubble voicing the moral

**Color convention**: Inner ring darkest / most saturated within the pastel range (dusty rose), outer rings lighter (lavender → baby-blue → peach). Never more than 4 rings — readability collapses.

**Aspect ratio**: prefer `1:1` (square) or `4:3`. Wide `16:9` wastes side space on a circular form.

**Common failures**:
- Uneven sector sizes in the same ring (breaks the "equal siblings" read)
- More than 4 rings (becomes a target board, not an infographic)
- Filling the outermost ring to the canvas edge (no breathing room kills the hand-drawn feel)
- Tiny unreadable labels in inner rings — inner rings hold 1–3 words max; longer phrases belong in outer rings

## Handling edge cases

| Situation | Resolution |
|---|---|
| Text has both "N patterns" AND deep explanation of one | Offer to produce 2 images: a grid overview + a single-scene deep dive |
| Text is a comparison but has 3+ sides | Not a comparison — it's a grid. Each cell becomes one option. |
| Text is really a linear 7-step process | Use single-scene left-to-right, break into two rows if needed |
| User asks for a mind-map tree | Out of scope — single-scene with a central root handles 2 levels; beyond that suggest a real mind-map tool |
| Input is a list of 10+ items | Ask user to pick top 5 or bucket them; do not cram |
