# Designer toolkit: Spec

**Last updated:** October 12, 2026

**Status:** draft, low fidelity. This spec agrees on a direction. Screens and components come after.

## TL;DR

- The toolkit is Sharon's workspace for coded prototypes. It frames any prototype and holds every state, doc, comment, idea, copy decision, check and version beside it.
- When work is done, every state goes to Figma, so clients and teammates get the files they expect without the toolkit.
- Documentation, comments, ideas, copy, checks and versions save to Supabase. Invited reviewers can then comment from a shared link, and Sharon sees their comments in the toolkit. Sign-in keeps each prototype private.

## What the words mean

- **Shell:** the toolbar and panels around a prototype. It owns no product screens.
- **Prototype:** a product build the shell frames, like the client portal.
- **State:** one named view of a screen, like empty, loading, error or a persona's view. Each state has its own link.
- **Details page:** the page behind each prototype that holds its documentation, comments, ideas, copy, checks and versions.
- **Version:** one Netlify deploy, made before a meeting or a share.
- **Contract:** the agreed messages the shell and a prototype use to share state.
- **Supabase:** the database behind the toolkit. It saves what people write, from the toolkit or from a shared link.

## How the area works today

- The original toolkit build runs on its own and shows BambooHR prototypes. The toolbar host that drove it was never in the build.
- Each prototype describes its versions, personas and page states in a `prototype-config.json` file. The original also kept docs links, future work, to-dos and version notes in JSON files beside it.
- Notes, ideas and copy for new work end up in chat, Notion, FigJam, Google Docs and the code.
- Clients ask for Figma files. Today that means redrawing coded screens by hand.
- Nothing checks a prototype's usability or accessibility on a schedule.

## Problems to solve

1. A viewer can't see every state of a prototype in one place, so handoff gets described instead of shown.
2. Notes, ideas, copy and decisions are scattered, so Sharon re-finds context before every meeting.
3. Clients want Figma files, and redrawing coded screens wastes hours and drifts from the code.
4. There's no record of what changed between the versions people reviewed.
5. Usability and accessibility checks happen by memory, so gaps show up late.

## Goals

- Anyone with the link can switch a prototype's version, persona and state from one toolbar.
- Every doc, comment, idea and copy decision for a prototype is one click from the prototype.
- Every state reaches Figma in one pass, in light and dark, with no redrawing.
- Every version people reviewed can be reopened, with what changed since the one before.
- Every state shows its accessibility result and heuristic score.
- The shell stays quiet, so the prototype is the only thing that stands out.

## Out of scope

- Live Jira, Slack or comment syncing. The original panels pulled from internal tools.
- Changing a prototype's own look. Prototypes keep their own styles.
- Real-time collaboration inside the toolkit. People review through links and Figma.
- Sending the toolkit itself to clients.

## Sources of truth

- **What are a prototype's versions, personas and states?** That prototype's `prototype-config.json`, in its own repo.
- **Which prototypes does the shell list?** The ones Sharon added by link or HTML file, saved in Supabase. Each deploy ships a snapshot of that list, so later changes don't alter links people already have.
- **What documentation, ideas and comments exist?** Supabase, tied to the prototype. Comments are also tied to a state and version.
- **What's the approved wording for a screen?** The copy table in Supabase, one row per string.
- **What did each version change?** The versions table in Supabase, one row per deploy, with its permanent link.
- **Who can see a prototype?** Sharon, plus invited reviewers, who see only its comments. Supabase's access rules (row-level security) enforce it.
- **What are the components and tokens?** Storybook in [design-system-skeleton](https://github.com/sharonlafleur1984/design-system-skeleton) for the shell. Each prototype's own Storybook or code for its components.
- **What's the design of record for the client?** The Figma file the states are sent to.
- **What is the viewer looking at right now?** The shell's state, mirrored to the page address so a link reopens the same view.

## Fields and editors

- **Version, persona, state:** the viewer picks them in the toolbar, or they arrive from a shared link.
- **The choices in each list** come from the prototype's config file. Nobody types them in the shell.
- **Comments from reviewers:** people Sharon invites by email to one prototype write them, after signing in with a magic link. Sharon may resolve or hide them.
- **Documentation and ideas:** Sharon writes them on the details page. Documentation is a wiki of Markdown pages in folders, and each edit saves the earlier copy. Each idea keeps its date and the version it was written against, filled in by the toolkit.
- **Copy strings:** each has a key, the text, a status (draft, in review, final) and a note. Sharon fills the text and status. The key is set once in code.
- **Version entry:** the deploy link and date are filled by the deploy. Sharon may add a summary. The comments and documentation changes since the last version are pulled in automatically, and Sharon may edit the summary.
- **Accessibility result:** filled by the automated check on each state. Nobody types it.
- **Heuristic score:** Sharon scores each of Nielsen's 10 heuristics from 0 to 4 per state. A second pass by AI may suggest scores, and Sharon overwrites them.
- **Figma link per state:** filled when the state is sent to Figma.

## Page design

- **The toolbar** sits outside the prototype frame, so it never covers product screens. Version, persona and state are visible. Platform, add-ons and dev mode sit behind a "More" control.
- **One shortcut** (Cmd or Ctrl and backslash) hides the toolbar for clean screenshots, matching the original.
- **The details page** opens from the toolbar, with tabs for Documentation, Comments, Ideas, Copy, Checks and Versions.
- **Documentation is the default tab.** It holds the prototype's wiki, made of Markdown pages in folders. Every other tab lists its newest items first.
- **States** show as a grid of thumbnails on the details page, each with its link, its check results and its Figma link.
- **The shell is always dark.** Reading surfaces, like the Documentation tab, can switch between light and dark. The prototype's own theme toggle stays separate.
- **Never shown:** former employers' personal data (names, emails, Slack IDs), client notes in any public view, and company-only internal links.

The look itself lives on [Skin](Skin).

## Requirements

| Priority | Requirement | How it gets checked |
|---|---|---|
| Must | Switching version, persona or state updates the framed prototype within 400ms | Playwright test per control |
| Must | The shell sends state with the original message type, so unchanged prototypes respond | Playwright test against the original build |
| Must | Every state has its own link that reopens it exactly | Playwright test opens each state link from the config |
| Must | A comment left on a shared Netlify link shows in the Comments tab | Playwright test leaves a comment on a deploy as an invited reviewer, then reads it in the toolkit |
| Must | Only reviewers invited to a prototype can read or write its comments, and everything else stays Sharon's alone | A test signs in as an invited reviewer, who reads only comments, and as an outsider, who reads nothing |
| Must | No Supabase secret key ships to the browser or the repo | Gitleaks in CI (continuous integration), plus a check that the build holds only the publishable key |
| Must | Every control works by keyboard, with a visible focus ring | axe scan plus a keyboard Playwright test |
| Must | Every state passes axe with WCAG 2.2 AA (Web Content Accessibility Guidelines, level AA) rules switched on (`wcag22aa`) | Storybook a11y (accessibility) addon set to `error`, and `@axe-core/playwright` on state links |
| Must | Every deploy adds a version row with its permanent link and the comments and documentation changes since the last one | A Netlify `onSuccess` build plugin writes the row, checked by a test |
| Must | Every state can be sent to Figma in light and dark in one pass | Manual run on one real prototype, with a count of frames against states |
| Should | Each state shows its last heuristic score and who scored it | Manual review of the Checks tab |
| Should | Copy marked final is the only copy shipped in a version | A test fails if a shipped string's status isn't final |
| Should | The toolbar hides and returns with the shortcut | Playwright test |
| Could | A dev mode panel shows the current state as code a developer can copy | Manual review |

## Dependencies

- The [design system](https://github.com/sharonlafleur1984/design-system-skeleton) adds a toolkit theme. Its Roadmap lists this under Later.
- A Supabase project for the toolkit, created Oct 12, 2026.
- Each prototype loads a small script that lets invited reviewers comment from its shared link.
- A Figma capture tool. See [Open decisions](#open-decisions).
- Netlify, for hosting and deploy links.

## How we'll judge the options

For getting states into Figma, the criteria are:

- frames that stay editable
- light and dark in one pass
- cost for one person
- how much of it Claude can run

## Options and the pick

How states get to Figma. Full comparison on [Research](Research#htmltodesign-gives-the-best-value-for-state-frames).

| Option | What it costs |
|---|---|
| **html.to.design, bulk import of state links (recommended)** | About $12 a month on PRO. Editable frames with auto layout, but no Figma variants. |
| Figma's own capture (`generate_figma_design`) | Free during the beta, but one page at a time and raw layers |
| story.to.design | About $149 a month. Real Figma components with variants, but not screens laid out as a flow |

## Open decisions

- **How should states get to Figma?** The recommendation is to try one real prototype on html.to.design's free tier and on Figma's free capture. Then pay for html.to.design PRO only if its frames are clearly better.
- **Which free font stands in for Fields?** This is for the BambooHR prototypes. The recommendation will come with a side-by-side comparison.

## On the bench

[Backlog](Backlog)

## Success metrics

| Problem it watches | What changes | Where the number comes from | If it moves the wrong way |
|---|---|---|---|
| A viewer can't see every state in one place (problem 1) | First-time viewers who find a named state, its documentation and its version in under a minute | Notes from 3 recorded sessions | Rework the toolbar and details page labels, then test again |
| Clients want Figma files (problem 3) | States that land in Figma without redrawing, out of all states | Frames in the Figma file against states in the config | Switch capture tools, or fix the states that break |
| No record of what changed (problem 4) | Versions with a working link and a summary of changes, out of all deploys | The versions table in Supabase | Fix the deploy plugin, then backfill from Netlify's deploy list |
| Checks happen by memory (problem 5) | States with a current accessibility result and heuristic score | The Checks tab | Add the missing checks to the deploy step |

## Risks and what we'd do

On the [Roadmap](Roadmap#what-could-go-wrong).

## Rabbit holes

- Rebuilding every original panel. Jira, specs and comments pulled from internal tools.
- Building threaded, real-time comments like Figma's. A comment per state, with one level of replies, that Sharon can resolve covers it.
- Recovering readable source for the BambooHR prototypes. The unminified code has machine-made names, so a rebuild beats a restore.
- Treating the heuristic score as the whole truth. One evaluator finds only about 35% of problems ([Nielsen Norman Group](https://www.nngroup.com/articles/how-to-conduct-a-heuristic-evaluation/theory-heuristic-evaluations/)), so scores are labeled single evaluator.

## Known defects

- **Outside fonts.** Icons are bundled from Font Awesome Free. Fields still loads, and gets replaced.
- **Personal data in the original JSON.** The original project files hold former coworkers' names, emails and Slack IDs. They stay in the private repo and get swapped for sample data before anything is public.

## Build order

In dependency order, in four stages.

### Stage 1: a build that runs on its own, with tests

1. Finish bundling fonts, so the build runs on its own.
2. Write the contract down.
3. Add Playwright tests against the original build.

### Stage 2: the toolbar and state links

4. Build the toolbar on the contract.
5. Give every state its own link.

### Stage 3: saving to Supabase

6. Set up Supabase: the tables, sign-in and access rules per prototype.
7. Build the details page on Supabase, including comments from the shared link.
8. Add the deploy plugin that writes each version to Supabase.

### Stage 4: checks, Figma and the skin

9. Add the accessibility check per state.
10. Add the heuristic scoring.
11. Test the Figma capture on one real prototype.
12. Make the Figma capture one pass for every state.
13. Move the shell onto the Fireside theme in Storybook.

---

Private details, like the original files and where they came from, live in Sharon's private Notion project documents.
