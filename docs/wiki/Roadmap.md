# Roadmap

**Last updated:** October 11, 2026

| Now | Next | Later |
|---|---|---|
| **Does it run on its own?** Every page renders with nothing loaded from BambooHR's servers. | **Can one shell frame every prototype?** A rebuilt toolbar drives the client portal and the current product prototype. | **Does it read as Sharon's?** The shell becomes a third theme in the design system, in Storybook. |

## Milestones

| Milestone | Done when | Timing |
|---|---|---|
| Runs on its own | Every page and persona renders with zero requests to BambooHR's servers | Not set yet |
| Shell rebuilt | The toolbar switches version, persona and page state through the existing message contract, with tests | Not set yet |
| Both prototypes in the shell | The client portal and the current product prototype both respond to the toolbar | Not set yet |
| Shell theme in Storybook | Every shell component passes the Storybook gate in the toolkit theme | Not set yet |

## What could go wrong

These are the few things that could sink the project, and each has a plan.

| If this happens... | ...then | So we're... |
|---|---|---|
| BambooHR's internal data lands in a public repo | Sharon breaks a former employer's trust (viability) | Keeping the BambooHR source in private repos. Public repos hold only Sharon's shell and sample data. |
| The rebuilt shell drifts from the message contract | Prototypes stop answering the toolbar (feasibility) | Testing every toolbar control against the contract with Playwright |
| Viewers can't tell what the toolbar does | The piece fails at its one job (usability) | Running 3 short sessions with first-time viewers before calling it done |

Where things live: [Spec](Spec) · [Decisions](Decisions) · [Documents](Documents)
