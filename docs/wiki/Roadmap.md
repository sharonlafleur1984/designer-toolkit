# Roadmap

**Last updated:** October 12, 2026

| Now | Next | Later |
|---|---|---|
| **Can one shell frame any prototype?** A rebuilt toolbar and a details page for notes, ideas, copy and docs. | **Can a finished state reach Figma without redrawing?** Every state captured to Figma, and every deploy saved as a version. | **Does it read as mine and hold up?** The quiet skin in Storybook, plus heuristic and accessibility checks per state. |

## Milestones

| Milestone | Done when | Timing |
|---|---|---|
| Runs on its own | Every page renders with zero requests to BambooHR's servers | Not set yet |
| Shell rebuilt | The toolbar switches version, persona and page state through the existing message contract, with tests | Not set yet |
| Details page | Each prototype has a details page with notes, ideas, copy and docs, saved in Supabase | Not set yet |
| Notes from the shared link | A note left on a Netlify link shows on the details page | Not set yet |
| Versions from deploys | Every Netlify deploy adds a version entry with its link and the notes since the last one | Not set yet |
| States to Figma | Every state of one real prototype lands in Figma in one pass, light and dark | Not set yet |
| Checks per state | Each state shows its automated WCAG 2.2 AA (Web Content Accessibility Guidelines, level AA) result and its heuristic score | Not set yet |
| Quiet skin in Storybook | Every shell component passes the Storybook gate in the toolkit theme, light and dark | Not set yet |

## What could go wrong

These are the few things that could sink the project, and each has a plan.

| If this happens... | ...then | So we're... |
|---|---|---|
| A client's confidential notes land in this public repo | Sharon breaks a client's trust (viability) | Keeping notes in Supabase behind sign-in, with access rules per project, and testing that outsiders read nothing |
| The Figma capture produces flat or broken frames | Clients still get redrawn screens, and the main payoff is gone (feasibility) | Testing one real prototype on the free tiers before paying for any tool |
| Netlify deletes old deploys after 30 days | Old version links break (feasibility) | Saving every version's link and notes in Supabase, not only on Netlify |

Where things live: [Spec](Spec) · [Backlog](Backlog) · [Decisions](Decisions) · [Documents](Documents)
