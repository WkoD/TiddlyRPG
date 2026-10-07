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

- **House rules:** <!-- deviating rules -->

Who plays which character is in the field `player` of the characters (see below), not here.

## Conventions (DM decision)

The format offers several optional mechanisms. For each, the DM decides whether/how to use it in
this campaign - Claude follows that:

- **Session documentation:** <!-- Default proposal: no separate session log tiddlers; sessions
  are appended to the respective `Event` tiddler: the in-world date goes into its `date` field, the
  text into a section starting with `<<date>>`, the player characters who were there are tagged
  on it). Alternative: dated session tiddlers of their own. -->
- **Open items/plot threads:** <!-- Default proposal: use the `open-items` snippet inline in
  `Event` tiddlers (callout box, remove/shrink once resolved). Alternative: central tracker
  tiddler. -->
- **Maps of locations:** <!-- Default proposal: no sub-tiddlers - the map image in the field `map`
  of the location (`images/map/`), its places of interest as `<<spot "Name">>` sections at the
  end of its text, battle maps in the field `battlemap` (`images/battlemap/`) or as parameter of
  a spot; everything shows in the location's tab "Map" (see `CLAUDE.md`, "Maps of a location"). -->
- **Player visibility:** <!-- Default proposal: switch between the public view, the view of a
  player and the view of the DM with the page control "View" at the table; what only some
  players know is tagged `Secret` with their characters, parts of a text are locked with
  `<<secret "Character">>` or `<$secret for="Character">…</$secret>` (render convenience, no
  access protection). Whether the published copy offers the view of the DM:
  `tiddlers/$__config_dndwiki_view_dm-published.tid` with `yes`, default no. Alternative: do
  not use. -->
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
- **Location hierarchy (parent/child):** the field `location` ("liegt in") or a spot in the text
  of the parent ("Teil von"); the path of parents shows below the title. Tags express no
  places. <!-- Name the roots of this campaign here (worlds, planes, continents). -->
- **Player level:** body of `PlayerLevel.tid`.
- **Open plot threads:** search for the open-items snippet (`@@.tc-tiddler-frame`) in `Event`
  tiddlers.
- **Campaign structure / story arcs:** events with a player character tagged on them (the
  characters who were there); timeline and table on the hub `Campaign`.
- **Player characters:** tiddlers tagged `Player` (active) and tiddlers with a field `player`
  (played before), or the `Player` hub. The field `player` names the real player.
- **Secrets:** tiddlers tagged `Secret` (hub `Secret`, complete in the view of the DM).

*Then* make consistent proposals that build on existing tiddlers/tags (set explicit
`[[WikiLinks]]`).
