# Skin: how the toolkit looks

**Last updated:** October 13, 2026

**Direction:** quiet and dark, in the Retro palette. Deep blue-green chrome, one gold accent, thin borders and lots of space, so the prototype stands out. Light and dark mode both. Chosen Oct 13, 2026 ([Decisions](Decisions)).

The skin is a theme in [design-system-skeleton](https://github.com/sharonlafleur1984/design-system-skeleton), not a separate system. Visual ideas collect on the [FigJam board](https://www.figma.com/board/62L8u38vabqutND1Cx8ZpD).

## The recipe

Linear, Vercel and Figma all land on the same few moves.

- **One gray scale, each step with a job.** Backgrounds, then borders, then text. Nothing picks a gray by eye.
- **One accent, used rarely.** Selected, focused and the one main action. Nothing decorative.
- **Chrome dimmer than the content.** Sidebars and toolbars sit a few notches below the prototype.
- **Fewer, softer borders.** Structure comes from spacing first.
- **Panels that get out of the way.** Everything around the prototype can collapse or hide.

## The Retro palette

Every color comes from one family, so changing one means checking the rest. Values are from the [shell preview](https://github.com/sharonlafleur1984/designer-toolkit-code/tree/main/shell-preview), in dark mode.

| Job | Color | Hex |
|---|---|---|
| Shell background | Near-black from Smalt Blue | `#051013` |
| Behind the prototype | Lighter blue-green | `#1a2c31` |
| Main text | Cream | `#f6f2e1` |
| Secondary text | Hampton | `#e2d8a5` |
| Accent: selected, focus, the main action | Harvest Gold | `#e1a36f` |
| Warning pill | Calico, dark tint | `#f0e0ba` on `#473c1e` |
| Success pill | Sea Nymph, dark tint | `#cbe4e2` on `#1b3f3d` |
| Info pill | Smalt Blue, dark tint | `#cee2e8` on `#173e48` |
| Danger | Brick red | `#bb635a` |

Contrast on the shell background, checked against [WCAG 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html): Hampton 13.4:1, Harvest Gold 8.9:1, brick red 4.6:1. The warning pill's text is 8.3:1 on its tint.

## What the references did

| Reference | The move worth borrowing | Look at it |
|---|---|---|
| Linear, 2024 | Cut the theme from 98 hand-set variables to 3 inputs: base, accent and contrast. Pulled blue out of the chrome to look "more neutral and timeless." | [Writeup](https://linear.app/now/how-we-redesigned-the-linear-ui) · [before](https://webassets.linear.app/images/ornj730p/production/23839a6bacba4a7617728dada3d37a40dc3584aa-2352x1380.png?q=95&auto=format&dpr=2) · [after](https://webassets.linear.app/images/ornj730p/production/2ef6f0599f502940b18eae2c37a1fbd9ee09be25-2352x1380.png?q=95&auto=format&dpr=2) · [light and dark](https://webassets.linear.app/images/ornj730p/production/b7551ae44d0365c0ed87d7e5e23aeb0421233ba5-2352x1656.png?q=95&auto=format&dpr=2) |
| Linear, March 2026 | Sidebar a few notches dimmer, smaller icons, softer separators. "Structure should be felt not seen." | [Writeup](https://linear.app/now/behind-the-latest-design-refresh) |
| Vercel Geist | Gray 100 to 1000 with fixed roles: 100 to 300 backgrounds, 400 to 600 borders, 900 and 1000 text. | [Geist colors](https://vercel.com/geist/colors) |
| Figma UI3 | The work takes center stage, panels collapse, and the whole UI can hide. Input backgrounds came back for clarity. | [Writeup](https://www.figma.com/blog/behind-our-redesign-ui3/) · [panels](https://cdn.sanity.io/images/599r6htc/regionalized/78f63a332bd5337dc3ef5fa6648a9e1044fb4497-1608x1072.png?w=528&h=352&q=75&fit=max&auto=format) |

## Which grays to use

The Retro surfaces above replace this pick. It stays here for the reasoning behind giving each step one job.

**Recommended: Radix Colors `gray`.** It's a pure gray with almost no tint, so it won't clash with a prototype's own colors. It ships light, dark and transparent versions ([Radix](https://www.radix-ui.com/colors/docs/palette-composition/composing-a-palette)).

Its 12 steps each have a role ([Radix scale](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale)):

| Step | Job in the toolkit |
|---|---|
| 1 to 2 | Page and panel backgrounds |
| 3 to 5 | Hover, pressed and selected backgrounds |
| 6 | Quiet dividers |
| 7 | Input and control borders |
| 8 | Focus rings and strong borders |
| 11 | Secondary text |
| 12 | Main text |

Alternatives: [Geist gray](https://vercel.com/geist/colors) and [shadcn/ui Neutral](https://ui.shadcn.com/docs/theming).

## Dark mode

- **Not an inverted light theme** ([Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/dark-mode)).
- **Dark gray, not black.** Material suggests #121212 for the base ([Material](https://m2.material.io/design/color/dark-theme.html)).
- **Raised panels get lighter, not shadowed** (same source).
- **The accent gets its own dark value,** checked again for contrast.

## How quiet is too quiet

The contrast floor, from WCAG 2.2 AA (Web Content Accessibility Guidelines, level AA). It holds in light and dark, on every surface.

- **Text:** 4.5:1, or 3:1 for large text ([W3C 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html)).
- **Anything that shows a control or its state** needs 3:1. That covers input borders, focus rings and icons that carry meaning ([W3C 1.4.11](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html)).
- **Dividers that are only decoration** can be fainter. Step 6 is fine for those.
- **Thin lines look fainter than their color** because of anti-aliasing, so test borders on screen, not only by the numbers (same source).

## In Storybook

Storybook's theme options cover most of the skin: `appBg`, `appContentBg`, `appPreviewBg`, `appBorderColor`, `barBg`, and `colorSecondary` as the one accent ([Storybook theming](https://storybook.js.org/docs/configure/user-interface/theming)). The toolbar and panels can hide, which keeps the prototype in front ([Storybook](https://storybook.js.org/docs/configure/user-interface/features-and-behavior)).

## Still open

- **Type.** The typeface is still open. Tracked in [Spec, Open decisions](Spec#open-decisions).
- **Full color ranges.** Retro needs 100 to 900 steps for every color before it goes into the design system.
- **Light mode values.** The preview has a light mode, but its colors haven't been checked for contrast yet.

Full research: [Research](Research#quiet-chrome-uses-one-gray-scale-and-one-accent).
