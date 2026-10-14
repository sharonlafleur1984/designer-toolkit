# Decisions

**Last updated:** October 14, 2026

Newest first.

<details>
<summary><b>Oct 14, 2026:</b> Collaborators are added by email in the toolkit, and can ask for access</summary>

- **Decided by:** Sharon
- **Decision:** each prototype has two groups, both added by email. People are managed in one place shown in two spots: a **Share** button in the toolbar, and **Settings → Prototypes → People**. Both show the same list and controls.
  - **Collaborators** see everything: documentation, notes and ideation, heuristic reviews and comments.
  - **Reviewers** see comments only.
- **How they get in:** an email with a sign-in link (a magic link). No password, and no GitHub account needed. The email they sign in with has to match the one they were added with.
- **Request access:** someone who signs in with an email that isn't on the list sees that they don't have access yet, with a Request access button. Sharon gets the request at the top of Share (and People), and approving it sends them a sign-in link.
- **Who sees what there:** only the owner can add or remove people and answer requests. Collaborators see the list, with a note that only the owner can add people. Reviewers don't see Share or People. Supabase's access rules enforce this too, so hiding the controls isn't the only lock.
- **Saved in Supabase:** the lists live in the database, so code updates and new deploys never change them.
- **GitHub:** the toolkit can fill the collaborator list from a linked repo's collaborators when their emails are visible, but the toolkit's list decides access.
- **Every private page says so at the top:** "Private to you and this prototype's collaborators." A prototype with no collaborators says "Private to you."
- **Why:** collaborators may never make a GitHub account, and GitHub usually hides people's emails, so GitHub can't reliably say who's who. An email list that Sharon controls can.
- **Other options:** reading access from GitHub repo collaborators (misses anyone without an account); sign in with GitHub only (shuts out people without an account).
- **Changes:** the Oct 12 decision that only comments are shared. Reviewers still see only comments, and collaborators are a new, wider group.

</details>

<details>
<summary><b>Oct 13, 2026:</b> States in Figma use Figma's frames and Figma's comments</summary>

- **Decided by:** Sharon
- **Decision:** a prototype can be linked to a Figma file. A state that's in Figma shows its Figma frame, and its comments are Figma's comments, so one thread shows up in both places. A state that isn't in Figma yet keeps the toolkit's own screenshot and comments, and its open comments move to Figma when the state does.
- **Why:** Figma is where finished states go anyway, and stakeholders already review there. Two comment systems for the same screen would split the conversation.
- **How it syncs:** comments sync both ways. Figma edits show up in the toolkit on the next refresh. Code changes reach Figma only when Sharon sends states, on a deploy or by a button, so designer edits made in Figma never get overwritten.
- **Changes:** the Oct 12 decision on reviewer comments. For states in Figma, reviewers comment with their own Figma accounts, and Sharon lets them know. The email invite and magic link still cover states not yet in Figma.
- **Watch for:** Figma's comment notifications don't include the pin position, so the toolkit fetches each new comment after it's notified ([Figma forum](https://forum.figma.com/ask-the-community-7/enhancement-request-include-client-meta-positioning-information-to-comment-webhook-28245)). Comment reads and writes go through [Figma's comments API](https://developers.figma.com/docs/rest-api/comments-endpoints/), which limits how often it can be called.

</details>

<details>
<summary><b>Oct 12, 2026:</b> The skin is Fireside, and the shell is always dark</summary>

- **Decided by:** Sharon
- **Decision:** the toolkit uses Sharon's Fireside palette, and the shell is always dark. Reading surfaces, like the Documentation tab, can switch to light.
- **Colors and their jobs:** rust is the one accent, with bright rust #D06C3E for buttons. Fire red means danger, lake green success, and honey a warning. Details on [Skin](Skin).
- **Why:** a warm, calm frame, like a cabin at dusk, that keeps the prototype the brightest thing on screen. Bright rust outranks the honey warning, and it stays distinct from fire red for people with red-green color blindness.
- **Other options:** a blue or violet accent, which felt cold. A gold accent. Warnings as a second fire red, which is hard to tell apart from danger.
- **Replaces:** the Oct 12 decision that the skin is quiet neutral, in light and dark.

</details>

<details>
<summary><b>Oct 12, 2026:</b> Every change goes through a pull request, and main is protected</summary>

- **Decided by:** Sharon
- **Decision:** work in `designer-toolkit-code` happens on a branch and lands through a pull request. A "Protect main" rule set blocks direct pushes, deleting `main` and rewriting its history.
- **Why:** checks run before anything lands, and each pull request explains the change in plain language. Sharon checks changes on her own computer before merging. Only bundles get a Netlify site, when one is sent.
- **Other options:** committing straight to `main`. That keeps history and undo, but nothing gets checked or previewed first.

</details>

<details>
<summary><b>Oct 12, 2026:</b> Reviewers comment by email invite and sign in with a magic link</summary>

- **Decided by:** Sharon
- **Decision:** comments are the one shared space. Sharon invites reviewers by email, one prototype at a time, and they sign in with a link sent to that email. Everything else in the toolkit is Sharon's alone.
- **Why:** every comment has a real name, and only invited people see what others wrote.
- **Other options:** anyone with the link leaves a comment after typing a name. Names can't be trusted, and anyone who gets the link reads every comment.
- **Watch for:** Supabase's built-in email sender is for testing and sends only a few emails an hour. Real reviewers need a custom email sender.

</details>

<details>
<summary><b>Oct 12, 2026:</b> Supabase for now, behind a layer that can be swapped</summary>

- **Decided by:** Sharon
- **Decision:** the toolkit is for Sharon alone for now, with its data in Supabase. All reads and writes go through one storage layer in the code, so a future backend is a new adapter, not a rewrite.
- **Why:** if the toolkit becomes a product, it would likely move to AWS (Amazon Web Services) under a business account. Sharon doesn't want to host other people's data on a personal account.
- **Builds on:** the Oct 12 decision that Supabase is the backend.

</details>

<details>
<summary><b>Oct 12, 2026:</b> A deploy ships the prototypes added at the time, frozen</summary>

- **Decided by:** Sharon
- **Decision:** whatever prototypes are in the toolkit when it deploys are the ones that ship, like an export. To leave one out of a deploy, remove it first. Removed prototypes stay under Recently added.
- **Why:** what people review is exactly what was sent. It matches the decision that a version is one Netlify deploy.

</details>

<details>
<summary><b>Oct 12, 2026:</b> Each prototype has its own everything</summary>

- **Decided by:** Sharon
- **Decision:** each prototype has its own documentation, comments, ideas, copy, checks and versions. Nothing is shared between prototypes.
- **Why:** context sits one click from the screens it's about.
- **Other options:** one toolkit-wide wiki with a folder per prototype.

</details>

<details>
<summary><b>Oct 12, 2026:</b> The toolkit repos never hold a prototype</summary>

- **Decided by:** Sharon
- **Decision:** a prototype's code, config, data and bugs live in that prototype's own repo. All toolkit documentation lives in this repo, and `designer-toolkit-code` holds only the shell's code. The toolkit starts empty, and prototypes are added by link or HTML file, each with a nickname.
- **Why:** the toolkit frames any prototype, the way Storybook can load any library, so nothing about one prototype belongs inside it.
- **Replaces:** the old compiled Payroll Summit build in `designer-toolkit-code`, now removed. It lives on in the `payroll-summit` repo.

</details>

<details>
<summary><b>Oct 12, 2026:</b> Supabase is the backend</summary>

- **Decided by:** Sharon
- **Decision:** notes, ideas, comments, copy, checks and versions save to Supabase.
- **Why:** a Netlify link can't save anything by itself. With Supabase, people leave notes on the shared link and they show up in the toolkit.
- **Other options:** JSON files in each prototype's repo. Those can't take notes from a shared link.

</details>

<details>
<summary><b>Oct 12, 2026:</b> The toolkit is a working tool; finished states go to Figma</summary>

- **Decided by:** Sharon
- **Decision:** the toolkit is where Sharon prototypes and collaborates. When work is done, every state the prototype shows becomes a Figma frame, because clients want Figma files. The toolkit itself is never sent.
- **Why:** coded prototypes are faster to work in, but clients review and keep work in Figma.
- **Other options:** a PDF handoff pack or a shareable web page as the final deliverable. Neither gives clients editable files.

</details>

<details>
<summary><b>Oct 12, 2026:</b> A version is one Netlify deploy</summary>

- **Decided by:** Sharon
- **Decision:** work stays on Sharon's computer and GitHub. She deploys to Netlify only before a meeting or a share, and each deploy becomes a version with the notes since the last one.
- **Why:** versions then match exactly what people reviewed.
- **Other options:** every saved change as a version (too many to show anyone), or a manual "save version" button.
- **Watch for:** Netlify deletes old deploys after 30 days, or 90 on paid plans ([Netlify](https://docs.netlify.com/deploy/manage-deploys/manage-deploys-overview)). Each version's link and notes are also saved in Supabase.

</details>

<details>
<summary><b>Oct 12, 2026:</b> Notes and ideas live on each prototype's details page</summary>

- **Decided by:** Sharon
- **Decision:** notes, ideas, copy and docs for a prototype are kept on its details page inside the toolkit. That's how the original toolkit worked.
- **Why:** context sits one click from the screens it's about.
- **Other options:** the wiki plus FigJam, or Notion. Both sit apart from the screens.

</details>

<details>
<summary><b>Oct 12, 2026:</b> Heuristic checks use Nielsen's 10 plus WCAG 2.2 AA (Web Content Accessibility Guidelines, level AA)</summary>

- **Decided by:** Sharon
- **Decision:** each state gets a scored checklist of Nielsen's 10 usability heuristics and automated WCAG 2.2 AA checks.
- **Why:** usability and accessibility both, with the automated part running on its own.
- **Other options:** Nielsen's 10 only (misses accessibility), or a custom checklist.

</details>

<details>
<summary><b>Oct 12, 2026:</b> The skin is quiet neutral, in light and dark (replaced)</summary>

- **Decided by:** Sharon
- **Decision:** grayscale chrome with one accent, thin borders and lots of space, so the prototype is the only colorful thing on screen. Details on [Skin](Skin).
- **Why:** the toolkit must never pull attention from the prototype.
- **Other options:** pure monochrome (hard to show what's selected), or warm neutral (can shift how a prototype's colors look).
- **Replaced by:** the Oct 12 decision that the skin is Fireside, and the shell is always dark.

</details>

<details>
<summary><b>Oct 12, 2026:</b> BambooHR prototypes are shown publicly; the code stays private</summary>

- **Decided by:** Sharon
- **Decision:** the BambooHR prototypes are public Netlify links with no password. Planning, docs and links live in this public repo. The code stays in the private `designer-toolkit-code` repo so nobody takes it.
- **Why:** this is Sharon's portfolio. The work is already released, or is ideation the team won't build now that the department is gone.
- **Replaces:** the Oct 11 rule that no BambooHR content ever lands in a public repo.
- **Still never public:** former coworkers' personal data, like names, emails and Slack IDs.

</details>

<details>
<summary><b>Oct 12, 2026:</b> Client planning stays in the client's own repo</summary>

- **Decided by:** Sharon
- **Decision:** a client project's planning lives in that project's repo. This repo holds only the toolkit's own planning.
- **Why:** client plans are confidential, and this repo is public.

</details>

<details>
<summary><b>Oct 11, 2026:</b> The shell lives in a new public repo; the code stays private</summary>

- **Decided by:** Sharon
- **Decision:** the shell and this wiki get a new public repo. The original toolkit build and both prototypes stay in private repos.
- **Why:** the original repo's history holds BambooHR's internal data. A new repo starts clean, with nothing to scrub.
- **Other options:** strip the original repo, rewrite its history and make it public. One missed file would leak internal data.

</details>

<details>
<summary><b>Oct 11, 2026:</b> The shell gets Sharon's own design system; the prototypes keep their original look</summary>

- **Decided by:** Sharon
- **Decision:** the toolbar and panels are built from Sharon's design system. The prototypes inside stay as they were.
- **Why:** the shell is the part that's Sharon's own work. The prototypes are work samples, so they should look like the product they came from.
- **Other options:** building a separate design system from screenshots of styles she likes. Her existing system already plans a toolkit theme.

</details>

<details>
<summary><b>Oct 11, 2026:</b> Fields is replaced with a free lookalike</summary>

- **Decided by:** Sharon
- **Decision:** the prototypes stop using Fields, BambooHR's own typeface, and use a free font that looks close.
- **Why:** Fields is licensed to BambooHR and shouldn't ship in Sharon's repos.
- **Next:** pick the font from a side-by-side comparison.

</details>

<details>
<summary><b>Oct 11, 2026:</b> Icons come from Font Awesome Free, bundled in the repo</summary>

- **Decided by:** Sharon
- **Decision:** every icon is a local file from [Font Awesome Free](https://fontawesome.com/download). About 70 icons that only exist in the paid set get the closest free stand-in.
- **Why:** the build loaded icons from BambooHR's servers. That can stop working any day, and those icons are licensed to BambooHR.
- **Other options:** keep loading from BambooHR's servers.

</details>

<details>
<summary><b>Oct 11, 2026:</b> Make the toolkit run first, then turn it into a shell for existing prototypes</summary>

- **Decided by:** Sharon
- **Decision:** get the original build running and looking right, then use it to frame the client portal and current product prototypes.
- **Why:** a working shell around real prototypes shows developer handoff in action.
- **Other options:** recovering clean source code first. The recovered code has machine-made names, so that's a rebuild either way.

</details>
