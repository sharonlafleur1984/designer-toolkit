# Decisions

**Last updated:** October 11, 2026

Newest first.

<details>
<summary><b>Oct 11, 2026:</b> The shell lives in a new public repo; BambooHR source stays private</summary>

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
