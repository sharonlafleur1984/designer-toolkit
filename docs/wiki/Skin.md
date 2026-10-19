# Skin: how the toolkit looks

**Last updated:** October 12, 2026

**Direction:** Fireside. Autumn warmth, still water, room for the dark. The shell is always dark, and one rust accent is used rarely, so the prototype stays the brightest thing on screen.

The skin is a theme in [lantern-design-system](https://github.com/sharonlafleur1984/lantern-design-system), not a separate system. Visual ideas, with Sharon's notes on what she loves and what loses her, are on the [FigJam board](https://www.figma.com/board/62L8u38vabqutND1Cx8ZpD).

## The recipe

Linear, Vercel and Figma all land on the same few moves.

- **One gray scale, each step with a job.** Backgrounds, then borders, then text. Nothing picks a gray by eye.
- **One accent, used rarely.** Selected, focused and the one main action. Nothing decorative.
- **Chrome dimmer than the content.** Sidebars and toolbars sit a few notches below the prototype.
- **Fewer, softer borders.** Structure comes from spacing first.
- **Panels that get out of the way.** Everything around the prototype can collapse or hide.

## What the references did

| Reference | The move worth borrowing | Look at it |
|---|---|---|
| Linear, 2024 | Cut the theme from 98 hand-set variables to 3 inputs: base, accent and contrast. Pulled blue out of the chrome to look "more neutral and timeless." | [Writeup](https://linear.app/now/how-we-redesigned-the-linear-ui) · [before](https://webassets.linear.app/images/ornj730p/production/23839a6bacba4a7617728dada3d37a40dc3584aa-2352x1380.png?q=95&auto=format&dpr=2) · [after](https://webassets.linear.app/images/ornj730p/production/2ef6f0599f502940b18eae2c37a1fbd9ee09be25-2352x1380.png?q=95&auto=format&dpr=2) · [light and dark](https://webassets.linear.app/images/ornj730p/production/b7551ae44d0365c0ed87d7e5e23aeb0421233ba5-2352x1656.png?q=95&auto=format&dpr=2) |
| Linear, March 2026 | Sidebar a few notches dimmer, smaller icons, softer separators. "Structure should be felt not seen." | [Writeup](https://linear.app/now/behind-the-latest-design-refresh) |
| Vercel Geist | Gray 100 to 1000 with fixed roles: 100 to 300 backgrounds, 400 to 600 borders, 900 and 1000 text. | [Geist colors](https://vercel.com/geist/colors) |
| Figma UI3 | The work takes center stage, panels collapse, and the whole UI can hide. Input backgrounds came back for clarity. | [Writeup](https://www.figma.com/blog/behind-our-redesign-ui3/) · [panels](https://cdn.sanity.io/images/599r6htc/regionalized/78f63a332bd5337dc3ef5fa6648a9e1044fb4497-1608x1072.png?w=528&h=352&q=75&fit=max&auto=format) |

## The Fireside palette

Sharon's six anchors, each a 100 to 900 ramp built on perceptual lightness, plus honey for warnings. The full ramps live in the design system's `designer-toolkit` theme.

| Color | Source | Mood | Job in the toolkit |
|---|---|---|---|
| Near-black | 900 #1A1612 | Nightfall, grounding depth | The frame. 900 is the base, 800 panels and cards, 700 raised and hover. |
| Cream | 100 #F8F0E8 | Moonlight, luminous canvas | Main text. Lighter steps for quieter text. |
| Peach | 200 #E9CEB5 | Evening light, soft warmth | Supporting text and information |
| Rust | 500 #AA6140 | Autumn earth, signature accent | The one accent: selected, focus and the main button. Buttons use bright rust #D06C3E. |
| Fire red | 600 #BF2B07 | Crackling ember, focused energy | Danger, as solid fills or dark tints |
| Lake green | 700 #304341 | Still water, quiet contrast | Success, and calm surfaces |
| Honey | #E1C167 | Golden hour, gentle caution | Warnings only |

### Rules that keep it calm

- **Rust is rare.** One main button, the focus ring, the selected item. Used everywhere, rust on black reads as Halloween.
- **Every status color has an icon or label.** Rust and fire red are the closest pair, and they need the icon to stay apart.
- **Fire red is never text on the frame.** Its middle shades sit too close to bright rust.
- **The strip around the prototype stays near-black,** so a prototype's own colors look true.

Picked over a cool blue or violet accent and a gold accent. Bright rust outranks the honey warning, and it stays distinct from fire red for people with red-green color blindness, checked by simulating protanopia and deuteranopia.

## Dark mode

The shell is always dark. Reading surfaces, like the Documentation tab, can switch to light.

- **Not an inverted light theme** ([Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/dark-mode)).
- **Warm dark gray, not black.** The base is #1A1612. Material suggests a dark gray like #121212 ([Material](https://m2.material.io/design/color/dark-theme.html)).
- **Raised panels get lighter, not shadowed** (same source).
- **Long reading gets softer text,** a cream instead of pure white, and a light option for the wiki.

## How quiet is too quiet

The contrast floor, from WCAG 2.2 AA (Web Content Accessibility Guidelines, level AA). It holds on every surface.

- **Text:** 4.5:1, or 3:1 for large text ([W3C 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html)).
- **Anything that shows a control or its state** needs 3:1. That covers input borders, focus rings and icons that carry meaning ([W3C 1.4.11](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html)).
- **Dividers that are only decoration** can be fainter.
- **Thin lines look fainter than their color** because of anti-aliasing, so test borders on screen, not only by the numbers (same source).

## In Storybook

Storybook's theme options cover most of the skin: `appBg`, `appContentBg`, `appPreviewBg`, `appBorderColor`, `barBg`, and `colorSecondary` as the one accent ([Storybook theming](https://storybook.js.org/docs/configure/user-interface/theming)). The toolbar and panels can hide, which keeps the prototype in front ([Storybook](https://storybook.js.org/docs/configure/user-interface/features-and-behavior)).

## Still open

- **Type.** The typeface isn't chosen. The theme uses After Graduation's type for now.
- **The glass and light recipe.** "Natural" can only be judged on screen, so three versions get built in Storybook for Sharon to react to.

Full research: [Research](Research#quiet-chrome-uses-one-gray-scale-and-one-accent).
