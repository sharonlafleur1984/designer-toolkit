# Backlog

**Last updated:** October 12, 2026

Every idea not on the [Roadmap](Roadmap). Nothing here is planned until it's decided.

<details>
<summary><b>Decided</b> (none yet)</summary>

N/A. Nothing has moved off the bench yet.

</details>

<details open>
<summary><b>Ideas</b></summary>

| # | Problem | Recommendation | Status |
|---|---|---|---|
| 1 | Figma frames from screen captures aren't real components | Sync Storybook to Figma as components with story.to.design, once a client needs a Figma library | Researched: ready for you |
| 2 | One evaluator finds only about a third of usability problems | Add a second heuristic pass by AI, labeled as a suggestion | Needs research |
| 3 | Reviewers can't leave feedback on a version without Figma | Turn on Netlify's feedback drawer for branch deploys | Needs research |
| 4 | Small visual changes slip through between versions | Add visual snapshots per story with Chromatic's free tier | Researched: ready for you |
| 5 | Some people want one file they can keep, not a link | Export a PDF of every state from Figma | Needs research |

<details>
<summary>1. Real Figma components from Storybook</summary>

- **Problem:** screen captures land as frames, not reusable Figma components with variants.
- **Options:** story.to.design (about $149 a month), Figma's `use_figma` tool (free in beta, paid later), or keep frames only.
- **Evidence:** story.to.design makes native components with variants from story args ([story.to.design](https://story.to.design/)). Pricing: [paid plans](https://story.to.design/docs/paid-plans).
- **Recommendation:** wait until a client asks for a component library in Figma.

</details>

<details>
<summary>2. An AI second pass on heuristics</summary>

- **Problem:** a single evaluator finds about 35% of problems, and NN/g (Nielsen Norman Group) recommends 3 to 5 evaluators ([NN/g](https://www.nngroup.com/articles/how-to-conduct-a-heuristic-evaluation/theory-heuristic-evaluations/)).
- **Options:** an AI pass that suggests scores Sharon overwrites, a peer reviewer, or user tests on anything scored 3 or 4.
- **Recommendation:** research how well an AI pass agrees with a human one before trusting it.

</details>

<details>
<summary>3. Feedback on a deploy</summary>

- **Problem:** people without Figma have nowhere to comment on a version.
- **Evidence:** Netlify's drawer works on deploy previews and branch deploys, not on permanent deploy links ([Netlify](https://docs.netlify.com/deploy/review-deploys/netlify-drawer-for-feedback/overview)).
- **Recommendation:** check which Netlify plan includes it before deciding.

</details>

<details>
<summary>4. Visual snapshots between versions</summary>

- **Problem:** a small visual change can slip into a version unnoticed.
- **Evidence:** Chromatic is free up to 5,000 snapshots a month ([Chromatic](https://www.chromatic.com/docs/faq/free-plan-snapshot-limit)).
- **Recommendation:** add it when the shell components are in Storybook, not before.

</details>

<details>
<summary>5. A PDF of every state</summary>

- **Problem:** some reviewers want one file to keep.
- **Options:** export frames from Figma to PDF, or print each state link to PDF.
- **Recommendation:** only if a client asks. Figma is the deliverable.

</details>

</details>
