# Connect a prototype

Last updated: Oct 19, 2026

- **What it is:** the first time someone links a prototype's repo, the toolkit reads it and shows what it found to fill itself in.
- **The rule:** it suggests and never converts. Each finding is Keep, Edit or Ignore, and changes to the prototype's own repo come as a pull request its owner approves.
- **First:** the GitHub connection, because the toolkit can't read a private repo without it.

## The problem

A designer links a prototype, and the toolkit stays mostly empty. Its pages, states, personas, milestones and docs already exist in the repo, often organized for another tool. Retyping them is slow, and guessing at them breaks trust.

It works when a linked prototype has its pages, milestones and docs in the toolkit within a few minutes. Nothing changes that its owner didn't choose.

## How it works

1. **Connect GitHub.** This happens the first time the toolkit needs a repo it can't read, not at sign-in. People without GitHub never see it. See [Connecting GitHub](#connecting-github).
2. **Pick the repo** from your list of repos, with a search box. The toolkit suggests the repo the Netlify site was built from.
3. **The toolkit reads the repo.** This takes a few seconds, and the toolkit shows its progress while it reads.
4. **"Here's what I found."** One screen lists each finding: what it is, where it was found, and how sure the toolkit is.
5. **You decide each one:** Keep, Edit or Ignore.
6. **Only then does the toolkit fill in.** Anything that needs a change in the prototype's repo becomes a pull request there.

## Connecting GitHub

The toolkit asks GitHub for access the way Netlify and Vercel do, so nobody ever sees or pastes a token.

**The problem:** a designer linking a private prototype repo hits a dead end, because the toolkit needs access it can't ask for. It's solved when they can link a private repo in under a minute, without leaving the toolkit or editing a file.

1. **Ask at the moment of need.** When a repo can't be read, the error becomes a next step: "client-portal is private. Connect GitHub so the toolkit can read it." with **Connect GitHub** and Cancel.
2. **GitHub handles the permission.** GitHub's own screen opens, with only that repo selected and read-only access.
3. **Come back to the same spot, already linked.** "Here's what I found" opens once the toolkit has read the repo.
4. **Pick, don't type, from then on.** Link a repo shows a searchable list of the repos the toolkit can see, with the Netlify site's repo suggested first.
5. **One place to manage it.** Settings gets a Connections section: "Connected as sharonlafleur1984 · 2 repos", with Manage on GitHub and Disconnect.

| When this happens | The person sees |
|---|---|
| They cancel on GitHub | "Not connected. The toolkit can't read client-portal until GitHub allows it." with **Try again** |
| The repo wasn't included | "GitHub hasn't shared client-portal with the toolkit." with **Add it on GitHub** |
| An organization's repo needs an admin's OK | "Waiting for your GitHub admin to approve." The toolkit checks again on its own. |

| Option | Verdict |
|---|---|
| **GitHub App (recommended)** | Read-only, limited to the repos you choose, and it doesn't expire. People know the pattern from Netlify and Vercel. |
| Sign in with GitHub (OAuth app) | Simpler to build, but it asks for every repo the person has. |
| Paste a token | Leaves the toolkit, confuses scopes, and expires without warning. |

- **What it needs:** a Netlify function for GitHub's callback, and a Supabase row that keeps the installation. The access stays on the server, never in the browser.
- **Until it's built:** the toolkit runs locally with `GITHUB_TOKEN` in `.env` (the output of `gh auth token`). The error for a private repo should say that, instead of a dead end.

## What the toolkit looks for

- **Every file, not known places.** A vibecoding agent may have put notes, plans and scenarios anywhere.
- **By what's in it.** The toolkit recognizes a file by its contents, not its name or folder.
- **Everything shows.** The toolkit is invite-only, so it's already private. Hiding things by default only loses information.


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
- Every row starts on Keep, with Edit and Ignore beside it.
- Edit opens the row to rename it before it's kept.
- **Add to the toolkit** adds them in one step. A count list above it says what it will add and what's ignored.
- Nothing is saved until you choose. Leaving the screen keeps what's already in the toolkit as it was.
- The screen can be opened again later from Settings, for example after the prototype's repo changes.

## What it needs first

- **The GitHub connection,** as described in [Connecting GitHub](#connecting-github).
- **Your yes** before any change to a prototype's repo.

## Build order

Each step is its own pull request, in this order:

1. **Connect GitHub:** the GitHub App, the Connect GitHub step where a repo can't be read, and Connections in Settings ([#58](https://github.com/sharonlafleur1984/designer-toolkit/issues/58)).
2. **The repo list:** Import from GitHub shows your repos to pick from, instead of a pasted link.
3. **The reader:** reads the repo on the server and turns what it finds into findings, each with where it was found and how sure.
4. **"Here's what I found":** the screen with Use it, Change it and Skip. It fills in the toolkit only.
5. **Matching other setups:** Storybook stories, mock users, flags and docs folders, one at a time.
6. **Changes in the prototype's repo:** like adding a state switch, as a pull request its owner approves.

## Open questions

- How sure should the toolkit be before it checks a suggestion for you? Or should nothing ever start checked?
- When the prototype's repo changes later, should the toolkit offer new findings, or wait until someone asks?

Sources: Sharon's Oct 19 direction to read every file and show everything found, the Oct 14 decision on milestones ([Decisions](Decisions)), and Sharon's Oct 15 direction: "make suggestions, don't just do it."
