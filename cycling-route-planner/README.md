# Routecard

A cycling route planner. Loop or point-to-point routing, draggable "bulges" that let you push a loop's distance out in a direction without hand-drawing detours, avoid zones and road bans, an elevation profile you can scrub, alternate route options, per-leg time estimates at different riding speeds, and shareable links.

**[Live demo →](../)** — hosted on GitHub Pages, single HTML file, nothing to install.

## How this was built

The code was written entirely by [Claude](https://claude.com) (Anthropic), an AI assistant, across a long iterative conversation — no hand-written code in this project.

What I did was direct and test it, the same way I'd work with any engineer:

- **Set the product direction.** Every feature here — the loop-bulge mechanic, Komoot-style stop insertion, avoid zones, alternates, the elevation chart, fitness-level time estimates, the share-link system — started as something I asked for, usually after using an earlier version and noticing what was missing or annoying.
- **Made the UX calls.** Things like numbering stops A/B/1/2/3 consistently across the map and the lists, collapsing long stop/leg lists by default, click-to-highlight instead of a second confirmation step, what "extend" should mean on the bulge slider — these were my calls, iterated on until they felt right.
- **Found real bugs by actually using it**, not just by reading the code:
  - Caught that colour-by-type silently reverted to a plain line on every route recalculation.
  - Caught that a bulge could keep adding distance to a loop that had already grown past it, instead of backing off.
  - Caught a leg in the distance breakdown reading exactly `0.0 km` when there was visibly real distance on the map between those two stops — which turned out to be a genuine bug in how leg boundaries were matched to the route geometry when a route looped near itself.
  - Caught that a 37 km / 305 m climb route was estimating 3h42m, which didn't add up — that led to fixing an elevation-noise bug that was overstating total climb by roughly 2x.
  - Caught a page-load crash ("nothing is working") that turned out to be a variable-ordering bug in newly added code.

None of that was guesswork on my part — I compared what the app showed against what the map and the numbers should have implied, and pushed back until the discrepancy was explained and fixed.

## Features

- Loop or point-to-point routes, with drag-to-reorder stops
- "Bulges" — drag a pin to push a loop's distance outward toward an area, with live suppression when the route already passes close enough
- Avoid zones (draggable, resizable) and specific-road bans
- GPX import, including converting an imported track into an editable route
- Elevation profile with hover/click syncing to the map
- Alternate route options (BRouter's alternate paths, fetched on demand)
- Leg-by-leg time estimates across 7 riding-speed presets
- Undo for destructive edits
- Shareable links (route state is encoded in the URL — whoever opens it re-plots on their end)
- Export to GPX, or send straight to Komoot's upload page

## Stack

Single static `index.html`. [Leaflet](https://leafletjs.com/) for the map, [BRouter](https://brouter.de/) for routing, [lz-string](https://github.com/pieroxy/lz-string) for compressing share links. No build step, no backend.

## Known limitations

- Routing runs against BRouter's public demo server, which can be slow or rate-limited under load.
- Share links encode your stops/settings, not the plotted route itself, so the person opening a link re-plots — this keeps links short but means routing has to succeed again on their end.
- Leg time and climb estimates are reasonable approximations, not a physical model — treat them as a guide, not a promise.
