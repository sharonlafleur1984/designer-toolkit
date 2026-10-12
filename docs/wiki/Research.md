# Research: tools for the toolkit

**Last updated:** October 12, 2026

What the [Spec](Spec) and [Skin](Skin) are built on. Each section links to its sources.

## Summary

The best setup for this toolkit costs about $12 a month and mostly uses tools Sharon already has.

- **Figma frames:** html.to.design PRO ($12/month billed yearly) bulk-imports a list of Netlify state URLs, per theme, into editable auto layout frames ([html.to.design](https://html.to.design/docs/pro-plan)). Figma's own capture tool is free in beta, but it works one page at a time and produces raw layers ([Figma](https://developers.figma.com/docs/figma-mcp-server/code-to-canvas/)).
- **Skin:** Linear, Vercel Geist and Figma UI3 share one recipe. Each step of a neutral gray scale has a fixed job, there's one accent, and the chrome is dimmer than the content.
- **Checks:** Storybook's a11y (accessibility) addon can fail a build on any story. WCAG 2.2 AA (Web Content Accessibility Guidelines, level AA) is **off by default** and has to be switched on ([Storybook](https://storybook.js.org/docs/writing-tests/accessibility-testing)). Even switched on, automation catches only about 57% of issues ([Deque](https://www.deque.com/automated-accessibility-coverage-report/)), so the heuristic and WCAG checklist stays manual.
- **Versions:** the pattern everyone uses is a live draft plus frozen, named snapshots. Netlify already creates a frozen URL for every deploy. It deletes old deploys after 30 days, so the version list has to live somewhere durable, like the repo or a database ([Netlify](https://docs.netlify.com/deploy/manage-deploys/manage-deploys-overview)).

## html.to.design gives the best value for state frames

Make every prototype state reachable by its own URL, for example with query params or a `?theme=dark` param. Then any of these tools can capture it.

| Option | What you get in Figma | Batch | Light and dark | Cost |
|---|---|---|---|---|
| html.to.design | Editable frames, optional auto layout, auto-created styles. No variants. | Bulk URL list on PRO, plus an MCP (Model Context Protocol) server | Pick a theme per import | Free 10 imports a month; PRO $12/month yearly |
| Figma `generate_figma_design` | Editable frames, raw geometry. Variables bind if a library is attached. | One page per capture, so an agent has to loop | Capture each theme URL separately | Free in beta |
| Figma `use_figma` | Real components, variants, variables, auto layout | Agent-driven | Can be modeled as variables | Free in beta, paid later; Full seat |
| story.to.design | Native components with variants from story args | Many stories per import, one-click sync | Themes become a variant property | $149/month Team |
| Storybook Connect, Chromatic | Nothing. Links only. | n/a | n/a | Chromatic account |

Sources for the table: html.to.design [PRO](https://html.to.design/docs/pro-plan), [bulk import](https://html.to.design/docs/bulk-import-url-list) and [overview](https://html.to.design/docs/). Figma [code to canvas](https://developers.figma.com/docs/figma-mcp-server/code-to-canvas/), [write to canvas](http://developers.figma.com/docs/figma-mcp-server/write-to-canvas/) and [MCP guide](https://github.com/figma/mcp-server-guide/blob/main/README.md). story.to.design [pricing](https://story.to.design/docs/paid-plans) and [globals](https://story.to.design/docs/storybook-globals). [Chromatic Figma plugin](https://docs.chromatic.com/docs/figma-plugin).

### Why html.to.design wins

- **Bulk import:** a pasted list of URLs comes in all at once, but only on PRO ([html.to.design](https://html.to.design/docs/bulk-import-url-list)).
- **Themes and viewports:** you can import the same page with different theme and viewport combinations ([html.to.design](https://html.to.design/docs/)).
- **Scripting:** its MCP server works with Claude Code, so the import can be scripted ([html.to.design MCP](https://html.to.design/docs/mcp-tab)).
- **Private pages:** the browser extension captures behind a login. Saving a local `.h2d` file keeps data off their servers ([html.to.design](https://html.to.design/docs/import-private-page)).

### Where Figma's own tool fits

- **What it makes:** `generate_figma_design` turns live browser UI into standard Figma layers ([Figma](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)).
- **Rate limits:** it's exempt from the standard rate limits (same source).
- **Seats:** any seat can write to drafts. Editing a file outside drafts needs a Full seat ([Figma](https://developers.figma.com/docs/figma-mcp-server/code-to-canvas/)).
- **Known gap:** a February 2026 user report says its output has no component instances or variant properties ([Figma Forum](https://forum.figma.com/suggest-a-feature-11/figma-mcp-generate-figma-design-should-resolve-html-elements-to-existing-library-components-instead-of-raw-frames-51286)).

`use_figma` builds real components, but it can't handle images or custom fonts yet. It caps output at 20kb per call ([Figma](http://developers.figma.com/docs/figma-mcp-server/write-to-canvas/)).

### When story.to.design is worth $149

Only if the goal is a true Figma component library synced from Storybook.

It makes native components with variants and auto layout ([story.to.design](https://story.to.design/)). A private Storybook needs its local agent, which runs on `localhost:6006` ([story.to.design](https://story.to.design/docs/local-mode)). The output is components, not screen frames laid out as a flow.

**Watch out:** neither html.to.design nor story.to.design publishes its free import limit clearly. html.to.design's docs say both 10 and 12 a month ([PRO plan](https://html.to.design/docs/pro-plan), [overview](https://html.to.design/docs/)). Test one real prototype on the free tier before paying.

## Quiet chrome uses one gray scale and one accent

### What the references did

#### Linear, 2024 and March 2026

Linear cut its theme from 98 hand-set variables to 3: base color, accent and contrast ([Linear](https://linear.app/now/how-we-redesigned-the-linear-ui)). It limited how much blue went into the chrome to look "more neutral and timeless" (same source).

The 2026 refresh made the sidebar "a few notches dimmer," shrank tabs and icons, and softened separators. It followed the rule "Structure should be felt not seen" ([Linear 2026](https://linear.app/now/behind-the-latest-design-refresh)).

The refresh also moved from blue-gray to a warmer, less saturated gray. Linear warned that going too warm looks "muddy" (same source).

#### Vercel Geist

Every gray step has a fixed role ([Geist](https://vercel.com/geist/colors)). Steps 100 to 300 are for backgrounds, 400 to 600 for borders, 900 for secondary text and 1000 for primary text.

There are only two page backgrounds, and the second is used "sparingly." Use solid gray by default and alpha gray only for overlays (same source).

#### Figma UI3

The work takes "center stage," panels collapse, and the toolbar moved to the bottom ([Figma](https://www.figma.com/blog/behind-our-redesign-ui3/)). Figma tested a UI that only showed on hover and dropped it as too unstable. It added input backgrounds and dropdown borders back for clarity (same source).

#### Tools with no official writeup

Raycast, Arc, Framer, Zeroheight and Supernova have no official writeups on chrome color. Only third-party analyses exist, so they're left out here.

### Light and dark guidance

Dark mode is not an inversion ([Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/dark-mode)). Material recommends a #121212 surface instead of black. It shows elevation with lighter surfaces, not shadows ([Material](https://m2.material.io/design/color/dark-theme.html)).

Radix warns that tinted grays can clash with colorful content, "especially in dark mode." It says pure `gray` "will work well with any hue" ([Radix](https://www.radix-ui.com/colors/docs/palette-composition/composing-a-palette)). The shell frames prototypes that keep their own look, so a near-zero chroma gray is the safer choice.

### Token sets ready to adopt

| Set | Why use it | Source |
|---|---|---|
| Radix Colors `gray` | 12 steps with fixed roles, light and dark and alpha versions | [Radix scale](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale) |
| Vercel Geist gray | 100 to 1000 with documented roles | [Geist](https://vercel.com/geist/colors) |
| shadcn/ui Neutral | Paired light and dark semantic tokens in OKLCH (lightness, chroma, hue) | [shadcn/ui](https://ui.shadcn.com/docs/theming) |

The Radix role map is the clearest contract ([Radix](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale)).

- Steps 1 and 2 are app backgrounds.
- Step 6 is quiet dividers.
- Step 7 is interactive borders.
- Step 8 is focus rings.
- Steps 11 and 12 are text.

In Storybook, the `create()` theme variables cover most of the skin. They are `appBg`, `appContentBg`, `appPreviewBg`, `appBorderColor`, `barBg`, and `colorSecondary` as the single accent ([Storybook](https://storybook.js.org/docs/configure/user-interface/theming)). Hiding the toolbar and panel keeps the prototype dominant ([Storybook](https://storybook.js.org/docs/configure/user-interface/features-and-behavior)).

### The contrast floor for quiet

- **Text:** 4.5:1, or 3:1 when large ([W3C 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html)).
- **Controls and focus:** any border that is the only cue for a control needs 3:1 against what's next to it. So does every focus indicator ([W3C 1.4.11](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html)).
- **Decorative dividers:** these are exempt. Soft Linear-style separators are fine for structure, but input borders can't be that faint.
- **Thin lines:** W3C warns they render fainter than their CSS color (same source).
- **Radix contrast:** Radix only guarantees contrast in APCA (Accessible Perceptual Contrast Algorithm), not WCAG 2 ratios ([Radix](https://www.radix-ui.com/colors/docs/palette-composition/understanding-the-scale)). Check the real pairs yourself in both modes.

## Automated checks cover a slice, the checklist covers the rest

### Automated WCAG per story and state

`@storybook/addon-a11y` runs axe-core on every story ([Storybook](https://storybook.js.org/docs/writing-tests/accessibility-testing)). Its default rules are WCAG 2.0 and 2.1 only.

To set it up:

- **Add 2.2 AA:** set `parameters.a11y.options.runOnly` to include `wcag22aa` alongside the defaults (same source).
- **Fail on violations:** set `parameters.a11y.test = 'error'` globally and pair it with the Vitest addon. Any new violation then fails CI (continuous integration), per the same source.
- **Allow known issues:** mark known-broken components `'todo'`, and remove those as you fix them (same source).
- **Check the framework:** the Vitest addon needs a Vite-based framework ([Storybook](https://storybook.js.org/docs/writing-tests/integrations/vitest-addon)).

For deployed prototype URLs, use Playwright with `@axe-core/playwright` and add `wcag22aa` to `withTags` ([Playwright](https://playwright.dev/docs/accessibility-testing)). One spec per state mirrors the per-story model.

axe only checks what is rendered. Every state, including focus, error and empty, needs its own story or URL to be covered.

### What automation misses

Adding `wcag22aa` turns on only one rule, `target-size` ([axe-core](https://github.com/dequelabs/axe-core/blob/develop/doc/rule-descriptions.md)). Deque expects it to be the only WCAG 2.2 rule axe ever adds ([Deque](https://www.deque.com/blog/axe-core-4-5-first-wcag-2-2-support-and-more)). That leaves five new criteria for the manual list ([W3C](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/)).

| Criterion | Level | Check at |
|---|---|---|
| 2.4.11 Focus not obscured | AA | Each screen with sticky elements |
| 2.5.7 Dragging movements | AA | Any drag interaction |
| 3.2.6 Consistent help | A | Across prototype pages |
| 3.3.7 Redundant entry | A | Multi-step forms |
| 3.3.8 Accessible authentication | AA | Login flows |

Automated tools find **57% of real issues by volume** across 13,000+ pages and states ([Deque](https://www.deque.com/automated-accessibility-coverage-report/)). In an older GOV.UK test, every tool combined missed 29% of planted barriers ([GOV.UK](https://accessibility.blog.gov.uk/2017/02/24/what-we-found-when-we-tested-tools-on-the-worlds-least-accessible-webpage/)).

### Nielsen's 10 heuristics as a checklist

Use the canonical list from NN/g (Nielsen Norman Group), and credit Jakob Nielsen with a link, as NN/g asks ([NN/g](https://www.nngroup.com/articles/ten-usability-heuristics/)). Rate each problem 0 to 4, from "not a problem" to "usability catastrophe" ([NN/g severity](https://www.nngroup.com/articles/how-to-rate-the-severity-of-usability-problems/)).

Maze's free PDF breaks each heuristic into numbered yes, no or NA (not applicable) questions, which makes a ready checklist ([Maze](https://assets-cdn.maze.co/Heuristic+evaluation+checklist.pdf)).

**The solo catch:** one evaluator finds only about 35% of problems, and NN/g recommends at least three ([NN/g](https://www.nngroup.com/articles/how-to-conduct-a-heuristic-evaluation/theory-heuristic-evaluations/)). Single-evaluator severity ratings are "too unreliable to be trusted" ([NN/g severity](https://www.nngroup.com/articles/how-to-rate-the-severity-of-usability-problems/)).

Label results as single-evaluator. Add a second rater (a peer or an AI pass, scored separately) for anything rated 3 or 4.

Heuristics fit flows better than isolated components. Run them per prototype task flow, and per story only for interactive states.

### Where results live

No existing tool links heuristic findings to a Storybook story ID ([NN/g templates](https://www.nngroup.com/articles/how-to-conduct-a-heuristic-evaluation/), [Notion template](https://www.notion.com/templates/heuristic-evaluation-system), [Figma template](https://www.figma.com/community/file/905622673082476274/heuristic-evaluation-template)).

The toolkit's Checks tab fills the gap, with one row per finding. Each row holds the story or route, state, version, heuristic or WCAG criterion, severity, evaluator and status.

axe results stay in CI output. Chromatic is the paid option if you want per-story accessibility history without building it ([Chromatic](https://www.chromatic.com/docs/accessibility)).

## Every tool versions the same way: draft plus frozen snapshots

### How comparable tools do it

**Supernova** keeps an editable "Current draft" and read-only versions with a semver number, name and description ([Supernova](https://learn.supernova.io/latest/settings/design-system/versions-O5ZSWkgQ)).

**Zeroheight** releases freeze the styleguide, and a "Latest" release collects notes until the next one is cut ([zeroheight](https://help.zeroheight.com/hc/en-us/articles/35886984873883-Creating-and-managing-releases)). Zeroheight warns that embedded Storybooks in old releases show today's live Storybook unless you change the URL each release (same source).

That's the lesson: **version the whole deployed build,** not a page pointing at a live Storybook.

**Netlify** gives every deploy a permalink whose content "never changes" ([Netlify](https://docs.netlify.com/deploy/deploy-overview.md)). `netlify deploy --prod --message "..."` attaches a note ([Netlify CLI (command-line interface)](https://github.com/netlify/cli/blob/main/docs/commands/deploy.md)).

But **deploys are deleted after 30 days** (90 on paid plans), and a deleted permalink returns 404 ([Netlify](https://docs.netlify.com/deploy/manage-deploys/manage-deploys-overview)). Record each meeting's URL and notes somewhere durable.

For the changelog, Changesets bumps the version and writes changelog entries. It works for single-package repos ([Changesets](https://github.com/changesets/changesets/blob/main/README.md)). Storybook MDX (Markdown that can hold components) can render a CHANGELOG.md as a docs page ([Storybook](https://github.com/storybookjs/storybook/blob/next/docs/writing-docs/mdx.mdx)), so it shows inside the toolkit.

### Notes and ideation

Notes that live inside the artifact survive handoff.

- **Storybook MDX** supports standalone docs pages in the sidebar, alongside stories ([Storybook MDX](https://storybook.js.org/docs/writing-docs/mdx)).
- **Figma Dev Mode annotations** use categories like Accessibility, Development and Interaction ([Figma](https://help.figma.com/hc/en-us/articles/20774752502935-Add-measurements-and-annotate-designs)). That's a good structure for per-screen notes.
- **Storybook tags** can mark status, like experimental, stable or deprecated ([Storybook](https://storybook.js.org/docs/writing-stories/tags)).

Comment threads go stale. Chromatic disables comments on old builds ([Chromatic](https://chromatic.com/docs/quickstart)). The Netlify Drawer allows live review comments, but only on Deploy Previews and branch deploys, **not permalinks** ([Netlify](https://docs.netlify.com/deploy/review-deploys/netlify-drawer-for-feedback/overview)).

### Copy decisions

Ditto and Frontitude share one pattern. Each string has a stable key, a status (Draft, In Review, Final), comments and an activity log ([Ditto](https://help.dittowords.com/en/articles/13192027-status), [Frontitude](https://www.frontitude.com/guides/automate-your-developer-handoff)).

Developers pull only final strings into code, for example `frontitude pull --status=final` ([Frontitude](https://www.frontitude.com/blog/introducing-frontitudes-first-developer-integration)). Ditto writes the status into the Figma layer name, so people without a seat can see it ([Ditto](https://help.dittowords.com/en/articles/13192027-status)).

Neither tool is needed for one writer. A strings file per prototype with key, text, status and a short note on why shows the same handoff skill. An MDX page can render it as a copy deck.

## The real gap is linking, not tooling

No product ties a heuristic finding, a copy decision and a frozen build together by story ID and version. The toolkit's details page, keyed on state and deploy link, closes that gap. It's the kind of thing a stakeholder reads as handoff skill rather than tool shopping.

Confirm one thing before committing. Run one real prototype through html.to.design's free tier and one Figma capture before paying for either. No fidelity test on Sharon's own prototypes exists yet.
