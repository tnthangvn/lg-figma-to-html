# Figma Mobile — design_history_sp
Node: `3096-5857` | File: `7VtVH7aNgLLIXrAwMKsjVX`

---

## Page
| Property | Value |
|---|---|
| Width | 375px |
| Background | `#000000` |
| Layout | column |

---

## Header (position: absolute, top: 0)
| Property | Value |
|---|---|
| Height | 72px |

### Logo — node `3096:5935`
| Width | Height | Position |
|---|---|---|
| 73px | 63px | top-left |

### Menu icon — node `3096:6433`
| Width | Height | Position |
|---|---|---|
| 83px | 72px | left: 292px, top: 0 |

---

## Year Overlay (position: absolute)
| Property | Value |
|---|---|
| x | 14px |
| y | 88px |
| Layout | row, align-items: center, gap: 6px |

| Text | Font | Weight | Size | Color | Letter-spacing |
|---|---|---|---|---|---|
| `1982` | MMC | 400 | 19.25px | `#FF9D00` | 8% |

### Bar
| Width | Height | Color |
|---|---|---|
| 18px | 1px | `#FF9D00` |

---

## Hero (Frame 2581 SP)
| Property | Value |
|---|---|
| Width | 375px (fill) |
| Height | 296px |
| Border-radius | 298px |
| Opacity | **0.6** |
| Vignette (::after) | `inset 0 0 33px 22px rgba(0,0,0,1)` |
| Image | `hero-car-65b00d.png` |
| object-fit | cover |

---

## Content Wrapper — Frame 2609 (node `3327:10553`)
| Property | Value |
|---|---|
| Width | 375px |
| Layout | column, align-items: stretch, gap: 24px |
| Padding | 0 24px |
| position-y | 296px (starts below hero) |

---

## Gen Title Block
| Text | Font | Weight | Size | Color | Letter-spacing |
|---|---|---|---|---|---|
| `1982.5 発売` | Noto Sans JP | 700 | 18px | `#FF9D00` | 8% |
| `初代パジェロ` | Noto Sans JP | 500 | 24px | `#FF9D00` | 10% |

---

## Text Sections (same as desktop, inside padding)
| Role | Font | Weight | Size | Color | Line-height |
|---|---|---|---|---|---|
| Section heading | Noto Sans JP | 500 | 22px | `#DADADA` | 1.5 |
| Body text | Noto Sans JP | 400 | 13px | `#DADADA` | 1.8 |
| Sub heading | Noto Sans JP | 500 | 18px | `#DADADA` | 1.5 |

---

## Spec Card — Frame 2607 (node `3392:4710`)
| Property | Value |
|---|---|
| Layout | column, align-items: center, gap: **32px** |
| Padding | **36px 0 41px** |
| Background | `rgba(255,255,255,0.06)` |

| Text | Font | Weight | Size | Color | Letter-spacing |
|---|---|---|---|---|---|
| `L040 SPEC` | MMC | 500 | 21px | `#FF9D00` | 8% |

### Spec Grid (mobile)
| Property | Value |
|---|---|
| Layout | column, align-items: center, gap: **14px** |
| Container width | 290px |

### Spec Row (mobile)
| Column | Width | Font | Size |
|---|---|---|---|
| Label | 110px | Noto Sans JP 400 | 11px |
| Value | 170px | MMC 400 | 11px |

### Spec Divider (mobile)
| Max-width | Height |
|---|---|
| 290px | 1px |

---

## Timeline Nav — Frame 2596 (mobile)
| Property | Value |
|---|---|
| Layout | row, justify-content: center, align-items: center, align-self: stretch, gap: 24px |

*(Same PREV/NEXT content as desktop, gap between items: 24px instead of 68px)*

---

## Pill Buttons — Frame 2604 (mobile, node `3338:11346`)
| Property | Value |
|---|---|
| Layout | **column**, align-items: **stretch**, align-self: stretch, gap: 24px |

| Property | Value |
|---|---|
| Width | fill (full container width) |
| Height | 48px |
| Border-radius | 50px |
| Border | 0.8px solid `#FF9D00` |
| Background | transparent (`rgba(0,0,0,0)`) |
| Text | Noto Sans JP 600 **14px** `#FF9D00` letter-spacing 16% |

---

## Follow Section — Frame 178 (node `3457:5403`)
| Property | Value |
|---|---|
| Width | 335px |
| Layout | column, align-items: center, gap: 32px |
| Padding | 0 0 40px |

### Follow Copy — Frame 124
| Width | Layout |
|---|---|
| 242px | column, gap: 8px |

| Text | Font | Weight | Size | Color | Letter-spacing | Align |
|---|---|---|---|---|---|---|
| `FOLLOW` | MMC | 500 | **20px** | `#FFFFFF` | 8% | center |
| subtitle | Noto Sans JP | 600 | **13px** | `#FFFFFF` | **5%** | **center** |
| subtitle line-height | 2.8em | | | | | |

### Social Icons — Frame 219 (IMAGE-SVG, node `3457:5407`)
| Property | Value |
|---|---|
| Layout | row, align-items: center, gap: **40px** |
| Icon size | **36×36px** each |
| Asset | `social-icons-mobile.png` (264×36 display) |

---

## Footer — footer_en_SP (node `3338:11384`)
| Property | Value |
|---|---|
| Width | 375px (fill) |
| Layout | column, align-items: stretch |

### Back to Top — component `pc` (instance `3338:11385`)
| Property | Value |
|---|---|
| Width | fill (375px) |
| Height | 60px |
| Background | `#D3D3D3` |
| Box-shadow | `0 0 4px #ED0000` |

| Text | Font | Weight | Size | Color | Letter-spacing |
|---|---|---|---|---|---|
| **`Back to top`** | **MMC** | **700** | 16px | `#000000` | 5% |

| Arrow icon | Size | Stroke |
|---|---|---|
| Up chevron | 25×25px | `#000000` 2px |

---

### Copyright — Frame 208 (node `3338:11386`)
| Property | Value |
|---|---|
| Width | fill (375px) |
| Height | 162px |
| Background | `#000000` |

### Copyright Inner — Frame 212
| Property | Value |
|---|---|
| Position | x: 20px, y: 50px |
| Width | 335px |
| Layout | column, gap: 30px |

### Policy Row — Frame 197
| Property | Value |
|---|---|
| Layout | row, justify-content: center, align-items: center, align-self: stretch, gap: 40px |

| Text | Font | Weight | Size | Color | Letter-spacing |
|---|---|---|---|---|---|
| `Privacy Policy` | MMC | 500 | 13px | `#FFFFFF` | 5% |
| `Cookie Policy` | MMC | 500 | 13px | `#FFFFFF` | 5% |

### Copyright Text
| Property | Value |
|---|---|
| Text | `© MITSUBISHI MOTORS CORPORATION.\n All rights reserved.` |
| Font | MMC |
| Weight | 500 |
| Size | 13px |
| Color | `#FFFFFF` |
| Letter-spacing | 5% |
| Line-height | 1.4em |
| Align | center |

---

## Structure Diagram (mobile)
```
page (375px)
├── header (absolute, height: 72px)
│   ├── logo (73×63, top-left)
│   └── menu (83×72, left:292)
├── year-overlay (absolute, x:14, y:88)
│   ├── "1982" (MMC 19.25px orange)
│   └── bar (18×1px orange)
├── hero (375×296, border-radius:298px, opacity:0.6)
└── content-wrapper (375px, padding:0 24px, gap:24px)
    ├── gen-header
    │   ├── gen-title-block (year label + gen name)
    │   └── text-sections (gap:100px)
    │       ├── main-text-block (gap:32px)
    │       └── sub-sections (gap:24px)
    └── spec-outer
        ├── spec-card (gap:32px, padding:36px 0 41px)
        └── bottom-section (375px, margin-left:-24px, gap:60px)
            ├── timeline-nav (centered row, gap:24px)
            └── gallery-section (gap:120px)
                ├── btn-row (column, stretch, gap:24px, padding:0 24px)
                │   ├── pill-btn (fill × 48px)
                │   └── pill-btn (fill × 48px)
                └── footer-block
                    ├── follow-section (335px, padding:0 0 40px, gap:32px)
                    │   ├── follow-copy (FOLLOW + subtitle)
                    │   └── social-icons (264×36px)
                    └── footer_en_SP (375px)
                        ├── back-to-top ("Back to top", gray, 60px)
                        └── copyright (black, 162px)
                            ├── Privacy Policy | Cookie Policy
                            └── © MITSUBISHI MOTORS CORPORATION.
```

> **Note**: Mobile has **NO footer car image**. Page ends with copyright section.

---

## Key Differences: Desktop vs Mobile

| Property | Desktop | Mobile |
|---|---|---|
| Page width | 1366px | 375px |
| Content width | 958px | 375px (pad: 0 24px) |
| Header height | 100px | 72px |
| Logo size | 115×100px | 73×63px |
| Menu size | 115×100px | 83×72px |
| Year position | top:291px, left:71px | x:14, y:88 |
| Year font size | 48px | 19.25px |
| Hero height | 647px | 296px |
| Hero border-radius | 1100px | 298px |
| Hero opacity | 1 | **0.6** |
| Content margin-top | -153px | 0 |
| Spec card gap | 42px | **32px** |
| Spec card padding | 40px 0 50px | **36px 0 41px** |
| Spec grid gap | 19px | **14px** |
| Spec label width | 240px | 110px |
| Spec value width | 300px | 170px |
| Spec divider width | 780px | 290px |
| Timeline gap | 68px | 24px |
| Buttons layout | row, gap:50px | column, stretch, gap:24px |
| Button width | 228px | fill |
| Button text size | 12px | **14px** |
| FOLLOW title | 24px | **20px** |
| FOLLOW subtitle | 15px, 8%, **left** | 13px, 5%, **center** |
| Social icon size | 42×42px | **36×36px** |
| Social icon gap | 48px | **40px** |
| Back-to-top text | `ページ上部へ戻る` (Noto Sans JP 600) | **`Back to top`** (MMC 700) |
| Footer car image | **YES** (645px) | **NO** |
| Copyright section | NO | **YES** (162px) |
