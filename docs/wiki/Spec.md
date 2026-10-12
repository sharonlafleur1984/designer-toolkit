# Designer toolkit shell: Spec

**Last updated:** October 11, 2026

**Status:** draft, low fidelity. This spec agrees on a direction. Screens and components come after.

## TL;DR

- The shell frames any prototype and switches its version, persona and page state, so a viewer can try developer handoff instead of reading about it.
- The original build already speaks a clear message contract. The shell is rebuilt on that contract, so old prototypes work unchanged.
- The shell is Sharon's own work, built from her design system. The prototypes inside keep their original look and stay private.

## What the words mean

- **Shell:** the toolbar and panels around a prototype. It owns no product screens.
- **Prototype:** a product build the shell frames, like the client portal.
- **Contract:** the agreed messages the shell and a prototype use to share state.
- **Page state:** a named scenario for a screen, like an empty state or an error.

## How the area works today

- The original toolkit build runs as a standalone app with its own small view bar.
- When framed, the app hides that bar and waits for a host to send state. That host was never in the build, so nothing drives it.
- Icons and fonts load from BambooHR's servers. Without them, icons render as blank squares.
- Each prototype describes its own versions, personas and page states in a config file, so the shell has everything it needs to list.

## Problems to solve

1. Nobody outside BambooHR can use the toolkit as it was meant to be used, because the toolbar is missing.
2. The build depends on BambooHR's servers for icons and fonts, which can stop working any day.
3. Sharon's portfolio describes her handoff skill, but a viewer can't try it.

## Goals

- A viewer switches version, persona and page state on a real prototype from one toolbar.
- Any prototype that follows the contract works in the shell without changes.
- The shell looks and feels like Sharon's work, not a copy of the original.

## Out of scope

- Live Jira, spec or comment syncing. The original panels pulled from internal tools.
- Changing the prototypes' own screens.
- Making BambooHR source code public.

## Sources of truth

- **What versions, personas and page states does a prototype have?** That prototype's `prototype-config.json`.
- **Which prototypes does the shell list?** One registry file in the shell's repo.
- **What is the viewer looking at right now?** The shell's state, mirrored to the page address so a link reopens the same view.
- **How do the shell and a prototype talk?** The contract, documented in the shell's repo.

## Fields and editors

- **Version, persona, page state:** the viewer picks them in the toolbar, or they arrive from a shared link.
- **The choices in each list** come from each prototype's config file. Nobody types them in the shell.
- **Default version and persona:** set by the prototype's config, and the viewer may overwrite them.

## Page design

- The toolbar sits outside the prototype frame, so it never covers product screens.
- Version, persona and page state are visible. Platform, add-ons and dev mode sit behind a "More" control.
- One keyboard shortcut (Cmd or Ctrl and backslash) hides the toolbar for clean screenshots, matching the original.
- Never shown: internal links, Jira data or anything else that only made sense inside BambooHR.

## Requirements

| Priority | Requirement | How it gets checked |
|---|---|---|
| Must | Switching version, persona or page state updates the framed prototype within 400ms | Playwright test per control |
| Must | The shell sends state with the original message type, so unchanged prototypes respond | Playwright test against the original build |
| Must | No request goes to BambooHR's servers | Network check in Playwright fails on any such request |
| Must | Every control works by keyboard, with a visible focus ring | axe scan plus a keyboard Playwright test |
| Should | A shared link reopens the same prototype and view | Playwright test opens a copied link |
| Should | The toolbar hides and returns with the shortcut | Playwright test |
| Could | A dev mode panel shows the current state as code a developer can copy | Manual review |

## Dependencies

- The [design system](https://github.com/sharonlafleur1984/design-system-skeleton) adds a toolkit theme. Its Roadmap lists this under Later.
- The client portal and current product prototypes stay reachable to the shell, in private repos.

## Options and the pick

Where the public shell lives.

| Option | What it costs |
|---|---|
| **New public repo for the shell (picked)** | One more repo. The BambooHR source stays private, with no history to scrub. |
| Clean the original repo, rewrite its history, then make it public | Fiddly, and one missed file leaks internal data |

## Open decisions

- **Which free font stands in for Fields in the prototypes?** The recommendation comes with a side-by-side comparison.
- **Is a public demo of the BambooHR screens okay?** The recommendation is to host only with sample data, after the repos are private.

## On the bench

N/A. No ideas parked yet.

## Success metrics

| Problem it watches | What changes | Where the number comes from | If it moves the wrong way |
|---|---|---|---|
| A viewer can't try the handoff tooling (problem 3) | First-time viewers who switch all three controls in under a minute | Notes from 3 recorded sessions | Rework the toolbar's labels and layout, then test again |
| The build breaks without BambooHR's servers (problem 2) | Requests to BambooHR's servers per page load | The Playwright network check | Find the new request and bundle that file |

## Risks and what we'd do

On the [Roadmap](Roadmap#what-could-go-wrong).

## Rabbit holes

- Rebuilding every original panel. Jira, specs and comments pulled from internal tools, and none of that belongs in a public piece.
- Recovering readable source for the prototypes. The unminified code has machine-made names, so a rebuild beats a restore.

## Known defects

- **Outside icons and fonts.** Icons are now bundled from Font Awesome Free, with close stand-ins for about 70 that only exist in the paid set. Fonts are next.

## Build order

1. Finish bundling icons and fonts, so the build runs on its own.
2. Write the contract down and add Playwright tests against the original build.
3. Build the toolbar on the contract.
4. Register the client portal and current product prototypes.
5. Move the toolbar onto the design system's toolkit theme, in Storybook.
6. Host it.

Private details, like the original files and where they came from, live in Sharon's private Notion project documents.
