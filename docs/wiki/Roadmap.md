# Roadmap

**Last updated:** October 19, 2026

| Now | Next | Later |
|---|---|---|
| **Can one shell frame any prototype?** The toolbar on a written contract, with tests and a link for every state. Plus one Figma capture test, the riskiest bet. **Can a prototype fill the toolkit in?** Connect a prototype: link it, see what the toolkit found, and keep what fits. Connecting GitHub comes first. | **Can notes and versions live beside the prototype?** A details page on Supabase, notes from a shared link, a version per deploy, and every state sent to Figma. | **Does it hold up and read as mine?** Checks per state, the Fireside skin in Storybook, and hosting the BambooHR prototypes. |

## Milestones

Each milestone is one parent issue on the [project board](https://github.com/users/sharonlafleur1984/projects/7). Its steps are the sub-issues underneath it.

| Milestone | Done when | Timing |
|---|---|---|
| [Prototype shell](https://github.com/sharonlafleur1984/designer-toolkit/issues/21) | The toolbar switches version, persona and state through the contract, every state has its own link, the tests pass, and the shell uses the Fireside skin | Not set yet |
| [Connect a prototype](https://github.com/sharonlafleur1984/designer-toolkit/issues/57) | A linked prototype's pages, milestones and docs are in the toolkit within a few minutes, chosen on "Here's what I found", starting with [Connect GitHub](https://github.com/sharonlafleur1984/designer-toolkit/issues/58) | In progress. Connect GitHub needs the Supabase project and sign-in from Backend and sharing |
| [Send to Figma](https://github.com/sharonlafleur1984/designer-toolkit/issues/24) | Every state of one real prototype lands in Figma in one pass, light and dark | Not set yet |
| [Backend and sharing](https://github.com/sharonlafleur1984/designer-toolkit/issues/22) | Each prototype has a details page saved in Supabase, a note left on a shared Netlify link shows there, and every deploy adds a version | Not set yet |
| [Checks](https://github.com/sharonlafleur1984/designer-toolkit/issues/23) | Each state shows its automated WCAG 2.2 AA (Web Content Accessibility Guidelines, level AA) result and its heuristic score | Not set yet |
| [Host the BambooHR prototypes](https://github.com/sharonlafleur1984/designer-toolkit/issues/25) | The BambooHR prototypes run on a public Netlify link, with Fields used legally | Not set yet |

## What could go wrong

These are the few things that could sink the project, and each has a plan.

| If this happens... | ...then | So we're... |
|---|---|---|
| A client's confidential notes land in this public repo | Sharon breaks a client's trust (viability) | Keeping notes in Supabase behind sign-in, with access rules per project, and testing that outsiders read nothing |
| The Figma capture produces flat or broken frames | Clients still get redrawn screens, and the main payoff is gone (feasibility) | Testing one real prototype on the free tiers before paying for any tool |
| Netlify deletes old deploys after 30 days | Old version links break (feasibility) | Saving every version's link and notes in Supabase, not only on Netlify |

Where things live: [Project board](https://github.com/users/sharonlafleur1984/projects/7) · [Spec](Spec) · [Backlog](Backlog) · [Decisions](Decisions) · [Documents](Documents)
