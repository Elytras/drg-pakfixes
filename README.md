# DRG pak fixes

Pak mods for Deep Rock Galactic that fix bugs and performance problems in other mods and in the game
itself. Byte patches for the game's executable live in [drg-bitfixes](https://github.com/Elytras/drg-bitfixes).

The top-level paks are for the release build. The paks in [`experimental/`](experimental) are for the
experimental branch (build CL-165596) only: install them there and not on release.

Every pak is compiled from C++ by AssetGen, in a private repo; the Commit column names the commit of the
fix's source. All paks here were checked current against that repo's `main` at `9751dfad`.

## Install

Install with [MINT](https://github.com/trumank/mint). Add a pak by its local path or by its raw URL,
`https://github.com/Elytras/drg-pakfixes/raw/main/<Name>_P.pak` (`.../raw/main/experimental/<Name>_P.pak` for an experimental one). Then place it as its row says:

- **Patch over:** the original mod stays installed. Put the fix **directly above** the original in the MINT
  list: the fix ships its own copy of some of the mod's files, and MINT keeps the copy of whichever mod is
  listed first. A patch is built against the version of the mod named in its row; after the mod updates,
  the patch can undo the update's changes to the files it carries.
- **Patch over, anywhere:** the original mod stays installed, and the fix can go anywhere in the list: it
  edits none of the mod's files and corrects it from outside.
- **Replacement:** remove the original mod and install the fix in its place.
- **Base game:** no other mod needed; anywhere in the list.

## Fixes

| Fix | What it fixes | Type | Original | Commit |
| --- | --- | --- | --- | --- |
| `AdvancedDarknessFix_P.pak` | Advanced Darkness scans every actor of the level for lights once a second, a 2-5 ms frame each second. The scan is spread over frames. | Patch over | [Advanced Darkness Reloaded](https://mod.io/g/drg/m/advanced-darkness-reloaded) (modfile 2845447) | `a4bc101e` |
| `AllyOutlinesFix_P.pak` | A teammate outlined only at the head; an empty resupply pod still outlined with "Disable Resupply Outline" on. | Patch over, anywhere | [Customizable Ally Outlines](https://mod.io/g/drg/m/customizable-ally-outlines) 1.7 | `9a60fa84` |
| `BuildInspectorFix_P.pak` | The page rebuilt every row on every hub open (6-12 ms); a row is now remade only when its builds change. Adds an "Always show names" box, for player names with four players or fewer. | Patch over | [Build Inspector](https://mod.io/g/drg/m/build-inspector) (modfile 4191394) | `5aa7bf70` |
| `BuyableMissions_P.pak` | A maintained build of Buyable Missions 2.0.5, whose author has left modding: biomes the menu did not know, such as Ossuary Depths, can be bought. | Replacement | [Buyable Missions](https://mod.io/g/drg/m/buyable-missions) 2.0.5 | `a2803e50` |
| `CD2FrozenFix_P.pak` | An enemy's "Materials" override is lost when the enemy is frozen and thawed. | Patch over | Custom Difficulty 2, updates 17, 18 and 18f1: not on mod.io | `7c2d9ef7` |
| `CD2VeteranFix_P.pak` | Enemies that CustomVeterans puts in another's place are not announced as spawned, so CD2's controls for their descriptor and other mods miss them. | Patch over | Custom Difficulty 2, update 18f1: not on mod.io | `9a05fb20` |
| `ColorfulSugarFix_P.pak` | Red sugar draws plain grey from the second mission on. Not yet checked in game. | Patch over | [Colorful Sugar](https://mod.io/g/drg/m/colorful-sugar) 1.0.2 | `c5997301` |
| `CombinedPresetsFix_P.pak` | Looks for the pickaxe menu among the open windows instead of walking every widget twice a second (4 ms/s on the Space Rig). | Patch over | [Combined Presets](https://mod.io/g/drg/m/combined-presets) 4.14 | `988b0d3b` |
| `CritterListFix_P.pak` | A host crash (access violation reading 0x130) in the critter cull, and new critters stopped for the rest of a mission. The same crash as drg-bitfixes' `critter_cull_crash_fix.lua`: install one or the other. Host only. | Base game | Base game | `c90d952f` |
| `CustomVanityFix_P.pak` | Each custom item was fetched 18 times per level load; now once. | Patch over | [Custom Vanity Framework](https://mod.io/g/drg/m/custom-vanity-framework) 1.1.2 | `988b0d3b` |
| `DownStatFix_P.pak` | 6-9 ms on every hub open and every 2D/3D switch: each of the mod's four pages now fills as it is shown. | Patch over | [downed stats/downed record](https://mod.io/g/drg/m/downed-statsdowned-record) 1.4.0 | `a9a4bdb9` |
| `EnemyRadarFix_P.pak` | A hub close could delete the settings file, so the radar lost its settings. The radar also re-added every dot to its canvas on every update. | Patch over | [Enemy Radar](https://mod.io/g/drg/m/enemy-radar) 2.2.1 | `fd1f143c` |
| `HealthNumberFix_P.pak` | Searched every widget once a second for the mission HUD, all session (1.5 ms/s); reads it off the HUD actor. | Patch over | [Health Number](https://mod.io/g/drg/m/health-number) 1.6 | `988b0d3b` |
| `InsectSwarmFix_P.pak` | A honeycomb destroyed instead of killed left its swarm flying; the swarm now goes with the comb. Host only. | Base game | Base game | `faec5e23` |
| `MagnificentMulesFix_P.pak` | The material list sorted by a Blueprint quicksort at every level load (most of a ~300 ms frame); sorted natively, same order. | Patch over | [Miracle's Magnificent M.U.L.E.s and More](https://mod.io/g/drg/m/miracles-magnificent-mules) 2.0.7 | `e4a9d17c` |
| `MissionTimerFix_P.pak` | The timer formatted in Blueprint every frame (4.6 ms/s); formatted natively and set only when it changes. | Patch over | [SimpleMissionTimer](https://mod.io/g/drg/m/simplemissiontimer) 0.4.3 | `112536cd` |
| `MOTDFix_P.pak` | Message presets past slot 0 were not kept; the Stat Track page builds its history texts once a level, not on every show. | Patch over | [MOTD + Stat Track](https://mod.io/g/drg/m/motd-stattrack) 2.4.0 | `a94d2543` |
| `MPBLevelCapFix_P.pak` | The Greenbeard Helper's "Under Level" box stopped at 300; it now goes to 10000. | Patch over | [More Players Balanced](https://mod.io/g/drg/m/more-players-balanced) 4.1.2 | `3655a288` |
| `OptionsAudioFix_P.pak` | The hitch on the escape menu's Options button: the audio-output row listed the system's audio devices 2 + 4n times for n devices; now once. | Base game | Base game | `efed4287` |
| `PlayerTitleFix_P.pak` | Searched every widget for the Space Rig HUD once a second (1.9 ms/s); keeps the HUD it found. | Patch over | [Custom Player Title](https://mod.io/g/drg/m/custom-player-title) 1.0 | `988b0d3b` |
| `SpectatorCamFix_P.pak` | Every player's spectator camera traced each frame with nobody spectating (6.7 ms/s); a camera ticks only while viewed. | Patch over | [Better Spectator](https://mod.io/g/drg/m/better-spectator-reloaded) (modfile 2845449) | `988b0d3b` |
| `StatTrackerFix_P.pak` | On a client the tracker could stay on a HUD the server had replaced, out of sight; it is put back on the current one. Not yet checked in game. | Patch over | [Live Mission Stat Tracker +](https://mod.io/g/drg/m/live-mission-stat-tracker-plus) 1.7.0 | `15e17406` |
| `TemperatureNumberFix_P.pak` | Searched every widget once a second for the mission HUD, all session on the Space Rig (2 ms/s); reads it off the HUD actor. | Patch over | [Temperature Number](https://mod.io/g/drg/m/temperature-number) 1.1.6 | `988b0d3b` |
| `TerrainSyncFix_P.pak` | Two multiplayer terrain desyncs: a client sees an alien egg without its egg-sack terrain, or keeps the Caretaker vault's placeholder terrain (it blocks shots, and standing on it drops you through the map). Host only. Install through MINT, never loose in `Paks`. Release only: Season 7 (the experimental branch) fixes both in the game, so leave it off there. | Base game | Base game | `43e1016a` |
| `WeaponRangesFix_P.pak` | The bug check, ten times a second, walked every pawn of the level and restyled every flying one. It now lists the pawns once a second and works on the flying enemies it has cached. | Patch over | [Visible Weapon Ranges](https://mod.io/g/drg/m/visible-weapon-ranges) 2.0.1 | `89826240` |

## Experimental fixes (CL-165596)

Mods that break on the experimental branch, built against its own game files.

| Fix | What it fixes | Type | Original | Commit |
| --- | --- | --- | --- | --- |
| `experimental/SeasonChallengesFix_P.pak` | The game crashes at launch: the mod ships release's season settings, which on experimental drop Season 7. Rebuilt on experimental's settings with the mod's one change, 5 active challenges. | Replacement | [Season Challenges Expanded](https://mod.io/g/drg/m/season-challenges-expanded) 1.2 | `75703545` |
| `experimental/VanityEraserFix_P.pak` | The game crashes at load: the mod ships release's vanity settings (`GD_Vanity`), which on experimental drop the tattoo preview and two category icons. Experimental's settings with the mod's one change, no DLC-locked items. Checked at load only: the game reaches the Space Rig with the mod and the fix; the vanity screens are not yet checked. | Patch over | [Vanity Restriction Eraser](https://mod.io/g/drg/m/vanity-restriction-eraser) 5.1.1 (5.0 too) | `d00aed0c` |
| `experimental/AllCampaignsList_P.pak` | The mod's list of assignments is fixed at its build, so experimental's new ones (the four Proficiency Unlocks, Xmas 2026 and its Old Hats and Tattoo) do not show. Builds the board's side list at each Space Rig load from every campaign the game ships, so later ones show too; Retirement and class campaigns are left to the game. Works alone; with the original it also keeps the original's older campaigns. Also restores Xmas 2025's Yearly Performance Bonus, which experimental dropped, rebuilt from release's own files (progress carries over). Checked in game: the list grows from 84 to 110, plus the restored one. | Patch over | [All Previous Campaigns Available](https://mod.io/g/drg/m/all-previous-campaigns-available) 1.8.0 (checked with; current is 1.15.1) | `706f1a0d` |

Notes:

- **Host only** fixes do their work on the host; clients may install them, and they then do nothing.
- `BuyableMissions_P.pak` still needs [Miracle Mod Manager](https://mod.io/g/drg/m/miracle-mod-manager). The mod
  is required by all players, so everyone in the lobby runs this build in place of the mod.io one.
- `CD2FrozenFix_P.pak`: Custom Difficulty 2 paints materials on each machine, so every player who runs CD2 wants it.

## Original authors

Each patch carries edited copies of the original mod's Blueprints, and `BuyableMissions_P.pak` is a full rebuild of its
mod. They are here because the fixes would otherwise go unshipped, not to replace anyone's work: if you are the
author of a mod listed above and want its fix or build taken down, open an issue and it will be removed.
