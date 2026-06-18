---
name: figma-essential
description: How to use Figma MCP (figma-developer-mcp) to fetch real design specs from Figma URLs or nodes, eliminating UI guesswork.
triggers: ['figma', 'convert figma', 'build from figma', 'implement design', 'figma mcp']
priority: medium
---

# Essential Figma MCP Notes

## When to use this

Use this workflow when the user:

- provides a Figma URL
- provides a Figma frame or node context
- asks things like "convert this Figma", "build this page", "implement this design"

## Hard requirement

Always use Figma MCP to fetch real design data.
Never guess, approximate, or invent design values.
If Figma MCP is unavailable, stop and tell the user.
Do not use WebFetch as a fallback for Figma URLs.

## MCP server: figma-developer-mcp

This project uses `figma-developer-mcp` configured in `.mcp.json` as the `figma-mcp` server.
Two tools are available:

| Tool | Purpose |
|------|---------|
| `mcp__figma-mcp__get_figma_data` | Fetch design data (nodes, styles, components) from a Figma file/node |
| `mcp__figma-mcp__download_figma_images` | Download image assets from Figma nodes to local disk |

## Parse the Figma URL

Typical format:

```
https://www.figma.com/design/{fileKey}/Title?node-id={nodeId}
```

Example:

```
https://www.figma.com/design/nkzHpIeOrtTjZRBdEwJ7DJ/KHACHSANDANANG?node-id=3312-2
```

Extract:

- `fileKey = nkzHpIeOrtTjZRBdEwJ7DJ`
- `nodeId = 3312-2`

## Core Figma MCP calls

### Fetch design data for a specific node

```javascript
mcp__figma-mcp__get_figma_data({
  fileKey: 'nkzHpIeOrtTjZRBdEwJ7DJ',
  nodeId: '3312-2',
  depth: 5,
})
```

### Fetch entire file

```javascript
mcp__figma-mcp__get_figma_data({
  fileKey: 'nkzHpIeOrtTjZRBdEwJ7DJ',
})
```

### Fetch with shallow depth (large files)

```javascript
mcp__figma-mcp__get_figma_data({
  fileKey: 'nkzHpIeOrtTjZRBdEwJ7DJ',
  nodeId: '3312-2',
  depth: 2,
})
```

### Download image assets

Images are saved to `/public/assets/images/` (web-accessible folder).

```javascript
mcp__figma-mcp__download_figma_images({
  fileKey: 'nkzHpIeOrtTjZRBdEwJ7DJ',
  nodes: {
    '4029:12345': { filePath: 'hero.png', scale: 2, format: 'png' },
    '4029:67890': { filePath: 'logo.svg', format: 'svg' },
  },
  localPath: '/public/assets/images',
})
```

After download, reference images with `/assets/images/hero.png` in HTML/CSS.

### Selection rule

- one specific node → `get_figma_data` with `nodeId`
- entire page or file → `get_figma_data` without `nodeId`
- image/icon export → `download_figma_images` → save to `/public/assets/images/`

## Response shape from get_figma_data

```json
{
  "name": "File name",
  "document": {
    "id": "0:0",
    "name": "Document",
    "type": "DOCUMENT",
    "children": [...]
  },
  "components": {},
  "styles": {}
}
```

When `nodeId` is specified, the response focuses on that node subtree.

## Fields to extract from Figma

### Colors

- `node.fills[0].color` — Figma returns `r`, `g`, `b` in `0–1` range

Convert to CSS:

```
r_css = round(r * 255)
g_css = round(g * 255)
b_css = round(b * 255)
→ color: rgb(r_css, g_css, b_css);
→ or with alpha: color: rgb(r_css g_css b_css / a);
```

### Typography

- `node.style.fontFamily`
- `node.style.fontWeight`
- `node.style.fontSize`
- `node.style.letterSpacing`
- `node.style.lineHeightPx`
- `node.style.textAlignHorizontal`
- `node.characters`

### Layout / Auto Layout

- `node.layoutMode` (`HORIZONTAL` | `VERTICAL` | `NONE`)
- `node.primaryAxisAlignItems`
- `node.counterAxisAlignItems`
- `node.layoutWrap`
- `node.itemSpacing`
- `node.paddingLeft` / `paddingRight` / `paddingTop` / `paddingBottom`
- `node.primaryAxisSizingMode`
- `node.counterAxisSizingMode`

### Border / effects / opacity

- `node.cornerRadius`
- `node.topLeftRadius` / `topRightRadius` / `bottomLeftRadius` / `bottomRightRadius`
- `node.effects`
- `node.opacity`
- `node.strokes`
- `node.strokeWeight`

### Size / bounds

- `node.absoluteBoundingBox.width`
- `node.absoluteBoundingBox.height`
- `node.absoluteBoundingBox.x`
- `node.absoluteBoundingBox.y`
- `node.rotation`
- `node.layoutGrids`

If a field is missing on a node type, do not invent it — use the returned payload as source of truth.

## Auto Layout to CSS mapping

| Figma field                            | CSS                                     |
| -------------------------------------- | --------------------------------------- |
| `layoutMode: HORIZONTAL`               | `display: flex; flex-direction: row`    |
| `layoutMode: VERTICAL`                 | `display: flex; flex-direction: column` |
| `layoutMode: NONE`                     | no flex container                       |
| `primaryAxisAlignItems: MIN`           | `justify-content: flex-start`           |
| `primaryAxisAlignItems: CENTER`        | `justify-content: center`               |
| `primaryAxisAlignItems: MAX`           | `justify-content: flex-end`             |
| `primaryAxisAlignItems: SPACE_BETWEEN` | `justify-content: space-between`        |
| `counterAxisAlignItems: MIN`           | `align-items: flex-start`               |
| `counterAxisAlignItems: CENTER`        | `align-items: center`                   |
| `counterAxisAlignItems: MAX`           | `align-items: flex-end`                 |
| `counterAxisAlignItems: BASELINE`      | `align-items: baseline`                 |
| `itemSpacing: N`                       | `gap: Npx`                              |
| `layoutWrap: WRAP`                     | `flex-wrap: wrap`                       |
| `layoutGrids[].pattern = COLUMNS`      | `grid-template-columns: repeat(N, 1fr)` |
| `layoutGrids[].pattern = ROWS`         | `grid-template-rows: repeat(N, 1fr)`    |

## Unit conversion

Convert `px` to `rem` by dividing by `16`.

Quick reference:

- `4px = 0.25rem`
- `8px = 0.5rem`
- `12px = 0.75rem`
- `16px = 1rem`
- `24px = 1.5rem`
- `32px = 2rem`

## Image handling

Always download real assets from Figma using `download_figma_images`.
Never use placeholder images (fake image services, generated placeholders, etc.).

Save to `/public/assets/images/` then reference directly in HTML/CSS:

```html
<img src="/assets/images/hero.png" alt="Hero" />
<img src="/assets/images/logo.svg" alt="Logo" />
```

```css
.hero {
  background-image: url('/assets/images/hero.png');
}
```

CSS rules for images:

- avatars: `object-fit: cover`
- logos: `object-fit: contain`

Common image node types to export:

- RECTANGLE with `fills[].type = IMAGE`
- SVG vectors / icon groups
- logos or vector groups
- background images

## Pixel-perfect workflow

The goal is to match Figma output as closely as possible. Follow this order for every component:

### Step 1 — fetch first, code second

Always call `get_figma_data` before writing any code.
Never approximate values from a screenshot or description.

### Step 2 — extract every value literally

Do not round or simplify unless Figma itself shows a round value.

| What to extract | Where to find it |
| --- | --- |
| Width / Height | `absoluteBoundingBox.width`, `absoluteBoundingBox.height` |
| Position (relative to parent) | Calculate from parent and child `absoluteBoundingBox` |
| Background color | `fills[0].color` converted to CSS |
| Border radius | `cornerRadius` or per-corner fields |
| Font family | `style.fontFamily` |
| Font size | `style.fontSize` — convert to `rem` |
| Font weight | `style.fontWeight` |
| Line height | `style.lineHeightPx` — convert to `rem` |
| Letter spacing | `style.letterSpacing` — in `px`, convert to `em` relative to font size |
| Gap between children | `itemSpacing` |
| Padding | `paddingTop`, `paddingRight`, `paddingBottom`, `paddingLeft` |
| Opacity | `opacity` |
| Box shadow | `effects[]` where `type = DROP_SHADOW` or `INNER_SHADOW` |
| Border | `strokes[]` + `strokeWeight` |

### Step 3 — effects to CSS

**Drop shadow:**

```
effects[i].type = DROP_SHADOW
→ box-shadow: Xpx Ypx Rpx Spx rgb(r g b / a);
```

Fields: `offset.x`, `offset.y`, `radius`, `spread`, `color`.

**Inner shadow:**

```
effects[i].type = INNER_SHADOW
→ box-shadow: inset Xpx Ypx Rpx Spx rgb(r g b / a);
```

**Blur:**

```
effects[i].type = LAYER_BLUR
→ filter: blur(Rpx);

effects[i].type = BACKGROUND_BLUR
→ backdrop-filter: blur(Rpx);
```

### Step 4 — verify layout mode

- `layoutMode = NONE` → use `position: relative` on parent, position children with coordinates from `absoluteBoundingBox` diff
- `layoutMode = HORIZONTAL` or `VERTICAL` → use flex, map all spacing/padding fields exactly
- If children use `layoutPositioning = ABSOLUTE` inside an auto-layout → those children get `position: absolute`

### Step 5 — letter spacing conversion

Figma letter spacing is in `px`. Convert to `em`:

```
letter-spacing: (value / fontSize)em
```

### Step 6 — line height

Figma `lineHeightPx` → convert to unitless ratio for CSS `line-height`:

```
line-height: lineHeightPx / fontSize
```

Or use `rem` if the design system prefers fixed sizes.

### Step 7 — check text truncation

If Figma shows text clipped:

- `textAutoResize = NONE` with a fixed box → add `overflow: hidden`
- Single line → `white-space: nowrap; overflow: hidden; text-overflow: ellipsis`

### Step 8 — gradients

For `fills[0].type = GRADIENT_LINEAR`:

```
background: linear-gradient(angleDeg, color-stop-1 pos%, color-stop-2 pos%);
```

Read `gradientHandlePositions` to compute angle and `gradientStops` for color/position.

### Step 9 — do not invent anything

If a Figma value is absent from the payload, ask the user or fetch a deeper node — do not guess.

---

## CSS rules

Write pure CSS. No utility framework classes.

- Every color value must come from Figma MCP — no invented colors.
- Every font family, font size, font weight must come from Figma MCP.
- Every spacing, padding, gap value must match Figma.
- Do not use inline styles.
- Prefer `display: flex` and `display: grid` for layout.
- Do not use `position: absolute` for overall layout structure.
- Use semantic HTML elements (`header`, `nav`, `main`, `section`, `article`, `footer`).
- Define reusable values as CSS custom properties at `:root`:

```css
:root {
  --color-primary: rgb(255, 87, 51);
  --color-text: rgb(30, 30, 30);
  --font-heading: 'Inter', sans-serif;
  --radius-card: 12px;
  --spacing-section: 4rem;
}
```

- Reference those variables in component styles instead of repeating raw values.
- Do not hardcode user-facing copy in HTML; use the project i18n system if available.
