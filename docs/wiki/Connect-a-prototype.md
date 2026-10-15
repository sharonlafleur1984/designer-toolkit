# Connect a prototype

Last updated: Oct 15, 2026

- **What it is:** the first time someone links a prototype's repo, the toolkit reads it and shows what it found to fill itself in.
- **The rule:** it suggests and never converts. Each finding is Use it, Change it or Skip, and changes to the prototype's own repo come as a pull request its owner approves.
- **First:** the GitHub connection, because the toolkit can't read a private repo without it.

## The problem

A designer links a prototype, and the toolkit stays mostly empty. Its pages, states, personas, milestones and docs already exist in the repo, often organized for another tool. Retyping them is slow, and guessing at them breaks trust.

It works when a linked prototype has its pages, milestones and docs in the toolkit within a few minutes. Nothing changes that its owner didn't choose.

## How it works

1. **Connect GitHub.** This happens the first time someone imports from GitHub, not at sign-in. People without GitHub never see it.
2. **Pick the repo** from your list of repos, with a search box.
3. **The toolkit reads the repo.** This takes a few seconds, and the toolkit shows its progress while it reads.
4. **"Here's what I found."** One screen lists each finding: what it is, where it was found, and how sure the toolkit is.
5. **You decide each one:** Use it, Change it or Skip.
6. **Only then does the toolkit fill in.** Anything that needs a change in the prototype's repo becomes a pull request there.

## What the toolkit looks for

| To fill in | What it looks for | If nothing turns up |
|---|---|---|
| The live prototype | A deploy link (Netlify or another host) | Asks for the link |
| Pages | Routes and page files | Lists the pages it found, for you to confirm |
| Page states | Sample data, a state setting in the link (like `?state=empty`), a fixtures folder | Suggests adding a small state switch, as a pull request |
| Personas, context and login states | Test users, roles, flags like first login or expired | Starts Scenarios with templates |
| Milestones | GitHub milestones and spec files | Offers Add milestone |
| Documentation | The wiki and a `docs/` folder | Starts with Project overview |
| Versions | Tags, releases and deploy history | Shows one version |

## Matching what people already have

People often arrive with a setup from another prototype tool. The toolkit recognizes that setup and suggests how it fits.

| Setup from another tool | Suggestion |
|---|---|
| Storybook stories for screens | "These 14 stories look like page states. Use them?" |
| Mock data or test users | "These 3 users look like personas. Add them to Scenarios?" |
| Flags like first login or expired account | "These look like login states. Add them?" |
| Their own docs folders | "Your Research folder fits Research. Your Specs look like Milestones." |
| Another tool's settings file | Maps its words to ours, and shows what's different |
| Something with no match | Keeps it as is, under its own name |

Each suggestion shows how sure the match is. A weak match is still offered, and marked as a guess.

## The "Here's what I found" screen

- One row per finding: what, where (a file or link), and how sure.
- Every row offers **Use it**, **Change it** and Skip.
- Change it opens the row to edit before it's used.
- **Use all suggestions** for when everything looks right. It still lists what it will do before it does it.
- Nothing is saved until you choose. Leaving the screen keeps what's already in the toolkit as it was.
- The screen can be opened again later from Settings, for example after the prototype's repo changes.

## What it needs first

- **The GitHub connection.** The key for reading private repos is stored on the server side (Supabase), never in the browser.
- **Your yes** before any change to a prototype's repo.

## Build order

Each step is its own pull request, in this order:

1. **Connect GitHub:** the first time someone imports, plus Disconnect in Settings.
2. **The repo list:** Import from GitHub shows your repos to pick from, instead of a pasted link.
3. **The reader:** reads the repo on the server and turns what it finds into findings, each with where it was found and how sure.
4. **"Here's what I found":** the screen with Use it, Change it and Skip. It fills in the toolkit only.
5. **Matching other setups:** Storybook stories, mock users, flags and docs folders, one at a time.
6. **Changes in the prototype's repo:** like adding a state switch, as a pull request its owner approves.

## Open questions

- How sure should the toolkit be before it checks a suggestion for you? Or should nothing ever start checked?
- When the prototype's repo changes later, should the toolkit offer new findings, or wait until someone asks?

Sources: the Oct 14 decision on milestones ([Decisions](Decisions)), and Sharon's Oct 15 direction: "make suggestions, don't just do it."
