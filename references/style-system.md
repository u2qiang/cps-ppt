# CPS Style System

Use these values verbatim. Do not invent per-page colors, fonts, or sizes.

## Canvas

| Property | Value |
| --- | --- |
| Format | 16:9 |
| Size | 1280 × 720 |
| viewBox | `0 0 1280 720` |
| Safe margin | 60px left/right, 40px top/bottom |
| Content area | x 60–1220, y 120–680 |

## Colors

| Token | HEX | Use |
| --- | --- | --- |
| bg | `#FFFFFF` | main background |
| bg_soft | `#F6F9FF` | alternate background |
| card | `#F8FAFC` | card fill |
| primary_soft | `#EFF6FF` | blue tint block |
| primary_tint | `#DBEAFE` | stronger blue tint |
| accent_soft | `#CFFAFE` | cyan tint block |
| warning_soft | `#FEF3C7` | amber tint block |
| primary | `#2563EB` | titles, icons, key blocks |
| primary_dark | `#1E40AF` | strong text on light blue |
| primary_light | `#3B82F6` | secondary blue |
| primary_lighter | `#60A5FA` | light blue layer |
| accent | `#0891B2` | arrows, secondary emphasis |
| accent_teal | `#0F766E` | third-level emphasis |
| warning | `#F59E0B` | risk / attention |
| warning_dark | `#B45309` | warning text |
| text | `#1E293B` | body and titles |
| text_secondary | `#475569` | descriptions |
| text_tertiary | `#64748B` | eyebrows, footer, captions |
| border | `#E2E8F0` | card borders, dividers |
| success | `#16A34A` | positive marks |
| danger | `#DC2626` | negative marks |

Rules:

- One page uses at most four colors plus neutrals.
- Use `#B45309` for text on `#FEF3C7`; `#F59E0B` alone fails contrast at small sizes.
- Never use `rgba()`.

## Typography

Font stack: `"Microsoft YaHei", "PingFang SC", Arial, sans-serif`

Code stack (only when truly needed): `Consolas, "Courier New", monospace`

| Role | Size | Weight | Ratio band |
| --- | --- | --- | --- |
| Cover title | 66 | bold | 2.5–5× body |
| Section opener | 40 | bold | 2–2.5× |
| Page title | 34 | bold | 1.5–2× |
| Hero number | 40 | bold | 1.5–2× |
| Subtitle | 24 | semibold | 1.2–1.5× |
| Body | 20 | regular | 1× |
| Annotation | 14 | regular | 0.7–0.85× |
| Page number | 12 | regular | 0.5–0.65× |

Safe intermediate sizes: 16, 26, 28, 32. Avoid 18, 22, 30, 44 — they fall outside the declared bands and trigger checker warnings.

## Page Chrome

```xml
<rect width="1280" height="720" fill="#FFFFFF"/>
<rect x="60" y="46" width="6" height="34" rx="3" fill="#2563EB"/>
<text x="80" y="74" font-size="34" font-weight="bold" fill="#1E293B">PAGE TITLE</text>
<text x="80" y="100" font-size="14" letter-spacing="1.2" fill="#64748B">ENGLISH EYEBROW</text>
<line x1="60" y1="120" x2="1220" y2="120" stroke="#E2E8F0" stroke-width="1"/>
<text x="60" y="700" font-size="12" fill="#64748B">DECK LABEL</text>
<text x="1220" y="700" text-anchor="end" font-size="12" fill="#64748B">02 / 16</text>
```

## Components

### Card With Tab Header

```xml
<rect x="60" y="150" width="380" height="486" rx="16" fill="#F8FAFC" stroke="#E2E8F0" stroke-width="1"/>
<path d="M 76 150 h 348 a 16 16 0 0 1 16 16 v 38 h -380 v -38 a 16 16 0 0 1 16 -16 Z" fill="#DBEAFE"/>
<use data-icon="tabler-outline/stack-2" x="88" y="164" width="24" height="24" fill="#2563EB"/>
<text x="122" y="183" font-size="24" font-weight="bold" fill="#1E40AF">Card title</text>
```

Tab path rule: `M (x+16) y h (w-32) a 16 16 0 0 1 16 16 v 38 h -w v -38 a 16 16 0 0 1 16 -16 Z`.

### Icon Chip

```xml
<rect x="82" y="170" width="40" height="40" rx="10" fill="#EFF6FF"/>
<use data-icon="tabler-outline/target" x="92" y="180" width="20" height="20" fill="#2563EB"/>
```

### Numbered Step

```xml
<rect x="684" y="214" width="512" height="76" rx="12" fill="#F8FAFC"/>
<rect x="700" y="232" width="40" height="40" rx="10" fill="#DBEAFE"/>
<text x="720" y="259" text-anchor="middle" font-size="16" font-weight="bold" fill="#1E40AF">1</text>
<text x="756" y="248" font-size="20" font-weight="bold" fill="#1E293B">Step title</text>
<text x="756" y="274" font-size="16" fill="#475569">One-line detail</text>
```

### Chip

```xml
<rect x="682" y="504" width="160" height="56" rx="10" fill="#FFFFFF"/>
<text x="762" y="539" text-anchor="middle" font-size="16" font-weight="bold" fill="#1E293B">FCFS</text>
```

### Table

- Header band: `#EFF6FF`, height 44, `rx=8`.
- Row height 46; separators `#E2E8F0` 1px.
- Method column starts at x=596; numeric columns at x=824, 954, 1084; status column at x=1160.
- Status uses `#16A34A` (positive) or `#DC2626` (negative).

### Timeline

```xml
<line x1="200" y1="216" x2="1080" y2="216" stroke="#DBEAFE" stroke-width="4"/>
<circle cx="300" cy="216" r="14" fill="#2563EB"/>
<text x="300" y="184" text-anchor="middle" font-size="24" font-weight="bold" fill="#2563EB">Phase</text>
<text x="300" y="252" text-anchor="middle" font-size="16" fill="#64748B">Duration</text>
```

### Warning Block

```xml
<rect x="60" y="500" width="560" height="160" rx="16" fill="#FEF3C7"/>
<use data-icon="tabler-outline/alert-triangle" x="82" y="520" width="24" height="24" fill="#B45309"/>
<text x="116" y="539" font-size="20" font-weight="bold" fill="#B45309">Section title</text>
```

### Formula Card

```xml
<rect x="620" y="180" width="290" height="88" rx="12" fill="#EFF6FF"/>
<text x="638" y="210" font-size="14" fill="#64748B">Label</text>
<text x="638" y="240" font-size="16" font-weight="bold" fill="#1E40AF">Formula</text>
```

## Icon Inventory

Use only these verified `tabler-outline` names:

`target, sitemap, stack-2, binary-tree, chart-bar, math, database, cpu, activity, lock, file-text, network, route, checklist, calendar, alert-triangle, book-2, settings, shield-check, clock, bulb, flag, circle-check, x, check, arrows-exchange, search, hierarchy, code, divide, server, device-desktop, refresh, users, arrow-right, arrow-down, arrow-narrow-right`

## Do / Don't

- Do vary composition: cards, split, table, flow, timeline, layered stack, mind map.
- Do use one idea per page and one accent color per block.
- Don't repeat the same 3-card grid on every page.
- Don't use shadows on peer cards; reserve them for at most one floating element.
- Don't put paragraphs inside cards; split into bullets or a second page.
