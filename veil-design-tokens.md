# Veil — Design Token Reference

Pulled from Figma file `l5vi6Y6EiwmUhpND7UKFV0` ("Veil — Design System").

Architecture: two collections. **Primitives** holds raw values and has four modes (Desert Warmth, Playful Pop, Ivory Veil, Neutral). **Semantic** is single-mode and only contains aliases into Primitives. Theme switching happens by changing the Primitives mode, never the Semantic one. In code this means: one set of semantic CSS variables, and a theme class that reswizzles the primitives underneath.

---

## 1. Semantic → Primitive mapping

These names are what the UI references. They never change per theme.

| Semantic | Primitive it aliases |
|---|---|
| `color/surface-page` | `color/sand-50` |
| `color/surface-card` | `color/cream-50` |
| `color/ink-primary` | `color/espresso-900` |
| `color/ink-secondary` | `color/taupe-500` |
| `color/ink-on-accent` | `color/button-text-base` |
| `color/accent` | `color/terracotta-500` |
| `color/accent-quiet` | `color/sand-200` |
| `color/surface-disabled` | `color/neutral-disabled` |
| `color/border-subtle` | `color/border-hairline` |
| `color/visibility-everyone` | `color/sage-500` |
| `color/visibility-teased` | `color/amber-400` |
| `color/visibility-hidden` | `color/clay-600` |
| `radius/radius-chip` | `radius/radius-sm` |
| `radius/radius-card` | `radius/radius-md` |
| `radius/radius-sheet` | `radius/radius-lg` |
| `spacing/space-1` … `space-7` | `spacing/space-1` … `space-7` (1:1) |
| `font/font-display` | `font/font-family-cormorant` |
| `font/font-body` | `font/font-family-dmsans` |

Note: the primitive names are historical (`terracotta-500`, `cormorant`) and carry Desert Warmth's vocabulary, but the values swap per mode. Always reference the semantic name in components.

---

## 2. Primitive color values by mode

| Primitive | Desert Warmth | Playful Pop | Ivory Veil | Neutral |
|---|---|---|---|---|
| `color/sand-50` | `#f5ede2` | `#fdf3f8` | `#fbf9f5` | `#f7f6f4` |
| `color/cream-50` | `#fffbf5` | `#ffffff` | `#ffffff` | `#ffffff` |
| `color/espresso-900` | `#2e2822` | `#2b2733` | `#3a3630` | `#1f1d1b` |
| `color/taupe-500` | `#7a6f63` | `#8a7f93` | `#756b60` | `#6b6660` |
| `color/terracotta-500` | `#c4714b` | `#f5617a` | `#c7a96b` | `#2e2a26` |
| `color/sand-200` | `#e8d5c4` | `#f7d9e4` | `#efe7d6` | `#cccccc` |
| `color/sage-500` | `#7b9370` | `#8bb89a` | `#8fa394` | `#8fa394` |
| `color/amber-400` | `#d9a566` | `#e0a5c6` | `#c9a9a0` | `#c9a9a0` |
| `color/clay-600` | `#8c3a3f` | `#c24a6e` | `#8a5a6b` | `#8a5a6b` |
| `color/off-white` | `#fffefb` | `#fffefb` | `#fffefb` | `#fffefb` |
| `color/button-text-base` | `#fffefb` | `#fffefb` | `#3a3630` | `#ffffff` |
| `color/neutral-disabled` | `#e7e1d8` | `#ece7ef` | `#ede9e2` | `#ede9e2` |
| `color/border-hairline` | `#ebdfcf` | `#f0e2ec` | `#efe9e0` | `#efe9e0` |

`color/off-white` is unaliased and identical in every mode. Treat it as a constant.

---

## 3. Radius by mode

| Primitive | Semantic | Desert Warmth | Playful Pop | Ivory Veil | Neutral |
|---|---|---|---|---|---|
| `radius-sm` | `radius-chip` | 8 | 12 | 9 | 9 |
| `radius-md` | `radius-card` | 12 | 16 | 14 | 14 |
| `radius-lg` | `radius-sheet` | 20 | 24 | 22 | 22 |

---

## 4. Spacing

Identical across all four modes. Never themed.

| Token | Value |
|---|---|
| `space-1` | 4 |
| `space-2` | 8 |
| `space-3` | 12 |
| `space-4` | 16 |
| `space-5` | 24 |
| `space-6` | 32 |
| `space-7` | 48 |

---

## 5. Type styles

Sizes and line heights are identical across the three real themes, so layouts never reflow on a theme swap. Only the family and weight change. Neutral is the exception: its display is 40/44 instead of 44/48.

### Desert Warmth
| Style | Family | Weight | Size / Line height | Letter spacing | Case |
|---|---|---|---|---|---|
| display | Cormorant Garamond | SemiBold (600) | 44 / 48 | -0.5% | as typed |
| title | Cormorant Garamond | SemiBold (600) | 22 / 28 | 0 | as typed |
| body | DM Sans | Regular (400) | 16 / 24 | 0 | as typed |
| caption | DM Sans | Regular (400) | 13 / 18 | 0.1% | as typed |
| label | DM Sans | SemiBold (600) | 12 / 16 | 0.6% | UPPERCASE |

### Playful Pop
| Style | Family | Weight | Size / Line height | Letter spacing | Case |
|---|---|---|---|---|---|
| display | Fredoka | Regular (400) | 44 / 48 | -0.5% | as typed |
| title | Fredoka | Regular (400) | 22 / 28 | 0 | as typed |
| body | Poppins | Regular (400) | 16 / 24 | 0 | as typed |
| caption | Poppins | Regular (400) | 13 / 18 | 0.1% | as typed |
| label | Poppins | SemiBold (600) | 12 / 16 | 0.6% | UPPERCASE |

### Ivory Veil
| Style | Family | Weight | Size / Line height | Letter spacing | Case |
|---|---|---|---|---|---|
| display | EB Garamond | Regular (400) | 44 / 48 | -0.5% | as typed |
| title | EB Garamond | SemiBold (600) | 22 / 28 | 0 | as typed |
| body | Jost | Regular (400) | 16 / 24 | 0 | as typed |
| caption | Jost | Regular (400) | 13 / 18 | 0.1% | as typed |
| label | Jost | SemiBold (600) | 12 / 16 | 0.6% | UPPERCASE |

### Neutral (pre-theme onboarding)
| Style | Family | Weight | Size / Line height | Letter spacing | Case |
|---|---|---|---|---|---|
| display | Inter | Semi Bold (600) | 40 / 44 | 0 | as typed |
| title | Inter | Semi Bold (600) | 22 / 28 | 0 | as typed |
| body | Inter | Regular (400) | 16 / 24 | 0 | as typed |
| caption | Inter | Regular (400) | 13 / 18 | 0 | as typed |
| label | Inter | Semi Bold (600) | 12 / 16 | 0.6% | UPPERCASE |

Letter spacing is expressed in Figma as a percentage of font size. In CSS use `em`: -0.5% becomes `-0.005em`, 0.1% becomes `0.001em`, 0.6% becomes `0.006em`.

Known issue: Cormorant Garamond uses oldstyle figures, so numerals sit at inconsistent heights. Decision was to keep the face and route all numerics (countdown, times, dollar amounts) through the body font instead.

---

## 6. Font loading

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@600&family=DM+Sans:wght@400;600&family=Fredoka:wght@400&family=Poppins:wght@400;600&family=EB+Garamond:wght@400;600&family=Jost:wght@400;600&family=Inter:wght@400;600&display=swap" rel="stylesheet">
```

---

## 7. CSS variable implementation

Semantic variables are declared once. Each theme class only overrides the primitive layer, matching the Figma architecture.

```css
:root {
  /* spacing — never themed */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 24px;
  --space-6: 32px;
  --space-7: 48px;

  /* constant */
  --color-off-white: #fffefb;

  /* type scale — sizes shared across the three real themes */
  --font-size-display: 44px;   --line-height-display: 48px;   --tracking-display: -0.005em;
  --font-size-title: 22px;     --line-height-title: 28px;     --tracking-title: 0;
  --font-size-body: 16px;      --line-height-body: 24px;      --tracking-body: 0;
  --font-size-caption: 13px;   --line-height-caption: 18px;   --tracking-caption: 0.001em;
  --font-size-label: 12px;     --line-height-label: 16px;     --tracking-label: 0.006em;

  /* semantic layer — aliases, identical in every theme */
  --surface-page: var(--sand-50);
  --surface-card: var(--cream-50);
  --surface-disabled: var(--neutral-disabled);
  --ink-primary: var(--espresso-900);
  --ink-secondary: var(--taupe-500);
  --ink-on-accent: var(--button-text-base);
  --accent: var(--terracotta-500);
  --accent-quiet: var(--sand-200);
  --border-subtle: var(--border-hairline);
  --visibility-everyone: var(--sage-500);
  --visibility-teased: var(--amber-400);
  --visibility-hidden: var(--clay-600);
  --radius-chip: var(--radius-sm);
  --radius-card: var(--radius-md);
  --radius-sheet: var(--radius-lg);
  --font-display: var(--font-family-display);
  --font-body: var(--font-family-body);
}

/* ---- Desert Warmth ---- */
.theme-desert-warmth {
  --sand-50: #f5ede2;
  --cream-50: #fffbf5;
  --espresso-900: #2e2822;
  --taupe-500: #7a6f63;
  --terracotta-500: #c4714b;
  --sand-200: #e8d5c4;
  --sage-500: #7b9370;
  --amber-400: #d9a566;
  --clay-600: #8c3a3f;
  --button-text-base: #fffefb;
  --neutral-disabled: #e7e1d8;
  --border-hairline: #ebdfcf;
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 20px;
  --font-family-display: 'Cormorant Garamond', serif;
  --font-family-body: 'DM Sans', sans-serif;
  --weight-display: 600;
  --weight-title: 600;
}

/* ---- Playful Pop ---- */
.theme-playful-pop {
  --sand-50: #fdf3f8;
  --cream-50: #ffffff;
  --espresso-900: #2b2733;
  --taupe-500: #8a7f93;
  --terracotta-500: #f5617a;
  --sand-200: #f7d9e4;
  --sage-500: #8bb89a;
  --amber-400: #e0a5c6;
  --clay-600: #c24a6e;
  --button-text-base: #fffefb;
  --neutral-disabled: #ece7ef;
  --border-hairline: #f0e2ec;
  --radius-sm: 12px;
  --radius-md: 16px;
  --radius-lg: 24px;
  --font-family-display: 'Fredoka', sans-serif;
  --font-family-body: 'Poppins', sans-serif;
  --weight-display: 400;
  --weight-title: 400;
}

/* ---- Ivory Veil ---- */
.theme-ivory-veil {
  --sand-50: #fbf9f5;
  --cream-50: #ffffff;
  --espresso-900: #3a3630;
  --taupe-500: #756b60;
  --terracotta-500: #c7a96b;
  --sand-200: #efe7d6;
  --sage-500: #8fa394;
  --amber-400: #c9a9a0;
  --clay-600: #8a5a6b;
  --button-text-base: #3a3630;
  --neutral-disabled: #ede9e2;
  --border-hairline: #efe9e0;
  --radius-sm: 9px;
  --radius-md: 14px;
  --radius-lg: 22px;
  --font-family-display: 'EB Garamond', serif;
  --font-family-body: 'Jost', sans-serif;
  --weight-display: 400;
  --weight-title: 600;
}

/* ---- Neutral (pre-theme onboarding only) ---- */
.theme-neutral {
  --sand-50: #f7f6f4;
  --cream-50: #ffffff;
  --espresso-900: #1f1d1b;
  --taupe-500: #6b6660;
  --terracotta-500: #2e2a26;
  --sand-200: #cccccc;
  --sage-500: #8fa394;
  --amber-400: #c9a9a0;
  --clay-600: #8a5a6b;
  --button-text-base: #ffffff;
  --neutral-disabled: #ede9e2;
  --border-hairline: #efe9e0;
  --radius-sm: 9px;
  --radius-md: 14px;
  --radius-lg: 22px;
  --font-family-display: 'Inter', sans-serif;
  --font-family-body: 'Inter', sans-serif;
  --weight-display: 600;
  --weight-title: 600;
  /* Neutral display runs smaller */
  --font-size-display: 40px;
  --line-height-display: 44px;
  --tracking-display: 0;
}
```

### Type style classes

```css
.type-display {
  font-family: var(--font-display);
  font-weight: var(--weight-display);
  font-size: var(--font-size-display);
  line-height: var(--line-height-display);
  letter-spacing: var(--tracking-display);
}
.type-title {
  font-family: var(--font-display);
  font-weight: var(--weight-title);
  font-size: var(--font-size-title);
  line-height: var(--line-height-title);
  letter-spacing: var(--tracking-title);
}
.type-body {
  font-family: var(--font-body);
  font-weight: 400;
  font-size: var(--font-size-body);
  line-height: var(--line-height-body);
  letter-spacing: var(--tracking-body);
}
.type-caption {
  font-family: var(--font-body);
  font-weight: 400;
  font-size: var(--font-size-caption);
  line-height: var(--line-height-caption);
  letter-spacing: var(--tracking-caption);
}
.type-label {
  font-family: var(--font-body);
  font-weight: 600;
  font-size: var(--font-size-label);
  line-height: var(--line-height-label);
  letter-spacing: var(--tracking-label);
  text-transform: uppercase;
}
/* numerals always ride the body face, per the Cormorant oldstyle-figure decision */
.num { font-family: var(--font-body); font-variant-numeric: lining-nums tabular-nums; }
```

