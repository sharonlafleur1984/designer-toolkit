# Designer toolkit: Spec

**Last updated:** October 14, 2026

**Status:** draft, low fidelity. This spec agrees on a direction. Screens and components come after.

## TL;DR

- The toolkit is Sharon's workspace for coded prototypes. It frames any prototype and holds every page state, doc, comment, idea, copy decision, check and version beside it.
- When work is done, every page state goes to Figma, so clients and teammates get the files they expect without the toolkit.
- Comments, ideas, copy, checks and versions save to Supabase. Invited reviewers can then comment from a shared link, and Sharon sees their comments in the toolkit. Sign-in keeps each prototype private.
- Documentation comes from the prototype's linked repo when there is one, and changes go back to it through approval.

## What the words mean

- **Shell:** the sidebar, toolbar and panels around a prototype. It owns no product screens.
- **Prototype:** a product build the shell frames, like the client portal.
- **Milestone:** a finish line inside a prototype's work, from the linked repo or from a spec written in the toolkit.
- **Page:** one screen of the prototype, listed under the milestone it belongs to.
- **Page state:** one named view of a page, like default, an edge case or an error. Each page state has its own link.
- **Details page:** the page behind each prototype that holds its documentation, notes, ideas and heuristic review.
- **Project docs:** the linked repo's wiki, as collaborators see it. Collaborators never see GitHub's own words (see [Saving and approval](#saving-and-approval)).
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

1. A viewer can't see every page state of a prototype in one place, so handoff gets described instead of shown.
2. Notes, ideas, copy and decisions are scattered, so Sharon re-finds context before every meeting.
3. Clients want Figma files, and redrawing coded screens wastes hours and drifts from the code.
4. There's no record of what changed between the versions people reviewed.
5. Usability and accessibility checks happen by memory, so gaps show up late.

## Goals

- Anyone with the link can move between a prototype's milestones, versions, pages and page states from one sidebar.
- Every doc, comment, idea and copy decision for a prototype is one click from the prototype.
- Every page state reaches Figma in one pass, in light and dark, with no redrawing.
- Every version people reviewed can be reopened, with what changed since the one before.
- Every page state shows its accessibility result and heuristic review.
- The shell stays quiet, so the prototype is the only thing that stands out.

## Out of scope

- Live Jira, Slack or comment syncing. The original panels pulled from internal tools.
- Changing a prototype's own look. Prototypes keep their own styles.
- Real-time collaboration inside the toolkit. People review through links and Figma.
- Sending the toolkit itself to clients.
- Phones. The toolkit is designed for desktop only, now and in any plan.

## Sources of truth

- **What versions, personas and page states exist?** The prototype's `prototype-config.json`, in its own repo.
- **Which prototypes does the shell list?** The ones Sharon added by link or HTML file, saved in Supabase. Each deploy ships a snapshot of that list, so later changes don't alter links people already have.
- **What documentation exists?** The linked repo's `docs/wiki`, always shown at its latest. A prototype with no linked repo keeps its documents in Supabase.
- **What milestones exist?** The linked repo's GitHub milestones, plus any specs written in the toolkit. Both can exist, each labeled with its source, and they're never merged.
- **Who changed a document, and was it approved?** The `document_versions` table in Supabase, shown on the document's History page.
- **What ideas and comments exist?** Supabase, tied to the prototype. Comments are also tied to a page state and version.
- **What's the approved wording for a screen?** The copy table in Supabase, one row per string.
- **What did each version change?** The versions table in Supabase, one row per deploy, with its permanent link.
- **Who can see a prototype?** Sharon, plus invited reviewers, who see only its comments. Supabase's access rules (row-level security) enforce it.
- **What are the components and tokens?** Storybook in [lantern-design-system](https://github.com/sharonlafleur1984/lantern-design-system) for the shell. Each prototype's own Storybook or code for its components.
- **What's the design of record for the client?** The Figma file the page states are sent to.
- **What is the viewer looking at right now?** The shell's state, mirrored to the page address so a link reopens the same view.

## Fields and editors

- **Sidebar choices:** prototype, milestone, version, page and page state. The viewer picks them in the sidebar, or they arrive from a shared link.
- **The choices in each list** come from the prototype's config file. Nobody types them in the shell.
- **Comments from reviewers:** people Sharon invites by email to one prototype write them, after signing in with a magic link. Sharon may resolve or hide them.
- **Documentation:** Sharon and collaborators write it on the details page, in the rich text editor (see [Editor and saving](#editor-and-saving)).
- **Project spec:** a name, a summary and milestone names. Adding it with milestone names creates a milestone spec for each one, with the name filled in.
- **Milestone spec:** the milestone's name, then Summary, Due date, Success looks like and Pages. Each of the four is optional and labeled "(optional)".
- **Ideas:** each keeps its date and the version it was written against, filled in by the toolkit.
- **Copy strings:** each has a key, the text, a status (draft, in review, final) and a note. Sharon fills the text and status. The key is set once in code.
- **Version entry:** the deploy link and date are filled by the deploy. Sharon may add a summary. The comments and documentation changes since the last version are pulled in automatically, and Sharon may edit the summary.
- **Accessibility result:** filled by the automated check on each page state. Nobody types it.
- **Heuristic review findings:** the AI review fills them, and the owner keeps, edits or dismisses each one (see [Heuristic review](#heuristic-review)).
- **Figma link:** filled when the page state is sent to Figma.

## Page design

The toolkit is built for desktop screens. One rule runs through every page: when there's nothing to show, show nothing. Empty due dates, summaries and milestones get no placeholder line.

### Sidebar and the order of things

Work nests in this order: prototype, then problem, then milestone (picked in the dropdown), then page, then page states.

- **The sidebar** lists Prototype, Milestone and Version, in that order. Version shows only when there are 2 or more versions.
- **Under those fields** sit the chosen milestone's pages. Each page opens to its page states (default, edge cases, errors). The current page is open, with Default selected.
- **No milestones yet:** the Milestone field is disabled and reads "No milestones yet". Under it, a quiet instruction reads "Link a repo or add a spec to start adding milestones."
  - Two buttons follow: Link a repo (primary) and Add a spec (secondary).
- **Linking a repo** goes through a "Connect this prototype" review. It shows what was found and where, and Sharon confirms it. Nothing is guessed.
- **The toolbar** sits outside the prototype frame, so it never covers product screens. It opens Dev mode, Comments, Properties and Settings.
- **One shortcut** (Cmd or Ctrl and backslash) hides the toolbar for clean screenshots, matching the original.

### Details page and Documentation

- **The details page** has tabs for Documentation, Notes & ideation and Heuristic review. Comments and Properties belong to each page state. Every tab except Documentation lists its newest items first.
- **Page states** show as a grid of thumbnails on the details page, each with its link, its check results and its Figma link.
- **Documentation is the default tab.** Its list starts with a quiet "+ Add document" (muted, with a plus icon), then categories that open and close.
- **Category order** follows the linked repo's wiki sidebar when there is one (for example Plan, Research, Reference, Meeting notes), plus the toolkit's Spec category. Without a wiki, the order is Overview, Spec, Decisions, Research, Handoff notes.
- **The Spec category** holds one project spec, with a milestone spec nested under it for each milestone.
- **Specs open as clean documents.** A gear opens their fields, where milestones can be added, renamed and removed. Removing one asks first.
- **Unsaved changes** ask before anyone leaves the page.

Templates arrive in this order.

1. **Spec,** now.
2. **Meeting notes,** next. Each is named by its date and holds when, who, what it's for, questions, notes, decisions and follow-ups. It can be linked to a milestone.
3. **Overview, Decisions, Research and Handoff notes,** after that.

### What follows the selected milestone

Picking a milestone never hides anything. Tabs and lists keep every item, and the selection only changes where each tab opens. A "Showing: <milestone>" line and a Show all control say what's in focus. The selection steers only when it changes.

| Scope | What it covers |
|---|---|
| Project-wide | Overview, project spec, Plan, Research, Reference, and Research in Notes & ideation |
| Per milestone | Milestone specs, Handoff notes, Links in Notes & ideation, and Heuristic review. Comments and Properties go one level lower, per page state. |
| Project-wide, taggable to a milestone | Meeting notes, Decisions and Ideas. Items tagged to the selected milestone show first. |

### Heuristic review

Each page state gets two kinds of check, labeled so judgment is never mistaken for measurement.

- **Measured:** automated accessibility scans.
- **Judgment:** an AI heuristic review, with each finding's severity (0 to 4), location and fix. Findings stay labeled "AI review" until the owner keeps, edits or dismisses them.

### Editor and saving

- **The editor is rich text, stored as Markdown,** so every document works in a GitHub wiki. It covers headings, bold, italic, strikethrough, links, bulleted, numbered and checklist lists, quotes, code, tables and dividers. Images come later.
- **Formatting** works from the toolbar and from Markdown shortcuts. Pasting from Google Docs, Notion or Word keeps whatever a wiki can show.
- **Add document** opens a blank page right away. It has a title and the muted line "Start typing, or paste your text here."
- **A quiet Templates toggle** shows or hides the template cards. They're hidden by default.
- **Clicking into the text** starts editing. The editor toolbar appears and ends with "Save changes".
- **Saving** hides the toolbar, and the page reads clean again. Nothing saves on its own.
- **"Saved" shows only after the save is confirmed.** This one is non-negotiable. Nothing says it saved, sent or was approved unless the code confirmed it.
- **A failed save** says why and what to do, and the text stays in edit mode.

### Saving and approval

The toolkit always shows the latest project docs. "Send for approval" opens a pull request on the repo's `docs/wiki`, and conflicts are resolved in the repo, never in the toolkit.

Collaborators see everyday words. GitHub's words show only in owner-only settings.

| Collaborators see | GitHub's word |
|---|---|
| project docs | wiki |
| project | repo |
| sent for approval | pull request |
| approve | merge |
| History | commit history |

The approved messages:

| When | Message |
|---|---|
| A save is confirmed | Saved |
| Offline | Couldn't save. You're offline. Your changes are still here, so try again once you're back online. |
| Signed out | Couldn't save. You've been signed out. Sign in again, and your changes will still be here. |
| Someone else changed the page | Couldn't save. Someone else changed this page while you were editing. Copy your changes before you reload the page. |
| The button that sends a change | Send for approval |
| Sending worked | Sent for approval. It shows in the project docs once it's approved. |
| Approved | Approved and added to the project docs. |
| No permission | Couldn't send this for approval. You don't have permission to change these docs. Ask the owner for access. |
| Leaving with unsaved changes | Discard your changes? |

### History

- **Each document has a History page,** a page of its own. A back link above it shows the document's name, like "← Portal plan", and Esc goes back.
- **The History table** has the columns Editor, Date, Change, Approved and Restore. Approved holds a timestamp, or Pending.
- **Change** is a short description the toolkit writes, and the editor can reword it.
- **Formatting-only changes** fold into the next real change.
- **Restore** makes a new change, which goes through approval like any other.
- **A page with a pending change** is read-only for everyone except its editor, with a line like "Alex's changes are waiting for approval. You can edit once they're approved."
- **A prototype with no linked docs** has no approval step. Saving is final, and History has no Approved column.

### Settings

Settings has two tabs.

- **Prototypes:** the prototype list, with rename, remove and remove all. Each prototype shows its linked repo with Change and Unlink, or "No repo linked" with Link a repo. People sits here too.
- **Toolkit:** Accessibility (Appearance and Display), Keyboard shortcuts, and Account.

### Privacy and the look

- **Private pages say so.** Each one opens with "Private to you and invited collaborators." A muted "Invite collaborators" link goes to Settings → Prototypes → People.
- **One selected style** for every button set, a faint fill with copper (primary) text.
- **One small type scale:** labels at 9px in small capitals, meta text at 11px, and body text at 12px.
- **The shell is always dark.** Reading surfaces, like the Documentation tab, can switch between light and dark. The prototype's own theme toggle stays separate.
- **Never shown:** former employers' personal data (names, emails, Slack IDs), client notes in any public view, and company-only internal links.

The look itself lives on [Skin](Skin).

## Requirements

| Priority | Requirement | How it gets checked |
|---|---|---|
| Must | Switching prototype, milestone, version, page or page state updates the framed prototype within 400ms | Playwright test per control |
| Must | The shell sends state with the original message type, so unchanged prototypes respond | Playwright test against the original build |
| Must | Every page state has its own link that reopens it exactly | Playwright test opens each page state link from the config |
| Must | "Saved", "Sent for approval" and "Approved" show only after the code confirms them, and a failed save keeps the text in edit mode | Playwright tests that fail the save offline, signed out and on a conflict |
| Must | A page with a pending change is read-only for everyone except its editor | A test signs in as the editor and as a second collaborator |
| Must | Every keyboard shortcut listed in Settings works | One test per listed shortcut |
| Must | A comment left on a shared Netlify link shows in the Comments tab | Playwright test leaves a comment on a deploy as an invited reviewer, then reads it in the toolkit |
| Must | Only reviewers invited to a prototype can read or write its comments, and everything else stays Sharon's alone | A test signs in as an invited reviewer, who reads only comments, and as an outsider, who reads nothing |
| Must | No Supabase secret key ships to the browser or the repo | Gitleaks in CI (continuous integration), plus a check that the build holds only the publishable key |
| Must | Every control works by keyboard, with a visible focus ring | axe scan plus a keyboard Playwright test |
| Must | Every page state passes axe with WCAG 2.2 AA (Web Content Accessibility Guidelines, level AA) rules switched on (`wcag22aa`) | Storybook a11y (accessibility) addon set to `error`, and `@axe-core/playwright` on state links |
| Must | Every deploy adds a version row with its permanent link and the comments and documentation changes since the last one | A Netlify `onSuccess` build plugin writes the row, checked by a test |
| Must | Every page state can be sent to Figma in light and dark in one pass | Manual run on one real prototype, with a count of frames against page states |
| Should | Each page state shows its heuristic review, with AI findings labeled until the owner keeps, edits or dismisses them | Manual review of the Heuristic review tab |
| Should | Copy marked final is the only copy shipped in a version | A test fails if a shipped string's status isn't final |
| Could | A dev mode panel shows the current state as code a developer can copy | Manual review |

## Dependencies

- The [design system](https://github.com/sharonlafleur1984/lantern-design-system) adds a toolkit theme. Its Roadmap lists this under Later.
- A Supabase project for the toolkit, created Oct 12, 2026.
- The GitHub connection, to read a linked repo's milestones and wiki and to send changes for approval.
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
- **What does Appearance in Settings change?** The shell is always dark (Oct 12), and the build now has a light mode too. Either the shell can go light, or Appearance covers only reading surfaces.
- **Where do the older controls live now?** Personas, Platform, add-ons, Copy and Versions aren't in the new sidebar, toolbar or details page tabs.

## On the bench

[Backlog](Backlog)

## Success metrics

| Problem it watches | What changes | Where the number comes from | If it moves the wrong way |
|---|---|---|---|
| A viewer can't see every state in one place (problem 1) | First-time viewers who find a named page state, its documentation and its version in under a minute | Notes from 3 recorded sessions | Rework the sidebar and details page labels, then test again |
| Clients want Figma files (problem 3) | Page states that land in Figma without redrawing, out of all page states | Frames in the Figma file against page states in the config | Switch capture tools, or fix the states that break |
| No record of what changed (problem 4) | Versions with a working link and a summary of changes, out of all deploys | The versions table in Supabase | Fix the deploy plugin, then backfill from Netlify's deploy list |
| Checks happen by memory (problem 5) | Page states with a current accessibility result and heuristic review | The Heuristic review tab | Add the missing checks to the deploy step |

## Risks and what we'd do

On the [Roadmap](Roadmap#what-could-go-wrong).

## Rabbit holes

- Rebuilding every original panel. Jira, specs and comments pulled from internal tools.
- Building threaded, real-time comments like Figma's. A comment per state, with one level of replies, that Sharon can resolve covers it.
- Recovering readable source for the BambooHR prototypes. The unminified code has machine-made names, so a rebuild beats a restore.
- Treating the heuristic review as the whole truth. One evaluator finds only about 35% of problems ([Nielsen Norman Group](https://www.nngroup.com/articles/how-to-conduct-a-heuristic-evaluation/theory-heuristic-evaluations/)), so AI findings stay labeled until the owner keeps, edits or dismisses them.

## Known defects

- **Outside fonts.** Icons are bundled from Font Awesome Free. Fields still loads, and gets replaced.
- **Personal data in the original JSON.** The original project files hold former coworkers' names, emails and Slack IDs. They stay in the private repo and get swapped for sample data before anything is public.

## Build order

In dependency order, in four stages.

### Stage 1: a build that runs on its own, with tests

1. Finish bundling fonts, so the build runs on its own.
2. Write the contract down.
3. Add Playwright tests against the original build.

### Stage 2: the sidebar and page state links

4. Build the sidebar on the contract.
5. Give every page state its own link.

### Stage 3: saving to Supabase

6. Set up Supabase: the tables, sign-in and access rules per prototype.
7. Build the details page on Supabase, including comments from the shared link.
8. Add the deploy plugin that writes each version to Supabase.

### Stage 4: checks, Figma and the skin

9. Add the accessibility check per page state.
10. Add the AI heuristic review.
11. Test the Figma capture on one real prototype.
12. Make the Figma capture one pass for every page state.
13. Move the shell onto the Fireside theme in Storybook.

---

Private details, like the original files and where they came from, live in Sharon's private Notion project documents.
