<!--
CAMPAIGN.md - SKELETON TEMPLATE (DnDWiki template).
This is the canonical template. In DnDWiki it stays empty/generic.
Every campaign fills in its OWN copy when copying the template 1:1, in the language of its
choice. This file belongs to the campaign - it is not distributed between repos and overwrites
nothing elsewhere.
-->

# CAMPAIGN.md

Campaign-specific context for Claude. **Strictly pointer based**: this file contains only stable
meta information and pointers to the wiki tiddlers - **no** data that can be derived from tiddlers
(names, level, dates, plot status), so that it does not go stale. Always read the real state live
from the tiddlers.

## Identity

<!-- Campaign identity: 1-2 lines, e.g. homebrew setting or official WotC adventure, content
     language, calendar (none, Harptos via dndwiki-forgottenrealms, own). No further narrative
     details. -->

## Table meta (NOT in tiddlers)

- **Player <-> character:** <!-- real player names <-> characters; leave empty if n/a -->
- **House rules:** <!-- deviating rules -->

## Conventions (DM decision)

The format offers several optional mechanisms. For each, the DM decides whether/how to use it in
this campaign - Claude follows that:

- **Session documentation:** <!-- Default proposal: no separate session log tiddlers; sessions
  are appended to the respective `Event` tiddler (several in-world points in time, separated by
  `---` with a date heading). Alternative: dated session tiddlers of their own. -->
- **Open items/plot threads:** <!-- Default proposal: use the `open-items` snippet inline in
  `Event` tiddlers (callout box, remove/shrink once resolved). Alternative: central tracker
  tiddler. -->
- **Maps of locations:** <!-- Default proposal: sub-tiddler `<location>/Map` (tag `Map`, field
  `image`) for an overview map and `<location>/BattleMap` (tag `BattleMap`) for a battle map next
  to the location tiddler, where a map makes sense. -->
- **Player visibility:** <!-- Default proposal: use the player login on the `Player` hub
  (`$:/state/dndwiki/player`) to switch between DM and player perspective at the table (render
  convenience, no access protection). Alternative: do not use. -->
- **Campaign-specific folders/assets:** <!-- e.g. additional subfolders under images/ for
  external tools (VTT screenshots or similar), if used. -->
- **Narrative style (tense):** <!-- Default proposal: no fixed rule, the DM decides. Example of a
  possible choice: past tense throughout as chronicle style, also for lasting properties/facts -
  does not imply death/non-existence then. Usual exceptions: direct speech/quotes, primary
  in-world documents, open-items callout boxes, trivia quiz blocks. -->


## Story planning workflow for Claude

**First read the real tiddler state through these pointers, never plan from memory or from this
file:**

- **Factions / locations / NPCs:** tiddlers with the respective type tag. Starting points:
  `Index` and the category hub tiddlers `Person`, `Location`, `Organisation`, `Event`,
  `Campaign`, ... (shadows from `dndwiki-core`).
- **Player level:** body of `PlayerLevel.tid`.
- **Open plot threads:** search for the open-items snippet (`@@.tc-tiddler-frame`) in `Event`
  tiddlers.
- **Campaign structure / story arcs:** tiddlers tagged `Campaign`.
- **Player characters:** tiddlers tagged `Player` or the `Player` hub.

*Then* make consistent proposals that build on existing tiddlers/tags (set explicit
`[[WikiLinks]]`).
