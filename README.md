# Livonia Fast Travel

Fast travel for a DayZ Livonia server. You don't need any mods, only the game's own `cfggameplay.json` features (object spawners and player restricted areas).

- **Log out standing at any well pump, outhouse or village bus stop** on the map (209 of them). When you log back in, you are in a hub: a garage floating high in the sky.
- **The hub has 31 portable toilets**, one per town, each with the town's name spelled out on the floor in front of it.
- **Log out standing in a toilet.** When you log back in, you are on open ground near that town, at one of ten spots kept clear of buildings, roads and water.

Walking into a teleport point does nothing on its own. The game only moves a player who logs in inside one, so travelling always means logging out at the point and logging back in.

## Requirements

- A DayZ server running the Livonia map (`dayzOffline.enoch` or your own Livonia mission), on DayZ 1.23 or newer (player restricted areas were added in 1.23).
- `cfggameplay.json` enabled. In `serverDZ.cfg`:

  ```
  enableCfgGameplayFile = 1;
  ```

## Install

1. **Copy the files.** Copy the `custom` folder from this repo into your mission folder, next to `cfggameplay.json`. If you already have a `custom` folder, copy the files into it. Your mission folder should then hold:

   ```
   mpmissions/dayzOffline.enoch/
     cfggameplay.json
     custom/
       teleports.json
       teleport-names.json
       pra-teleport-hub.json
       pra-teleport-adamow.json
       ... (31 town files in all)
   ```

2. **Spawn the hub.** In `cfggameplay.json`, add the two spawner files to `WorldsData.objectSpawnersArr`. Keep anything already in the list:

   ```json
   "objectSpawnersArr": [
       "./custom/teleports.json",
       "./custom/teleport-names.json"
   ],
   ```

3. **Turn on the teleports.** Add the 32 teleport files to `WorldsData.playerRestrictedAreaFiles`. If the key does not exist yet, add it inside `WorldsData`:

   ```json
   "playerRestrictedAreaFiles": [
       "./custom/pra-teleport-hub.json",
       "./custom/pra-teleport-adamow.json",
       "./custom/pra-teleport-bielawa.json",
       "./custom/pra-teleport-borek.json",
       "./custom/pra-teleport-brena.json",
       "./custom/pra-teleport-dolnik.json",
       "./custom/pra-teleport-drewniki.json",
       "./custom/pra-teleport-gieraltow.json",
       "./custom/pra-teleport-gliniska.json",
       "./custom/pra-teleport-grabin.json",
       "./custom/pra-teleport-huta.json",
       "./custom/pra-teleport-kolembrody.json",
       "./custom/pra-teleport-kulno.json",
       "./custom/pra-teleport-lembork.json",
       "./custom/pra-teleport-lipina.json",
       "./custom/pra-teleport-lukow.json",
       "./custom/pra-teleport-muratyn.json",
       "./custom/pra-teleport-nadbor.json",
       "./custom/pra-teleport-nidek.json",
       "./custom/pra-teleport-olszanka.json",
       "./custom/pra-teleport-polana.json",
       "./custom/pra-teleport-radacz.json",
       "./custom/pra-teleport-radunin.json",
       "./custom/pra-teleport-roztoka.json",
       "./custom/pra-teleport-sarnowek.json",
       "./custom/pra-teleport-sitnik.json",
       "./custom/pra-teleport-sobotka.json",
       "./custom/pra-teleport-tarnow.json",
       "./custom/pra-teleport-topolin.json",
       "./custom/pra-teleport-wrzeszcz.json",
       "./custom/pra-teleport-zalesie.json",
       "./custom/pra-teleport-zapadlisko.json"
   ]
   ```

4. **Restart the server.** DayZ only reads these files at startup.

A missing comma or bracket in `cfggameplay.json` stops the server from loading the whole file, so run it through a JSON validator before restarting.

## The destinations

The toilets are in alphabetical order around the hub. Facing the closed end of the room from the open side where you arrive, they run up the left wall, across the far wall and back down the right wall.

| # | Town | | # | Town | | # | Town |
|---|---|---|---|---|---|---|---|
| 1 | Adamów | | 12 | Kulno | | 23 | Roztoka |
| 2 | Bielawa | | 13 | Lembork | | 24 | Sarnówek |
| 3 | Borek | | 14 | Lipina | | 25 | Sitnik |
| 4 | Brena | | 15 | Lukow | | 26 | Sobotka |
| 5 | Dolnik | | 16 | Muratyn | | 27 | Tarnow |
| 6 | Drewniki | | 17 | Nadbór | | 28 | Topolin |
| 7 | Gieraltów | | 18 | Nidek | | 29 | Wrzeszcz |
| 8 | Gliniska | | 19 | Olszanka | | 30 | Zalesie |
| 9 | Grabin | | 20 | Polana | | 31 | Zapadlisko |
| 10 | Huta | | 21 | Radacz | | | |
| 11 | Kolembrody | | 22 | Radunin | | | |

## What each file does

| File | What it is |
|---|---|
| `teleports.json` | The hub: a `Land_Garage_Big` at 100, 1000, 100 (high above the map's south-west corner) with 31 `Land_Misc_Toilet_Mobile` inside. |
| `teleport-names.json` | The town names on the floor, drawn in a 3x5 pixel font with about 1,600 tiny `StaticObj_Misc_BoxWooden`. Optional: leave it out of `objectSpawnersArr` and the hub works the same, just unlabelled. |
| `pra-teleport-hub.json` | A 2 x 1.5 x 2 m box on each well pump, outhouse and village bus stop. Log out in one and you log back in at the hub. |
| `pra-teleport-<town>.json` | A box on that town's toilet in the hub and ten arrival spots around the town. Log out in the toilet and you log back in at one of the spots. The game sets your height to ground level. |

## Good to know

- **Teleports happen at login, not on contact.** The files use DayZ's player restricted areas, which move a player who logs in inside one of their boxes. Expect players to log out at an outhouse just to get to the hub, and anyone who happens to log out in one to wake up there.
- **The logout timer still applies.** Travelling takes as long as a logout and a login, so it is no escape from a fight.
- **You arrive at the spot nearest to where you logged out, not a random one.** From the hub, each town's toilet will usually send you to the same one of its ten spots.
- **To remove it**, take the files back out of both lists in `cfggameplay.json` and restart.

## Credits

The pixel font is the 3x5 "minifont" by /u/Udzu, from the r/PixelArt post "Smallest legible pixel fonts?".

Made for the DayZ Clan Wars Livonia server.
