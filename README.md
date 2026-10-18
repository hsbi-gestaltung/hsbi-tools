# HSBI Tools

A collection of useful tools, websites and resources used at the design faculty of HSBI (Hochschule Bielefeld), for students and staff alike.

Built with [Astro](https://astro.build) as a static site.

## Adding a tool

Anyone can suggest a tool through the [submission form](https://github.com/hsbi-gestaltung/hsbi-tools/issues/new?template=tool-submission.yml). Submitting it opens an issue, and a workflow turns that issue into a draft pull request with a new file in `src/content/tools/`. Once a maintainer reviews and merges the PR, the tool goes live with the next build.

Tools can also be added by hand: create a Markdown file in `src/content/tools/` with the frontmatter defined in `src/content.config.ts`.

## Automation

| Workflow | Trigger | What it does |
| :-- | :-- | :-- |
| `tool-submission.yml` | Issue with the `tool-submission` label opened or edited | Creates or updates the draft PR for the tool |
| `check-status.yml` | Push to `main`, Mon + Thu 08:00 UTC, manual | Checks each tool's URL, takes missing screenshots, commits the results to `main` |
| `deploy.yml` | After `check-status.yml` succeeds, manual | Builds the site and stores `dist/` as a workflow artifact (the upload to the server is not set up yet) |

Tools marked `internal: true` are only reachable from the HSBI network, so their status check is skipped and their screenshot has to be committed by hand.

The "zuletzt aktualisiert" date in the header is the time of the last change to `src/content/tools/` on `main`, i.e. the last merged tool PR.

## Development

Requires Node.js 22.12 or newer.

| Command | Action |
| :-- | :-- |
| `npm install` | Install dependencies |
| `npm run dev` | Start the dev server at `localhost:4321` |
| `npm run build` | Build the site to `./dist/` |
| `npm run preview` | Preview the build locally |
| `npm run screenshots` | Take screenshots for tools that have none yet (`SCREENSHOTS_FORCE=1` retakes all) |
| `node scripts/check-status.mjs` | Refresh `src/data/status.json` |
