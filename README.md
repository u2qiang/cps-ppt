# CPS-PPT

A Codex skill for building clean professional 16:9 slide decks in the **CPS / 清爽专业风** visual style.

## What It Does

- Locks a consistent visual system: light background, blue-teal accents, rounded cards, thin line icons.
- Provides 12 page recipes: cover, KPI overview, process flow, dense table, layered architecture, timeline, formula grid, and more.
- Encodes a complete pipeline: source → outline → SVG pages → quality check → speaker notes → editable PPTX.
- Includes two reference SVGs and a list of common layout defects with fixes.

## Install

Copy or clone this folder into your Codex skills directory:

```powershell
git clone https://github.com/u2qiang/cps-ppt.git "$HOME\.codex\skills\cps-ppt"
```

Or copy the existing folder:

```powershell
Copy-Item -Recurse . "$HOME\.codex\skills\cps-ppt"
```

Restart Codex or start a new turn so the skill is discovered.

## Usage

Invoke it explicitly:

```text
$cps-ppt
```

Or ask naturally:

```text
Use CPS-PPT to turn this Markdown into a 12-page clean professional deck.
用 CPS-PPT 把这份材料做成清爽专业风的 PPT。
```

## Structure

```text
cps-ppt/
├─ SKILL.md
├─ agents/
│  └─ openai.yaml
├─ references/
│  ├─ style-system.md
│  ├─ slide-recipes.md
│  └─ pipeline.md
└─ assets/
   ├─ reference-cover.svg
   └─ reference-cards.svg
```

## Requirements

- Codex with skills support.
- [`ppt-master`](https://github.com/) scripts for SVG quality checking and PPTX export:
  `project_manager.py`, `svg_quality_checker.py`, `total_md_split.py`, `finalize_svg.py`, `svg_to_pptx.py`.
- Python with `python-pptx`, `Pillow`, and `lxml`.

If `ppt-master` is unavailable, `SKILL.md` instructs the agent to stop and ask before using a reduced fallback.

## Notes

CPS-PPT is a **style and workflow layer**. It does not bundle PPT-MASTER; it calls the installed PPT-MASTER scripts. This keeps the skill lightweight and lets the conversion engine be updated independently.