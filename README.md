# astro-tocbutton

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
![GitHub all releases](https://img.shields.io/github/downloads/rgglez/astro-tocbutton/total)
![GitHub issues](https://img.shields.io/github/issues/rgglez/astro-tocbutton)
![GitHub commit activity](https://img.shields.io/github/commit-activity/y/rgglez/astro-tocbutton)
[![GitHub release](https://img.shields.io/github/release/rgglez/astro-tocbutton.svg)](https://github.com/rgglez/astro-tocbutton/releases/)
![GitHub stars](https://img.shields.io/github/stars/rgglez/astro-tocbutton?style=social)
![GitHub forks](https://img.shields.io/github/forks/rgglez/astro-tocbutton?style=social)

**astro-tocbutton** generates a floating table-of-contents button for Astro blog posts. Reads `h2`–`h6` headings from a `#article` element and renders a popover with navigation links. Positioned bottom-left by default (so it does not conflict with a bottom-right back-to-top button), and configurable to any corner. RTL-aware: placement mirrors automatically under `dir="rtl"`.

## Installation

```bash
npm install @rgglez/astro-tocbutton
```

## Usage

```astro
import TocButton from "@rgglez/astro-tocbutton";

<TocButton />
```

### Optional props

| Prop       | Type                                                         | Default          | Description                                                                 |
|------------|-------------------------------------------------------------|------------------|-----------------------------------------------------------------------------|
| `label`    | `string`                                                    | `"Table of contents"` | `aria-label` for the toggle button                                     |
| `position` | `"bottom-left" \| "bottom-right" \| "top-left" \| "top-right"` | `"bottom-left"`  | Fixed corner for the button. Uses logical edges, so it mirrors under RTL.   |

```astro
<TocButton position="top-right" label="On this page" />
```

Under `dir="rtl"`, `*-left` placements resolve to the right edge and `*-right` to the left (the inline-start/inline-end edges flip automatically).

## Requirements

- **Astro ≥ 5.7** — the icon is imported as a native SVG component (`import Icon from "./icon.svg"`), supported from Astro 5.7 onward.
- The article content must be wrapped in an element with `id="article"`. Headings (`h2`–`h6`) inside it must have `id` attributes (Astro / remark sets these automatically for markdown/MDX).
- [Tailwind CSS](https://tailwindcss.com/) **≥ 3.3** must be configured in your project (logical `start-*`/`end-*` utilities, used for RTL-aware positioning, were added in 3.3). If using Tailwind v4, add the package source to your content scan so utility classes are not purged:

```css
/* global.css (v4) */
@source "../node_modules/@rgglez/astro-tocbutton/src";
```

## Behavior

- Button is always visible on pages that contain headings; hidden if `#article` has none.
- Clicking the button opens/closes a popover anchored to it (above the button for `bottom-*` positions, below it for `top-*`).
- Headings are indented by level: `h2` = no indent, `h3` = `pl-4`, `h4` = `pl-8`, `h5` = `pl-10`, `h6` = `pl-12`.
- Clicking a heading link closes the popover and scrolls to the section.
- Also closes on **Escape** or click outside.
- Compatible with Astro View Transitions (`data-astro-rerun` guard prevents duplicate listeners).

## Development

| Target        | Description                                               |
|---------------|-----------------------------------------------------------|
| `make tags`   | List git tags sorted by semver (descending)               |
| `make patch`  | Bump PATCH version in `package.json`, commit, tag, push   |
| `make publish`| Publish current version to npm                            |

Typical release flow: `make patch` → `make publish`.

## License

Copyright (C) 2026 Rodolfo González González.

Licensed under the [Apache v2.0](https://www.apache.org/licenses/LICENSE-2.0.txt) license. Read the [LICENSE](LICENSE) file.
