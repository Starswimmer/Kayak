KAYAK V0.6 — FEATURE LIST
======================================================================

Kayak and AIDSL are free to use, modify, and distribute.

However, any project or mod using Kayak and/or AIDSL must clearly display the
following credit on its public release/presentation page (e.g.,
Steam Workshop page, NexusMods page or equivalent):

    "Powered by Kayak and AIDSL (built for Sentient Sands)"

and include links to:

    https://github.com/Starswimmer/Kayak
    https://steamcommunity.com/sharedfiles/filedetails/?id=3675880187

This attribution is required for all public uses of Kayak.
Exceptions may be granted for specific collaborators at the
author's discretion.

1. Kayak
2. AIDSL


1. Kayak - By Pineaxe

CONTEXT ENGINE
--------------
- Text-based world knowledge database (KayakDB): plain text files
  organized into folders. No binary formats, no SQL, no external
  dependencies. Everything is human-readable and hand-editable.

- Layered retrieval: extracts keywords from player input, matches
  them against the entity index, then expands outward by following
  field references across entities. A question about Blister Hill
  automatically pulls in Holy Nation, Holy Phoenix, and any
  connected lore — without hardcoded relationship tables.

- Configurable retrieval depth: max_keywords, max_layers,
  max_matches_per_layer, max_files, and timeout_ms are all
  user-tunable via config/core_config.txt.

- Knowledge filtering ($knows_about): per-NPC whitelists control
  what world knowledge each character can access. A desert hermit
  doesn't know about Blister Hill politics. A Holy Nation paladin
  does. Filters are grown automatically during gameplay when NPCs
  visit new locations.

- Weight-based priority: entities with higher weight scores are
  preferred when context space is limited. Major characters and
  capitals appear before minor settlements and generic items.


ENTITY SYSTEM
-------------
- Folder-per-entity design: each NPC, location, faction, item,
  or lore entry is a folder containing entity.txt plus optional
  auxiliary files (dialogue.txt, stats.txt, notes.txt, etc.).

- Free-form fields: entity.txt supports any key = value pair.
  No schema enforcement. Modders can add custom fields without
  code changes.

- Structural vs prose convention: plain fields (faction, race,
  role) are used for indexing and cross-entity linking. Prose
  fields ($personality, $backstory, $description) are injected
  as context but never followed as link seeds. Custom fields
  follow the same convention.

- AIDSL-compatible content fields: personality, backstory, and
  speech quirks can contain structured notation like (()),
  @tags, & lists, and >>priority<< markers. These pass through
  to the LLM prompt untouched.

- Auto-derived metadata: Category and Name are automatically
  inferred from the folder structure. No manual registration.

- IGN_ prefix convention: files and folders starting with IGN_
  are completely ignored by the indexer. Use for backups,
  archives, and raw logs.


CAMPAIGN SYSTEM
---------------
- Per-campaign isolation: each playthrough gets its own copy of
  the database. Editing one campaign never affects another.

- Template-based seeding: new campaigns are created by copying
  KayakDB/Template/. The template contains base lore, factions,
  locations, items, and races that apply to every playthrough.

- Campaign switching: hot-swap between campaigns at runtime
  without restarting. Index rebuilds automatically.

- Campaign-specific NPCs: characters generated during gameplay
  live in categories/campaign_npcs/ and are unique to that
  campaign.


PROMPT BUILDING
---------------
- Mandatory prompt injection: files in mandatory/<PromptType>/
  are always included at the top of every prompt of that type,
  in numeric prefix order (1_rules.txt, 2_base_lore.txt, etc.).
  Editable per-campaign.

- Multiple prompt types: Chat, Biography, Loremaster, Speak.
  Each has its own mandatory folder and retrieval policy.

- Structured prompt assembly: prompts are built in sections
  (MANDATORY, WORLD_CONTEXT, TARGET_NPC, STATS, DIALOGUE,
  PLAYER_MESSAGE) with clear delimiters.

- Stats injection: live runtime data (health, location,
  inventory, faction relation) is written to stats.txt and
  included in the NPC's prompt section.


CHARACTER PERSISTENCE (V3)
--------------------------
- CharacterGateway: single read/write interface for all character
  data. One read path, one write path, one cache.

- Merge-mode writes: when saving character data, only changed
  fields are updated in entity.txt. Custom fields added by hand
  (like $combat_style or $secret_knowledge) are preserved across
  saves. Manual edits survive gameplay.

- Dialogue-only writes: normal conversation logging writes only
  to dialogue.txt without touching entity.txt. Biographies and
  personalities are never overwritten during regular gameplay.

- Dirty tracking: writes are skipped when content hasn't changed
  since the last save. Reduces unnecessary I/O.

- Write reason logging: every write records its reason (generation,
  metadata_fix, dialogue, rename, regeneration, batch_generation)
  for debugging.

- LRU cache with invalidation: recently-accessed characters are
  cached in memory. Cache is busted on campaign switch, server
  restart, or manual reload.


DIALOGUE SYSTEM
---------------
- Persistent dialogue history: conversation lines are stored in
  dialogue.txt per entity, trimmed to a configurable maximum.

- Automatic archival: lines beyond the keep limit are moved to
  IGN_dialogue_backup/archive.txt (ignored by indexer, preserved
  for reference).

- Dialogue read/write/replace API: separate endpoints for
  appending, replacing, and reading dialogue history.


ECONOMY SYSTEM
--------------
- Layered price modifiers: global, per-city, and per-NPC price
  multipliers stack to produce dynamic pricing.

- Shop inventory injection: trader NPCs receive their current
  stock list in the prompt, with sell rules enforced.

- Configurable via in-game commands: /k_npc_prices, /k_city_prices,
  /k_global_prices adjust modifiers at runtime.


IN-GAME COMMANDS
----------------
- /k_help: list available commands.
- /k_visited <place>: add a location to the current NPC's knowledge.
- /k_job <text>: update an NPC's role/job.
- /k_backstory <text>: update an NPC's backstory.
- /k_speech <text>: update an NPC's speech quirks.
- /k_note <field> <value>: set any custom field on an NPC.
- /k_speak <line>: echo a line directly as NPC speech.
- /k_npc_prices <multiplier>: set per-NPC price modifier.
- /k_global_prices <multiplier>: set global price modifier.
- /k_city_prices <city> <multiplier>: set per-city price modifier.


SENTIENT SANDS INTEGRATION
--------------------------
- Bridge architecture: the SentientSandsBridge translates between
  the mod's internal data format and Kayak's entity format. The
  mod never touches KayakDB directly.

- Hub HTTP client: lightweight HTTP router handles retries,
  timeouts, and error normalization between the bridge and the
  Kayak server.

- Auto-start: SentientSands launches the Kayak server automatically
  when the game starts. No manual setup required after installation.

- Action hint detection: the bridge detects player intent (recruit,
  trade, attack, follow) from message content and injects
  appropriate action tags into the prompt.

- Faction knowledge seeding: when a new NPC is created, their
  $knows_about field is automatically populated based on their
  faction using a configurable knowledge table.

- Race knowledge seeding: NPCs also receive baseline knowledge
  based on their race (e.g., Shek know about Admag and Squin).

- Player bio sync: the player's character bio and faction
  description are synced from SentientSands campaign files into
  Kayak's mandatory prompt section.

- Character registry: in-memory name-to-ID mapping for fast
  identity resolution without Kayak round-trips.

- Legacy migration tools: addons/LegacyImports/ contains scripts
  and batch files for importing character data from pre-Kayak
  SentientSands versions.


MODDING SUPPORT
---------------
- Zero-code content addition: add NPCs, locations, factions,
  items, and lore by creating folders with text files. No
  programming required.

- Addon system: third-party content packs can be distributed as
  zip files and extracted into the Template or a named campaign.

- Hot reload: POST /campaign/reload_index rebuilds the index
  without restarting. Edit files, reload, test immediately.

- Full API: 26 HTTP endpoints for reading, writing, and querying
  every aspect of the database.

======================================================================
AIDSL — Pineaxe
======================================================================

So, why did I develop AIDSL?

AIDSL is a small “coding language” designed as the next step for Kayak’s entity files.

The problem I kept running into is simple: most formats we use today are built to be parsed, validated, and structured for machines, not to be understood by language models.

JSON, cfg, even minimal formats like DACK, they store data well. But they don’t carry intent. They don’t express weight, nuance, or meaning in a way an LLM can naturally interpret.

And when your entire system depends on how well an LLM understands context, that becomes a bottleneck.

So instead of forcing LLMs to adapt to rigid data formats, I flipped the approach.

AIDSL is declarative and semantic-first. It allows you to define meaning before usage, and to shape how information should be interpreted, not just stored.

For example:

Symbols can be redefined depending on context

Expressions can carry emphasis (like >> <<) to influence importance

Structures are written to be readable both by humans and LLMs, without relying on strict parsing rules

The same syntax can represent different systems depending on prior definitions


In other words, AIDSL is not just a data format.

It’s a layer that sits between raw data and LLM interpretation, giving you control over how the model reads the world.

For Kayak, that means entity files are no longer just containers of information. They become structured intent, directly shaping how NPCs think, react, and behave.

AIDSL is free to use and modify, that’s the point.
Public use requires proper credit as defined above.

======================================================================
Kayak V3 — Pineaxe
Built for Sentient Sands by Harvicus
======================================================================
