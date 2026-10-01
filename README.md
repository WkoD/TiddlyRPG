# DnDWiki

A **TiddlyWiki 5** (Node.js edition) for D&D campaigns. This repo is the **copyable campaign
template**: per-wiki config, data tiddler templates (`PlayerLevel`) and (empty) content in
`tiddlers/` plus assets (`images/`, `data/`). Engine and format layer come as dependencies:

- **Engine:** the official [`tiddlywiki`](https://www.npmjs.com/package/tiddlywiki) from npm,
  pinned in `package.json`.
- **Format layer:** from [`TiddlyDnD-Plugins`](https://github.com/WkoD/TiddlyDnD-Plugins), pinned
  to a fixed version - the plugin `dndwiki-core` (+ `staticfiles`, optionally
  `dndwiki-forgottenrealms`).
- **Graph stack:** [`flibbles/tw5-graph`](https://github.com/flibbles/tw5-graph) +
  [`tw5-vis-network`](https://github.com/flibbles/tw5-vis-network) +
  [`tw5-relink`](https://github.com/flibbles/tw5-relink), each pinned to a release tag as an npm
  Git dependency.

## Setting up a new campaign

1. **Copy** this repo 1:1 (e.g. via "Use this template" on GitHub) and rename it to
   `DnDWiki-<Name>`.
2. Set `name` in `package.json` to the campaign name.
3. `npm install` (fetches the engine + pinned format layer/graph stack).
4. Choose the language (see "Languages" below): `tiddlers/$__language.tid` and, for anything but
   en-GB, `"languages"` in `tiddlywiki.info`.
5. Optional: a calendar for in-world dates (see "Calendar" below), e.g. the Calendar of Harptos
   for the Forgotten Realms: add `"dndwiki-forgottenrealms"` to `"plugins"` in `tiddlywiki.info`.
6. Fill the per-wiki config in `tiddlers/`: `$:/SiteTitle`, `$:/SiteSubtitle`,
   `$:/DefaultTiddlers`; optionally the captions of the graph views `$:/graph/*` in the campaign
   language.
7. Set `tiddlers/PlayerLevel.tid` (free text, e.g. `Level 1` or `0 EXP`).
8. Fill in `CAMPAIGN.md` - campaign-specific context for Claude (identity, table meta,
   conventions); instructions in the file header.
9. Add lore content under `tiddlers/`, images under `images/`, PDFs under `data/book/`.
10. Push the repo to GitHub; `.github/workflows/npm-build-pages.yml` builds and deploys
    automatically to `gh-pages` (set the Pages settings once to the `gh-pages` branch).

Do not exclude any folders - format layer and plugins come from the pin.

## Languages

Everything the format layer displays (headings, labels, type names such as "Location", dates)
follows the wiki language. Internal names (tags, fields) stay English, so content does not change
when the language changes.

| Language | Code | Format layer | TiddlyWiki interface |
|---|---|---|---|
| English (British) | `en-GB` | complete (default) | built in |
| German | `de-DE` | complete | official pack |

To set the language, two entries:

1. `tiddlywiki.info`: `"languages": ["de-DE"]` - loads the TiddlyWiki pack. Not needed for en-GB.
2. `tiddlers/$__language.tid`:
   ```
   title: $:/language

   $:/languages/de-DE
   ```

The template is set to en-GB. A language switch in the Control Panel while `npm start` is running
also writes `tiddlers/$__language.tid` - commit it only if the switch is meant to stay. How to add
a language: `README.md` of `TiddlyDnD-Plugins` -> "Adding a language".

## Calendar

Dates such as `1351-07-11` are shown as entered unless a calendar is active. A calendar adds month
names, festivals, the era ("1351 DR") and a calculator on the `Calendar` hub.

- **Forgotten Realms:** add `"dndwiki-forgottenrealms"` to `"plugins"` in `tiddlywiki.info` - it
  brings and activates the Calendar of Harptos.
- **Own calendar:** copy the data tiddler `$:/dndwiki/calendar/Harptos` (from
  `dndwiki-forgottenrealms`) into the wiki under a new title, adapt months, days, festivals and
  leap rule, and set `$:/config/dndwiki/calendar` to its title. The data model is described in
  `README.md` of `TiddlyDnD-Plugins` -> "Calendar".

## Editing

Edit locally with live editing:

```bash
npm install    # once: fetch engine + format layer + graph stack
npm start      # server on http://localhost:8080 with live editing
```

Changes made in the browser are written back automatically as `.tid` files in `tiddlers/` - no
manual saving needed. Details/conventions: `CLAUDE.md` -> "Commands & CI".

## Publishing

The copy deployed by the CI to `gh-pages` is **read-only**.

More documentation: `CLAUDE.md` (development/conventions), `CAMPAIGN.md` (campaign-specific).
