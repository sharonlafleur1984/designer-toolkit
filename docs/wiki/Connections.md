# How everything connects

**Last updated:** October 14, 2026

- **GitHub holds everything.** Each repo has one job, like the toolkit's code, its docs, the design system or one prototype.
- **Netlify shows things.** Each Netlify site runs one repo's build at a public link. A site only shows what its build copies, so internal planning stays out.
- **Supabase remembers things.** It holds what people do in the toolkit (comments, notes, approvals, versions) behind a sign-in.
- **The toolkit ties them together.** It shows a prototype from its Netlify link and puts the planning beside it, read privately from GitHub and Supabase.
- **Keep this page true.** Anything that adds, changes or removes a Netlify site or the Supabase setup updates this page in the same pull request. See [Keeping this page up to date](#keeping-this-page-up-to-date).

## Who can see what

Each piece is public or private on purpose. This table is the one to check before putting anything new anywhere.

| Where | Who can see it | What belongs there |
|---|---|---|
| Your computer (localhost) | Only you | Anything. Prototypes run here while you work. |
| Private GitHub repos | Only you | Code, and internal planning: Jira links, problem statements, reviews, ideation |
| Public GitHub repos | Anyone | Docs and code with no client work, no real names and no secrets |
| Netlify sites | Anyone with the link, unless the site has a password | Only what a prototype needs to run |
| Supabase | You, plus reviewers you invite to comment | What people do in the toolkit |

## The repos

| Repo | Public or private | What it holds | Netlify site |
|---|---|---|---|
| [designer-toolkit](https://github.com/sharonlafleur1984/designer-toolkit) | Public | The toolkit's plan, decisions and this wiki | None |
| [designer-toolkit-code](https://github.com/sharonlafleur1984/designer-toolkit-code) | Private | The toolkit's code and its Supabase setup | None. The toolkit runs on your computer. |
| [design-system-skeleton](https://github.com/sharonlafleur1984/design-system-skeleton) | Public | Shared components, tokens and themes | [Design system Storybook](#design-system-storybook) |
| [summit-challenges](https://github.com/sharonlafleur1984/summit-challenges) | Private | The Summit Challenges prototype (it was Payroll Summit) | [Summit Challenges](#summit-challenges) |
| [client-portal](https://github.com/sharonlafleur1984/client-portal) | Private | The Client Portal prototype | [Client Portal](#client-portal) |
| [after-graduation](https://github.com/sharonlafleur1984/after-graduation) | Public | The After Graduation planner | [After Graduation](#after-graduation), not linked to this repo |
| [how-i-work](https://github.com/sharonlafleur1984/how-i-work) | Public | Your process, skills and starter templates | None |

## How Netlify works

Netlify takes a repo, runs its build, and puts the result at a link. Four things decide what a site does.

- **The build.** A `netlify.toml` file in the repo says which command builds the site and which folder to publish. The prototypes copy only what they need into a `dist` folder, so planning files never reach the site.
- **When it updates.** Every site here is linked to its repo's `main` branch, so **every merge to `main` publishes right away.** There is no "deploy only before a meeting" step yet.
- **Deploy previews.** Every pull request also gets its own public preview link, built from that branch. A preview publishes whatever the branch's build copies.
- **Old deploys.** Each deploy keeps its own link, even after a newer one goes live. Netlify deletes old deploys after 30 days on the free plan, or 90 on paid plans ([Netlify](https://docs.netlify.com/deploy/manage-deploys/manage-deploys-overview)).

Two rules follow from how the toolkit uses these sites:

- **No password on a prototype site.** A site behind a sign-in refuses to show inside another page, so it can't show in the toolkit.
- **The toolkit reads `prototype-config.json` from the site.** That file lists versions, personas and page states, and the site's `netlify.toml` lets other pages read it (a CORS header: cross-origin resource sharing).

You're signed in to the Netlify command-line tool on your computer. It lists sites with `netlify sites:list`.

## The Netlify sites

### Summit Challenges

- **Link:** https://summitchallenges.netlify.app/home
- **Built from:** [summit-challenges](https://github.com/sharonlafleur1984/summit-challenges), branch `main`
- **Updates:** on every merge to `main`, with a preview link for every pull request
- **Build:** `netlify.toml` copies the repo into `dist`, leaving out `home/project`, `home/prototype-details`, `home/toolkit-data.json` and `scripts/`. Those hold internal planning and Jira links.
- **Reads across sites:** `/home/prototype-config.json`
- **In the toolkit:** added by its link. Its planning (3 problems, 15 milestones, 30 page states) comes from `home/toolkit-data.json` in the private repo, not from this site.
- **Status, Oct 14:** Exposed. The `netlify.toml` above is waiting in [summit-challenges #5](https://github.com/sharonlafleur1984/summit-challenges/pull/5), and until it merges the site publishes the planning files.
- **After #5 merges:** earlier deploys and preview links still hold the planning files until they're deleted.

### Client Portal

- **Link:** https://brokerclientportal.netlify.app (opens the client list)
- **Built from:** [client-portal](https://github.com/sharonlafleur1984/client-portal), branch `main`
- **Updates:** on every merge to `main`, with a preview link for every pull request
- **Build:** `netlify.toml` copies `fabric-resources` and the `client-portal` folder into `dist`. It leaves out the docs, tests, `README.txt` and the `project` folder (internal planning with real names), except `project/version-history-seed.json`, which the prototype reads.
- **Reads across sites:** `/client-portal/prototype-config.json`
- **Redirect:** `/` goes to `/client-portal/?page=client-list`
- **Status, Oct 14:** Live

### Design system Storybook

- **Link:** https://designsystemskeleton.netlify.app
- **Built from:** [design-system-skeleton](https://github.com/sharonlafleur1984/design-system-skeleton), branch `main`
- **Updates:** on every merge to `main`. Every pull request gets a preview link, which the "Your turn" section links to.
- **Build:** `npm run build-storybook` on Node 22, publishing `storybook-static`
- **Status, Oct 14:** Live

### After Graduation

- **Link:** https://afterhighschool.netlify.app
- **Built from:** not the [after-graduation](https://github.com/sharonlafleur1984/after-graduation) repo. Netlify lists a copy it hosts itself as the source, so merging to that repo doesn't update this site.
- **Password:** yes, so it can't show inside the toolkit
- **Status, Oct 14:** Live, with a password

## How Supabase works

Supabase is the toolkit's database, sign-in and private file storage, in one project named "Designer-Toolkit" (US West). It was set up on Oct 12, 2026.

- **What it holds:**
  - the prototypes in the toolkit, including removed ones, which become Recently added
  - comments, with the reviewers invited to each prototype
  - documentation pages, with every earlier version
  - prototypes an AI asked to add, waiting for your yes
  - private files, like uploaded HTML prototypes and screenshots, in the `toolkit-files` storage
- **Who can read what:** access rules on every table (row-level security) let you see only your own rows. Reviewers see only the comments on prototypes they're invited to.
- **Sign-in:** by email link (a magic link), no password. Supabase's built-in email sender only sends a few emails an hour, so real reviewers need a custom sender.
- **Keys:** the toolkit's build holds only the publishable key, which is safe in a browser. The secret key never goes in a repo or a build.
- **Changes to the tables:** each change is a migration file in `supabase/migrations/` in [designer-toolkit-code](https://github.com/sharonlafleur1984/designer-toolkit-code), added by pull request.
- **Status, Oct 14:** set up, but the toolkit doesn't use it yet. It saves to the browser until sign-in is built.

## How a prototype gets into the toolkit

1. The prototype's repo builds a public Netlify site with nothing internal in it.
2. You add the prototype to the toolkit by its Netlify link, or its localhost link while you work.
3. The toolkit checks the link loads and can show in a frame before adding it.
4. Once GitHub is connected, the toolkit reads the planning (problems, milestones, pages and page states) from the private repo and saves it in Supabase.
5. You and invited reviewers see the live prototype with its planning beside it. Someone with only the Netlify link sees the prototype and nothing else.

Steps 1 to 3 work now. Step 4 is planned, and step 5 waits on it.

## Keeping this page up to date

Update this page in the same pull request as the change it describes.

- **A Netlify change updates its site's section.** That includes adding, removing or renaming a site, and any change to its `netlify.toml`, build, redirects or headers. Turning a password on or off counts too.
- **A Supabase change updates "How Supabase works."** That includes a new table, storage, sign-in setting or key.
- **Each section's status line gets a date** when it changes.
- The [how-i-work process](https://github.com/sharonlafleur1984/how-i-work/blob/main/process.md) and its `CLAUDE.md` template point here, so every repo that sets up a Netlify site knows to update this page.
