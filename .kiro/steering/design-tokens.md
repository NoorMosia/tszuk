# Design Tokens

All visual values live as CSS custom properties in `src/styles/global.css`. Components must reference these tokens — never hardcode raw values.

## Colors

| Token | Value | Usage |
|-------|-------|-------|
| `--color-sage` | `#E6F2DD` | Cover background |
| `--color-white` | `#FFFFFF` | Page background, Hero background |
| `--color-accent` | `#88BDA4` | Focus borders, blob shape, interactive highlights |
| `--color-text` | `#181818` | Primary body text, active highlight color |
| `--color-dark` | `#1A231E` | Footer background |
| `--color-sage-tint` | `#F4F9F1` | Capabilities column hover background |
| `--color-divider` | `#EAEAEA` | Column dividers, subtle borders |
| `--color-muted` | `#777777` | Inactive highlight text |

## Typography

| Token | Value | Usage |
|-------|-------|-------|
| `--font-family` | `'Inter', sans-serif` | All text |
| `--font-weight-light` | `300` | Subtitles, taglines |
| `--font-weight-regular` | `400` | Body text |
| `--font-weight-bold` | `700` | Headings, logotype |
| `--line-height-body` | `1.6` | Body paragraphs |
| `--letter-spacing-subtitle` | `0.15em` | Tagline, subtitles |

## Spacing

| Token | Value | Usage |
|-------|-------|-------|
| `--section-padding` | `120px` | Vertical section padding (desktop) |
| `--section-padding-mobile` | `64px` | Vertical section padding (mobile) |
| `--content-max-width` | `1200px` | Outer content container |
| `--manifesto-max-width` | `650px` | Hero text block width |

## Motion

| Token | Value | Usage |
|-------|-------|-------|
| `--easing` | `cubic-bezier(0.25, 1, 0.5, 1)` | All transitions |
| `--duration-reveal` | `600ms` | Scroll-reveal fade+slide |
| `--duration-highlight` | `400ms` | Text highlight color transition |
| `--duration-hover` | `300ms` | Hover scale/background transitions |
| `--duration-flip` | `0ms` | Scroll-driven (no fixed duration) |
| `--blob-duration` | `15s` | Blob border-radius morph cycle |

## Sizes

| Token | Value | Usage |
|-------|-------|-------|
| `--cover-flip-threshold` | `300px` | Scroll distance for full flip |
| `--parallax-factor` | `0.05` | Parallax scroll multiplier |
| `--hover-scale` | `1.03` | Card image hover zoom |

## Reduced Motion Override

When `prefers-reduced-motion: reduce` is active, all duration tokens are set to `0ms`. This is handled in `global.css` — components do not need to add their own media query for durations as long as they use the tokens.
