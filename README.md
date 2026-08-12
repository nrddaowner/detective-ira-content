# Detective IRA — case content

The cases for **Detective IRA**, a detective deduction game set across India.
This repository is the delivery channel: the app reads `content/manifest.json`
from here and downloads the case files it does not already hold.

It is **generated**. Nothing here is edited by hand — everything is produced from
the game's authoring tools and published in one step. Pull requests against these
files will not survive the next publish.

## Layout

```
content/
  manifest.json          version, the tag files are served from, sha256 of every file
  index.json             regions, cities, arc headers, the random deck
  stories/<id>.json      a story arc: its cases, and its finale wall
  cases/<id>.json        one playable case
```

## How the app reads it

The manifest is fetched from the `main` branch, which changes often and is cached
for hours. It names an immutable git **tag**, and every case file is fetched from
that tag instead — a tagged URL never changes, so a case that has shipped is
downloaded once and cached forever.

```
manifest  https://cdn.jsdelivr.net/gh/nrddaowner/detective-ira-content@main/content/manifest.json
files     https://cdn.jsdelivr.net/gh/nrddaowner/detective-ira-content@v1/content/cases/....json
```

Downloaded content is layered over the copy bundled inside the app, so the game
works offline, on first launch, and on any day this repository is unreachable.
Every downloaded file is checked against its hash and then run through the game's
full content validator before it is trusted; anything that fails is discarded and
the bundled copy stays live.

## Spoilers

These are the answers. `culpritId`, every alibi, and each arc's mastermind are all
here in plain JSON, because a free CDN in front of GitHub only serves public
repositories. If you would rather solve the cases, don't read the files.

## Licence

Content © the Detective IRA authors. Not for redistribution.
