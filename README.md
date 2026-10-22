# TiddlyRPG

A **TiddlyWiki 5** (Node.js edition) for tabletop role-playing campaigns. This repo is the **copyable campaign
template**: per-wiki config, data tiddler templates (`PlayerLevel`) and (empty) content in
`tiddlers/` plus assets (`images/`, `data/`). Engine and format layer come as dependencies:

- **Engine:** the official [`tiddlywiki`](https://www.npmjs.com/package/tiddlywiki) from npm,
  pinned in `package.json`.
- **Format layer:** from [`TiddlyRPG-Plugins`](https://github.com/WkoD/TiddlyRPG-Plugins), pinned
  to a fixed version - the plugin `tiddlyrpg-core` (+ `staticfiles`).
- **D&D content (optional):** from [`TiddlyRPG-DnD`](https://github.com/WkoD/TiddlyRPG-DnD),
  pinned the same way - the ruleset `tiddlyrpg-ruleset-dnd5e2014` (D&D 5e, rules of 2014) and
  the campaign setting `tiddlyrpg-setting-forgottenrealms` (calendar and coins).
- **Graph stack:** [`flibbles/tw5-graph`](https://github.com/flibbles/tw5-graph) +
  [`tw5-vis-network`](https://github.com/flibbles/tw5-vis-network) +
  [`tw5-relink`](https://github.com/flibbles/tw5-relink), each pinned to a release tag as an npm
  Git dependency.

## Setting up a new campaign

1. **Copy** this repo 1:1 (e.g. via "Use this template" on GitHub).
2. Set `name` in `package.json` to the campaign name.
3. `npm install` (fetches the engine + pinned format layer/graph stack).
4. Choose the language (see "Languages" below): `tiddlers/$__language.tid` and, for anything but
   en-GB, `"languages"` in `tiddlywiki.info`.
5. Optional: a ruleset and a campaign setting (see "Ruleset, campaign setting and rules
   language" below), e.g. D&D 5e and the Forgotten Realms: add the package `tiddlyrpg-dnd` to
   `devDependencies` and `"tiddlyrpg-ruleset-dnd5e2014"` and/or
   `"tiddlyrpg-setting-forgottenrealms"` to `"plugins"` in `tiddlywiki.info`; for a wiki in
   another language than English, choose the rules language. The package also brings the items,
   spells and creatures of the SRD 5.1 to take into the wiki one by one (in the editable wiki).
6. Fill the per-wiki config in `tiddlers/`: `$:/SiteTitle`, `$:/SiteSubtitle`,
   `$:/DefaultTiddlers`; optionally the captions of the graph views `$:/graph/*` in the campaign
   language.
7. Set `tiddlers/PlayerLevel.tid` (free text, e.g. `Level 1` or `0 EXP`).
8. Fill in `CAMPAIGN.md` - campaign-specific context for Claude (identity, table meta,
   conventions); instructions in the file header.
9. Choose the license of the campaign (see "License" below): replace `LICENSE`, `license` in
   `package.json` and the section "License" of this file.
10. Add lore content under `tiddlers/`, images under `images/` (where they come from: field
    `source`), PDFs under `data/book/`.
11. Push the repo to GitHub; `.github/workflows/npm-build-pages.yml` builds and deploys
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
a language: `README.md` of `TiddlyRPG-Plugins` -> "Adding a language".

## Ruleset, campaign setting and rules language

A game system and a world come as optional plugins:

| Choice | Options |
|---|---|
| Ruleset (rules terms: units, dice, damage, abilities, terms; macros such as `<<unit "30 ft">>`) | none, or `tiddlyrpg-ruleset-dnd5e2014` (D&D 5e, rules of 2014, terms of the SRD 5.1) |
| Campaign setting (calendar and currency) | none, `tiddlyrpg-setting-forgottenrealms` (Calendar of Harptos, coins of the Forgotten Realms), or an own calendar and currency (see below) |

Both come in the package `tiddlyrpg-dnd`. With one installed, it is active; Control Panel ->
Settings -> TiddlyRPG chooses among several or switches one off, and sets the **rules language**:
in which language rules terms are shown - the wiki language, one language for all, or per
domain; texts are read in every language. A German wiki shows "WEI", "9 m" and "50 GM" by default; for the English terms of
an English rulebook ("WIS", "30 ft", "50 gp") set it to English. The setting is stored in
`tiddlers/` (`$:/config/tiddlyrpg/rules/...`), so it applies to every reader. Ruleset and
campaign setting are set apart ("Ruleset options", "Campaign setting options"): English rules
terms with German month names are fine. Details:
`README.md` of `TiddlyRPG-Plugins` -> "Rulesets and campaign settings", "Rules language".

Without a currency (no campaign setting), `price: 50` stays a plain number and the hub "Currency"
is not listed under `Information`; with one, a price needs its coin: `price: 50 gp`. Without a
ruleset the hub "Ruleset" is not listed, and its macros show the text unchanged; without campaign
setting the hub "CampaignSetting" is not listed.

## Calendar

Dates such as `1351-07-11` are shown as entered unless a calendar is active. A calendar adds month
names, festivals, the era ("1351 DR") and a calculator on the `Calendar` hub.

- **Forgotten Realms:** add the package `tiddlyrpg-dnd` (repo `TiddlyRPG-DnD`) to
  `devDependencies` and `"tiddlyrpg-setting-forgottenrealms"` to `"plugins"` in `tiddlywiki.info` -
  it brings and activates the Calendar of Harptos and the coins of the Forgotten Realms.
- **Own calendar:** copy the data tiddler `$:/tiddlyrpg/calendar/Harptos` (from
  `tiddlyrpg-setting-forgottenrealms`) into the wiki under a new title, adapt months, days, festivals and
  leap rule, and set `$:/config/tiddlyrpg/calendar` to its title. The data model is described in
  `README.md` of `TiddlyRPG-Plugins` -> "Calendar". An own currency works the same way
  (`$:/tiddlyrpg/currency/ForgottenRealms`, `$:/config/tiddlyrpg/currency`; `README.md` of
  `TiddlyRPG-Plugins` -> "Currency").

## Editing

Edit locally with live editing:

```bash
npm install    # once: fetch engine + format layer + graph stack
npm start      # server on http://localhost:8080 with live editing
npm run check  # check every tiddler: errors and hints
```

Changes made in the browser are written back automatically as `.tid` files in `tiddlers/` - no
manual saving needed. While editing, errors and hints stand below the title of a tiddler (not in
the published copy). Details/conventions: `CLAUDE.md` -> "Commands & CI", "Checks".

How to use the wiki - the hubs, writing tiddlers, relations, locations, events, views and
secrets: `README.md` of `TiddlyRPG-Plugins` -> "Using the wiki", also in the wiki itself under
ControlPanel -> Plugins -> `tiddlyrpg-core` -> readme.

## Publishing

The copy deployed by the CI to `gh-pages` is **read-only**.

## License

The part between the lines `<!-- wiki -->` and `<!-- /wiki -->` also shows in the wiki, under
ControlPanel -> License, together with `LICENSE` and the licenses of all plugins. A campaign
replaces it with its own. If the campaign uses content of Wizards of the Coast (D&D, the
Forgotten Realms, an official adventure), it is fan content: the
[Fan Content Policy](https://company.wizards.com/en/legal/fancontentpolicy) wants it free for
everyone to use without credit - e.g. CC0 for the own content - and its notice in this section:
"[Title] is unofficial Fan Content permitted under the Fan Content Policy. Not approved/endorsed
by Wizards. Portions of the materials used are property of Wizards of the Coast. ©Wizards of the
Coast LLC."

A campaign that takes entries of the SRD 5.1 into its wiki (the content package of
`TiddlyRPG-DnD`) also carries, from the first one on, the attribution of page 1 of the SRD 5.1 in
this section, word for word: "This work includes material taken from the System Reference
Document 5.1 (“SRD 5.1”) by Wizards of the Coast LLC and available at
https://dnd.wizards.com/resources/systems-reference-document. The SRD 5.1 is licensed under the
Creative Commons Attribution 4.0 International License available at
https://creativecommons.org/licenses/by/4.0/legalcode."

<!-- wiki -->
The template TiddlyRPG is dedicated to the public domain under
[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) (`LICENSE`). A campaign
made from it chooses its own license.
<!-- /wiki -->

More documentation: `CLAUDE.md` (development/conventions), `CAMPAIGN.md` (campaign-specific).
