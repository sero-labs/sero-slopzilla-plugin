# @sero-ai/plugin-slopzilla

SlopZilla — the kaiju-sized AI slop idea generator for Sero. Pick a complexity level and tech stack, generate outlandishly sloppy app ideas, pick your favourite, bookmark the best ones, and launch them directly into a Sero workspace.

## Sero Plugin Install

Install in **Sero → Admin → Plugins** with:

```text
git:https://github.com/monobyte/sero-slopzilla-plugin.git
```

Sero clones the source repo, installs its dependencies locally, builds the UI, and then hot-loads the plugin into the sidebar.

## Pi CLI Usage

Install as a Pi package:

```bash
pi install git:https://github.com/monobyte/sero-slopzilla-plugin.git
```

The agent gains a `slopzilla` tool and a `/slopzilla` command.

## Tools

### `slopzilla`

Query your SlopZilla history and saved ideas.

| Action    | Description                                             |
|-----------|---------------------------------------------------------|
| `history` | List previously launched ideas with build status        |
| `saved`   | List bookmarked ideas you haven't launched yet          |

## Commands

| Command      | Description                                   |
|--------------|-----------------------------------------------|
| `/slopzilla` | Show your SlopZilla history via the agent     |

## Sero Usage

When loaded in Sero, the web UI mounts in the main app area with a multi-phase workflow:

1. **Config** — choose complexity (`low`, `medium`, `high`) and optional technologies
2. **Generating** — the agent generates a batch of gloriously sloppy app ideas
3. **Picking** — browse and pick your favourite idea (or save it for later)
4. **Remix** — optionally tweak the chosen idea before launching
5. **Launching** — the idea is handed off to a new Sero workspace with a full build prompt
6. **History** — review all past launches and their build status

## State File

State is stored globally under `SERO_HOME` when running inside Sero:

```
~/.sero-ui/apps/slopzilla/state.json
```

When used as a standalone Pi package (outside Sero), state falls back to the workspace:

```
workspace-root/
└── .sero/
    └── apps/
        └── slopzilla/
            └── state.json
```

### State Shape

```json
{
  "phase": "config",
  "complexity": null,
  "technologies": [],
  "ideas": null,
  "chosenIdea": null,
  "launchedWorkspaceId": null,
  "launchedSessionId": null,
  "history": [],
  "savedIdeas": []
}
```

| Field                  | Type                | Description                             |
|------------------------|---------------------|-----------------------------------------|
| `phase`                | `Phase`             | Current workflow phase                  |
| `complexity`           | `low\|medium\|high` | Selected complexity level               |
| `technologies`         | `string[]`          | Selected tech stack tags                |
| `ideas`                | `AppIdea[] \| null` | Generated idea batch                    |
| `chosenIdea`           | `AppIdea \| null`   | Idea selected for launch                |
| `launchedWorkspaceId`  | `string \| null`    | ID of the workspace the idea was sent to|
| `history`              | `HistoryEntry[]`    | All previously launched ideas           |
| `savedIdeas`           | `SavedIdea[]`       | Bookmarked ideas awaiting launch        |

## Development

```bash
npm install
npm run build       # Produces dist/ui/remoteEntry.js
npm run typecheck   # Zero-error TypeScript check
```

## License

MIT
