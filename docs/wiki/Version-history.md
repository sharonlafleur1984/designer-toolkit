# Version history

Last updated: Oct 19, 2026

- **What it is:** every version of a prototype, in the toolbar, so anyone can look at an earlier one.
- **How versions get added:** one for each update to the prototype, from wherever it's hosted or uploaded. Until the toolkit hears about updates, it uses the versions the prototype already lists, in the prototype's own order.
- **What a version means is up to you.** You choose a naming style when you first connect a prototype, and you can change it later.

## The problem

Designers and their teams need to see what changed between rounds, and to show an earlier round without digging for it. The toolkit frames one prototype at a time, so versions have to live beside it.

It works when someone picks any version from the toolbar and the prototype switches to it. A new update shows up as a new version on its own.

## How it works

1. **In the toolbar:** a Version menu, with the newest first.
2. **A new update adds a version.** The toolkit learns about updates from the host (a deploy) or from a new upload. Each one becomes a version.
3. **When the toolkit can't hear about updates yet,** it shows the versions the prototype lists about itself, in that order.
4. **How it's decided is explained in place:** an info icon next to Version opens a short note. The note never names a host, because the source could be an upload.
5. **Naming:** chosen when the prototype is connected, with a few options to pick from, and changeable in Settings.

## Naming options to offer at connect time

| Option | Looks like | Fits |
|---|---|---|
| Milestone and round | Milestone 2, round 3 | Work planned by milestones |
| Date | Oct 19 | Frequent updates with no fixed plan |
| Number | v12 | Simple counting |
| Your own words | "Beta with reports" | Teams that name rounds as they go |

The default is Milestone and round, since milestones already organize the toolkit.

## What it needs first

- The host to tell the toolkit about updates. For Netlify, a build hook or deploy notification. For uploads, the upload itself.
- Somewhere to keep versions for the team (Supabase), so they don't live only in one browser.

## Build order

1. **Show found versions** in the prototype's own order, with the info note. Done in designer-toolkit-code #38.
2. **The naming choice** at connect time, with the options above, and in Settings.
3. **Hearing about updates:** a new version per deploy or upload.
4. **Version history as its own page:** what changed between two versions, and who approved what. This needs its own plan.

## Open questions

- When a milestone has several rounds, should the Version menu group them by milestone?
- Should an earlier version stay viewable forever, or only for a set number of versions?

Sources: Sharon's Oct 19 direction; the Oct 14 decision on milestones ([Decisions](Decisions)).
