# Designer toolkit

Updated October 19, 2026

The Designer Toolkit is a quiet place for coded prototypes. It frames any prototype and keeps everything about it close: every version, persona and page state one click apart, with the notes, ideas, copy decisions and checks right beside it.

It wears [Lantern](https://github.com/sharonlafleur1984/lantern-design-system)'s Fireside theme, so the frame stays calm and the prototype is the brightest thing on the page.

> **This is a work in progress.** You can follow along in the [wiki](https://github.com/sharonlafleur1984/designer-toolkit/wiki), messy parts included.

## What it does

Every part has one of four statuses, the same ones Lantern uses.

- **Ready:** in the code on `main`.
- **Pending:** built, and waiting in a pull request.
- **On hold:** planned, waiting until a prototype needs it.
- **Not started:** planned, nothing built yet.

| Part | Status | What it does |
| --- | --- | --- |
| Frame a prototype | `Ready` | Shows any prototype, from a link or an HTML file, with its milestones, versions and page states in the sidebar. |
| Add a prototype | `Ready` | Takes a short nickname and a link or an HTML file. |
| Here's what I found | `Ready` | Reads what a prototype already describes about itself, like its personas, login states and versions, and lets you keep, edit or ignore each one. |
| Documentation | `Ready` | Holds the project spec, a spec for each milestone, and your own documents, beside the prototype. |
| Scenarios | `Pending` | Lists every persona, login state and context, and where each one came from. |
| Notes and ideation | `Not started` | Keeps links and notes for each milestone. |
| Heuristic review | `Not started` | Scores each milestone against usability heuristics. |
| Comments from a shared link | `Not started` | Lets invited reviewers comment on a shared link, and shows their comments here. |
| Version history | `Not started` | Shows what changed in each version. |
| Send to Figma | `Not started` | Sends every page state to Figma in one pass. |

## How it works

1. Each prototype lives in its own repo and on its own Netlify site.
2. The toolkit frames it and reads its `prototype-config.json`, the contract that names its versions, personas and page states.
3. Notes, comments and versions are saved in Supabase, behind sign-in.
4. Finished page states go to Figma.

How the pieces connect: [Connections](https://github.com/sharonlafleur1984/designer-toolkit/wiki/Connections).

## Where things are

- **The plan and docs:** this repo and its [wiki](https://github.com/sharonlafleur1984/designer-toolkit/wiki), with the Dashboard, Roadmap, Spec and Decisions
- **The code:** the private `designer-toolkit-code` repo
- **The look:** [Lantern](https://github.com/sharonlafleur1984/lantern-design-system), Fireside theme
- **How it sounds:** [docs/voice.md](docs/voice.md)

Part of [how Sharon works](https://github.com/sharonlafleur1984/how-i-work).
