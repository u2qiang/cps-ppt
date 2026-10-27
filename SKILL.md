---
name: cps-ppt
description: Build clean professional 16:9 slide decks in the CPS visual style. Use when the user asks for a "清爽专业风" deck, a clean/professional/consulting-style presentation, a structured review or training deck, or invokes CPS-PPT.
---

# CPS-PPT

Produce a 16:9 `.pptx` in the CPS visual system: white or very light blue background, blue-teal accents, rounded cards, thin line icons, and a clear information hierarchy.

## Use This Skill When

- The user asks for 清爽专业风, clean professional, consulting-style, or review-style slides.
- The source is Markdown, notes, a report, an outline, or a topic that should become a structured deck.
- The user accepts editable vector slides (native DrawingML), not one generated photo per page.

Do not use it for photo-led brand campaigns, magazine layouts, hand-drawn illustration decks, or pages that must be a single raster image.

## Output Contract

- Canvas: 16:9, `1280×720`, viewBox `0 0 1280 720`.
- 10–16 pages unless the user specifies another count.
- Every text element and shape remains editable in PowerPoint.
- Keep the project folder with `design_spec.md`, `spec_lock.md`, `svg_output/`, `notes/`, and `exports/`.
- Copy the final `.pptx` to a short, obvious path the user can open.

## Workflow

1. **Read the source and plan the deck.** Identify audience, goal, sections to keep or cut, and page count. Draft a page-by-page outline before writing any slide.
2. **Create the project.** Use `ppt-master`'s `project_manager.py init <name> --format ppt169`. If `ppt-master` is unavailable, tell the user before falling back to a plain `python-pptx` build.
3. **Lock the design system.** Read `references/style-system.md`. Copy its color, typography, spacing, and component tokens into `spec_lock.md`; do not improvise new values per page.
4. **Write `design_spec.md` + `spec_lock.md`.** Include page count, palette, fonts, icon library, page rhythm, and a content outline.
5. **Generate SVGs sequentially.** One page at a time, named `NN_page_name.svg`, into `svg_output/`. Use `references/slide-recipes.md` for page archetypes. Read `spec_lock.md` before every page.
6. **Quality check.** Run `svg_quality_checker.py`, fix every error, then render PNGs and visually inspect for overflow, overlap, and wrong arrow direction.
7. **Write speaker notes.** Put pure spoken narration in `notes/total.md` with `# NN_page_name` headings, then run `total_md_split.py`.
8. **Finalize and export.** Run `finalize_svg.py` then `svg_to_pptx.py`. Never substitute `cp` for `finalize_svg.py`.
9. **Report.** Give the final PPTX path, page count, and any limitations.

## Non-Negotiable Style Rules

- Background: `#FFFFFF` or `#F6F9FF`; cards `#F8FAFC`; borders `#E2E8F0`.
- Primary `#2563EB`, accent `#0891B2`, teal `#0F766E`, warning `#F59E0B`, warning-dark `#B45309`.
- Text `#1E293B`, secondary `#475569`, tertiary `#64748B`.
- Font: `"Microsoft YaHei", "PingFang SC", Arial, sans-serif`. Body 20px, page title 34px, subtitle 24px, annotation 14px, page number 12px.
- Icons: `tabler-outline` only, `stroke-width="2"`, via `<use data-icon="tabler-outline/<name>" .../>`.
- Header: 6×34px primary bar at `x=60,y=46`; title at `x=80,y=74`; eyebrow at `y=100`; divider at `y=120`.
- Footer: left label at `x=60,y=700`, page number right-aligned at `x=1220,y=700`.
- Cards: `rx=14–16`, 22–24px padding, 24px gap, no heavy shadows.
- Use 3–5 bullets per card. Never fill a card with a paragraph wall.
- Keep one visual identity but vary page composition: cards, split, table, flow, timeline, layered stack, mind map.

## Hard SVG / PPT Constraints

- No `mask`, `<style>`, `class`, `<foreignObject>`, `textPath`, `animate*`, `script`, `@font-face`, `<symbol>`, or `<g opacity>`.
- No `rgba()`; use `fill-opacity` / `stroke-opacity`.
- Use raw Unicode for `— → × ÷ ≥ ≤ · ⌈ ⌉ ⌊ ⌋`; never HTML named entities.
- Escape XML reserved characters as `&amp; &lt; &gt; &quot; &apos;`.
- Icons are placeholders until `finalize_svg.py`; blank icon chips in a browser preview are expected before that step.
- Every text size must stay inside the ramp bands in `references/style-system.md`.

## Reference Map

- `references/style-system.md` — colors, typography, spacing, header/footer, component specs.
- `references/slide-recipes.md` — page archetypes with coordinates and layout skeletons.
- `references/pipeline.md` — commands, QA loop, common defects, and fixes.
- `assets/reference-cover.svg` — cover structure reference.
- `assets/reference-cards.svg` — three-card content structure reference.

## Default Commands

```powershell
$PPT = "$HOME\.agents\skills\ppt-master\scripts"
python "$PPT\project_manager.py" init <name> --format ppt169 --dir <output_dir>
python "$PPT\svg_quality_checker.py" <project>
python "$PPT\total_md_split.py" <project>
python "$PPT\finalize_svg.py" <project>
python "$PPT\svg_to_pptx.py" <project>
```

If `ppt-master` is not present, stop and ask the user whether to install it or use a reduced `python-pptx` fallback.
