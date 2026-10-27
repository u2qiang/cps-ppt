# CPS Slide Recipes

Pick a recipe by the page's information shape. Adapt the geometry; do not copy the same layout on adjacent pages.

## 1. Cover

Use for the opening page.

- Left column x=60–620: eyebrow at y=94, two-line title at y=210/296, subtitle at y=380, pill at y=420–472, source note at y=556.
- Right column x=720–1180: 2×2 subject cards, each 216×158, gaps 28px.
- Add two soft background circles: one at top-right, one at bottom-left, using `#EFF6FF` / `#F6F9FF`.

## 2. Overview With Donut

Use for 3–6 part proportions with a headline total.

- Donut center `(330,390)`, outer radius 170, inner radius 105.
- Center total 40px bold; label 14px below.
- Legend in two columns above and below the chart.
- Right side: 2×2 cards, each 264×196, at x=640/936 and y=152/372.

Donut arc formula for a segment from angle a1 to a2:

```
M cx+R·cos(a1),cy+R·sin(a1)
A R,R 0 largeArc 1 cx+R·cos(a2),cy+R·sin(a2)
L cx+r·cos(a2),cy+r·sin(a2)
A r,r 0 largeArc 0 cx+r·cos(a1),cy+r·sin(a1) Z
```

## 3. Knowledge Map

Use for one core concept radiating into 4 branches.

- Center circle `(640,380)`, r=88, blue→teal gradient.
- Branch anchors at `(330,240)`, `(950,240)`, `(330,520)`, `(950,520)`.
- Connectors 3px `#DBEAFE`; branch dots r=6.
- Branch titles 28px bold; one-line description 16px; weight line 14px.
- Bottom takeaway centered at y=626; divider above at y=644.
- This is a `breathing` page: no card grid.

## 4. Three-Column Cards

Use for three parallel concepts or comparisons.

- Cards at x=60/450/840, y=150, 380×486, gap 30.
- Top tab band height 54; icon 24px at x+28, y+14; title 24px at x+62.
- Body bullets start at y=240; 5px dot + 20px heading + 16px detail.
- Bottom tint block inside each card: x+28, y+286, width 324, height 146.

## 5. Split Diagram + List

Use when one half needs a diagram and the other a list.

- Left panel: x=60, y=150, 560×486, `#F8FAFC`, border.
- Right panel: x=660, y=150, 560×486.
- Diagram area: y=214–400. List rows: 48px height, 12px gap, starting y=420.
- Keep diagram labels ≥14px.

## 6. Dense Table

Use for 6–9 rows of comparable values.

- Table x=580–1220, header y=184–228, rows 46px.
- Columns: method x=596, average x=824, worst x=954, space x=1084, status x=1160.
- Left side holds 2–3 summary cards at x=60, width 480.

## 7. Process Flow

Use for 3–8 sequential steps.

- Boxes 200×72, gap 24, starting x=60, y=150.
- Arrows: standalone triangle polygons, apex on the **right**:
  `<polygon points="x2,y x1,y-8 x1,y+8" fill="#0891B2"/>`
- Numbered or labeled steps; each step gets one line of detail.

## 8. Two-By-Two Cards

Use for four parallel conditions, risks, or dimensions.

- Cards 250×108, gap 16, at x=682/948, y=214/336.
- Title 20px bold; detail 14px centered.
- Use `#FEF3C7` for caution themes, `#EFF6FF` for neutral themes.

## 9. Layered Architecture

Use for OSI/TCP-IP, stack diagrams, or 3–5 horizontal layers.

- Columns 200–220 wide, gap 60.
- Layer block height 50–62, gap 6–8.
- Align all columns on the same top y=180 and keep the last block above y=470.
- Label each column above at y=166.

## 10. Timeline + Warning

Use for phased plans and common mistakes.

- Timeline line y=216, from x=200 to 1080.
- Three nodes at x=300/640/980, r=14; phase label above, duration below.
- Phase cards 280×190 at y=286, x=node−140.
- Bottom row: 560×160 cards at x=60/660, y=500.

## 11. Formula Grid

Use for a cheat-sheet page.

- Left list panel x=60, 520×420.
- Right formula grid: 2 columns × 4 rows, cards 290×88, gaps 20/12.
- Bottom strip 600×60 for supplementary formulas.
- Formula text 16px bold; label 14px.

## 12. Closing / Plan

Use for the final page.

- Reuse the timeline recipe for three phases.
- Add one warning block for common mistakes.
- End with a single-line takeaway or action, not a generic "Thank you".

## Layout Variety Check

Before generating, list the recipe used per page. If three consecutive pages use the same recipe, change one of them.
