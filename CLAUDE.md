# CLAUDE.md

Start here. This file tells Claude (and any developer) where everything lives, so only the needed file gets opened.

## What this is

Designer toolkit: Sharon's workspace for coded prototypes. It frames any prototype, switches its version, persona and state, and keeps every note, idea, copy decision, check and version beside it. Finished states go to Figma.

## Rules

- **How Sharon works:** follow [how-i-work](https://github.com/sharonlafleur1984/how-i-work) for the process and skills.
- **This repo is public.** It holds planning, docs and links only. Code lives in the private `designer-toolkit-code` repo.
- **No personal data, ever.** Not former coworkers' names, emails or Slack IDs, and no real user data. Sample data only.
- **No client work here.** A client project's planning lives in that project's own repo. Notes, copy and comments live in Supabase behind sign-in.
- **Never commit a Supabase secret key.** Only the publishable key goes in the build.
- **Every fact needs a source link,** or a label saying it's an estimate.
- **Ask before changing or deleting anything.** A recommendation is not approval.
- **Wiki pages are edited in `docs/wiki/`,** never in the GitHub Wiki tab.
- **Changing a Netlify site or Supabase, in any repo?** Update [`docs/wiki/Connections.md`](docs/wiki/Connections.md) in a pull request at the same time.
- **Every commit names its Claude session.** End each commit message with `Claude-Session:` and the link to the session that made it. That way any branch can be traced back to where the work happened.
- **Finish with a pull request.** Pushed work always gets one, even when it's small. A branch with no pull request looks abandoned.

## Where everything is

Start with [`docs/wiki/Documents.md`](docs/wiki/Documents.md): every document in this repo and when to open it. When you add or remove a document, update its row there and in the private Notion index in the same pass.

## Skills to use

- `product-manager` for roadmap, backlog and status
- `product-designer` for design, page structure and the component library
- `ux-writer` for any words people will read, with [`docs/voice.md`](docs/voice.md) for this project's voice
- `product-engineer` for any code work
- `spec-writer` for the spec
- `working-with-sharon` for how to write to Sharon

## Outside the repo

- Code: the private `designer-toolkit-code` repo
- Backend: Supabase (project not created yet)
- Project entry: Notion, Projects, "Designer toolkit"
- Visual ideas: [FigJam board](https://www.figma.com/board/62L8u38vabqutND1Cx8ZpD)
- Design source: Figma, Life Hub Library
- Screens to look at and edit: the [Designer Toolkit canvas](https://claude.ai/artifact/ChthBXbHNZ1rsqmqc8RfZZ) on claude.ai (private to Sharon)
