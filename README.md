# Slimboard — a featherweight make.fun frontend

[![make.fun · makefun-frontend-01](https://make.fun/badge/makefun-frontend-01.svg)](https://make.fun/bounty/makefun-frontend-01?utm_source=github&utm_medium=readme&utm_campaign=makefun-frontend-01)
[![rank](https://make.fun/badge/makefun-frontend-01/rebahan149/makefun-frontend-01-entry/rank.svg)](https://make.fun/bounty/makefun-frontend-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=makefun-frontend-01)
[![reward](https://make.fun/badge/makefun-frontend-01/rebahan149/makefun-frontend-01-entry/reward.svg)](https://make.fun/bounty/makefun-frontend-01?utm_source=github&utm_medium=readme&utm_campaign=makefun-frontend-01)

Slimboard is an original, dependency-free static frontend for [make.fun](https://make.fun),
built for the **makefun-frontend-01** bounty ("Build the best make.fun frontend").
No framework, no build step — just `app/index.html`, a few vanilla ES modules and one
stylesheet — reading make.fun's public API (`https://make.fun/api`, GET only) live.

## The four surfaces

- `#/` — the live bounty board: every open bounty with its **live pot** (prize + entry
  fees paid in), entry fee, entries, status and a ticking time-left, with type-to-filter,
  category filter and sorts (ending soonest, biggest pot, most entries, newest).
- `#/bounty/<slug>` — a bounty's own page: facts, phases, the rewards table split from
  the live pot, and its full description.
- `#/bounty/<slug>/leaderboard` — the ranked leaderboard with score intervals and prize
  places, rendered through a **windowed (virtual) list** so thousands of rows scroll
  smoothly, plus a row filter.
- `#/profile/<handle>` — a public profile: record (entered / placed / won / best
  placement / prize money), links, and every entry with its score.

## Why it is fast

- **Tiny first load** — a handful of small files, no framework, no fonts, no images.
- **ETag cache with stale-while-revalidate** — repeat views paint instantly from cache
  and revalidate with `If-None-Match`; a 304 costs no re-render. A small header counter
  shows live API requests vs. cache revalidations.
- **Cheap updates** — countdowns tick by rewriting only the countdown text nodes once a
  second; lists are never rebuilt to move a clock.
- Accessible by default: landmarks, labels, focus styles, keyboard-reachable controls,
  and a phone layout that restacks the board.

## Run it

```sh
node serve.ts --port 8091   # then open http://localhost:8091
```

Any static file server pointed at `app/` works just as well.

## Hand it in

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts
```

This copies `app/` and `screenshots/` to `out/` and writes `out/dossier.json` using the
vendored `vendor/makefun-frontend.ts` library (the kit's copy, unchanged).

MIT licensed — see `LICENSE`. By [@rebahan](https://make.fun/u/rebahan).
