# CPS Pipeline

Use this as the execution checklist. Keep SVG generation in the main agent; do not batch-generate pages with a script.

## Prerequisites

- Python with `python-pptx`, `Pillow`, `lxml`.
- `ppt-master` available at `~/.agents/skills/ppt-master` (or `$CODEX_HOME/skills/ppt-master`).
- Chrome or Edge available for PNG visual QA.
- If `ppt-master` is missing, stop and ask the user before using a reduced fallback.

## Step 1 — Source And Outline

Produce a page-by-page outline with:

- Slide number and title.
- 3–5 key points per slide.
- Layout recipe from `slide-recipes.md`.
- Any required images (CPS decks normally use none).

Confirm the outline with the user when the deck is substantial; proceed directly for small decks.

## Step 2 — Project Init

```powershell
$PPT = "$HOME\.agents\skills\ppt-master\scripts"
python "$PPT\project_manager.py" init <name> --format ppt169 --dir <output_dir>
python "$PPT\project_manager.py" import-sources <project> <source.md> --copy
```

Use `--copy`, not `--move`, unless the user explicitly wants the source moved.

## Step 3 — Design Lock

Write `spec_lock.md` with the tokens from `style-system.md`:

```markdown
## canvas
- viewBox: 0 0 1280 720
- format: PPT 16:9

## colors
- bg: #FFFFFF
- primary: #2563EB
...

## typography
- font_family: "Microsoft YaHei", "PingFang SC", Arial, sans-serif
- body: 20
- title: 34
- subtitle: 24
- annotation: 14
- cover_title: 66
- hero_number: 40

## icons
- library: tabler-outline
- stroke_width: 2
- inventory: target, stack-2, binary-tree, ...

## page_rhythm
- P01: anchor
- P02: dense
```

Every color used in an SVG must appear in `spec_lock.md`.

## Step 4 — Generate SVGs Sequentially

- One file per page: `svg_output/NN_page_name.svg`.
- Read `spec_lock.md` before each page.
- Keep the page chrome identical; vary the content area.
- Use `<use data-icon="tabler-outline/<name>" .../>` placeholders.
- Do not use `<foreignObject>`, `<style>`, `class`, `rgba()`, or `<g opacity>`.
- Wrap long text with `<tspan>` and explicit `x`/`dy`.

## Step 5 — Structural Quality Check

```powershell
$env:PYTHONIOENCODING='utf-8'
python "$PPT\svg_quality_checker.py" <project>
```

Fix every error. Warnings about color/font drift mean a token is missing from `spec_lock.md` or an SVG uses an unlisted value.

## Step 6 — Visual QA

Render every page to PNG and inspect:

```powershell
$chrome = 'C:\Program Files\Google\Chrome\Application\chrome.exe'
Get-ChildItem "$project\svg_output" -Filter *.svg | ForEach-Object {
  $png = "$project\qa\$($_.BaseName).png"
  & $chrome --headless=new --disable-gpu --hide-scrollbars --window-size=1280,720 `
    "--screenshot=$png" ("file:///" + ($_.FullName -replace '\\','/')) 2>$null
}
```

Check specifically:

- No text crosses a card or panel edge.
- No panel content extends below its container.
- Table columns do not collide.
- Arrows point right/down where intended.
- Icons are blank before `finalize_svg.py`; that is expected.
- Chinese punctuation and symbols render correctly.

## Step 7 — Speaker Notes

Write `notes/total.md` as pure spoken narration:

```markdown
# 01_cover

Opening sentence...

---

# 02_next_page

...
```

Then:

```powershell
python "$PPT\total_md_split.py" <project>
```

## Step 8 — Finalize And Export

Run the three commands one at a time:

```powershell
python "$PPT\total_md_split.py" <project>
python "$PPT\finalize_svg.py" <project>
python "$PPT\svg_to_pptx.py" <project>
```

Do not replace `finalize_svg.py` with a copy operation. It embeds icons, flattens text, and converts rounded rectangles.

## Common Defects And Fixes

| Symptom | Cause | Fix |
| --- | --- | --- |
| Arrow points left | Polygon apex is on the left | Put the apex at the larger x: `points="x2,y x1,y-8 x1,y+8"` |
| Content spills below a panel | Last baseline is past the panel bottom | Move the block up or reduce line count |
| Table columns touch | Column x positions too close | Widen the gap or move the status column right |
| Icons show as blank squares | `finalize_svg.py` not run | Run finalize before export |
| Font drift warning with `&quot;` | Double-quoted attribute | Use `font-family='"Microsoft YaHei", ...'` |
| Size drift warning | 18/22/44px used | Use 16/24/40 or another allowed size |
| Color drift warning | HEX not in `spec_lock.md` | Add the token or switch to an existing one |
| Card text looks like a paragraph | Too many words | Cut to 3–5 bullets or split the page |
| Deck looks like repeated card grids | Same recipe everywhere | Swap in a split, table, flow, or timeline page |

## Acceptance Checklist

- [ ] 16:9, 1280×720, consistent page chrome.
- [ ] Palette and fonts match `spec_lock.md`.
- [ ] All SVGs pass `svg_quality_checker.py` with 0 errors.
- [ ] Visual QA completed on every page.
- [ ] Speaker notes split 1:1 with SVG pages.
- [ ] `finalize_svg.py` completed.
- [ ] `.pptx` exported with 0 failed slides.
- [ ] Final file copied to a short path and reported to the user.
