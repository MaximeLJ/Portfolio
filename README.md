# Portfolio

Working tools, each built by directing [Claude](https://claude.com) (Anthropic) through iterative conversation and testing the result — planning the features, making the product and UX calls, and catching real bugs by actually using what got built. The code in each project folder was written by AI; each project's own README explains that project's split in more detail.

**[Browse the index →](https://YOUR-USERNAME.github.io/portfolio/)**

## Projects

| Project | What it is |
|---|---|
| [`cycling-route-planner/`](./cycling-route-planner) | A cycling route planner — loop/point-to-point routing, elevation, alternates, shareable links |

## Structure

Each project lives in its own folder with its own `index.html` (so it's reachable at `/portfolio/project-name/`) and its own `README.md`. To add a new one:

1. Create a new folder at the root of this repo, e.g. `new-project/`.
2. Put the project's entry point at `new-project/index.html`.
3. Add a short `new-project/README.md` describing it.
4. Add a row to the table above, and an entry in the root `index.html` list.

No build step for any of this — it's all static files served directly by GitHub Pages.
