# Singer

An automated Bard addon. It keeps a list of AoE songs up on the party, adds targeted (Pianissimo) songs on specific members or jobs, and handles Marcato, Clarion Call, Soul Voice, Nightingale, Troubadour, and Nitro. Song timers and recast windows are tracked so songs are refreshed before they wear off. Based on Ivaar's Singer, modified by PBW. This fork adds playlists used by the Kriz run bots.

- **Authors:** Ivaar, modified by PBW · **Version:** 2.3.1
- **Commands:** `//singer` or `//sing`
- **Files:** `Singer.lua` (commands, settings, display), `sing_cast.lua`, `sing_get.lua`, `song_timers.lua`, `data/settings.lua` (playlists and per-character song lists)

---

## Loading

1. Copy the folder to `Windower/addons/Singer/`.
2. On your BRD: `//lua load singer`
3. Load a playlist, then turn it on: `//sing pl melee`, then `//sing on`

The run bots drive it remotely, e.g. `send @BRD singer ballad 2 whm`, `so sing pl melee`, `send @BRD singer off`.

---

## Commands

### On/off and saving
| Command | What it does |
|---|---|
| `//sing` / `//sing on` / `//sing off` | Toggles, starts, or stops singing. |
| `//sing actions on\|off` | Same as on/off. |
| `//sing save` | Saves settings for all characters. |
| `//sing save <name>` / `//sing playlist save <name>` | Saves the current AoE song list as a playlist. |

### AoE songs and playlists
| Command | What it does |
|---|---|
| `//sing playlist <name>` (or `pl <name>`) | Loads a saved playlist as the AoE song list. |
| `//sing playlist <name> <member>` | Loads a playlist as Pianissimo songs for one member. |
| `//sing <slot#> <song name>` | Puts a song in AoE slot N. |
| `//sing <slot#> <song name> <member>` | Puts a song in slot N of a member's Pianissimo list. |
| `//sing <slot#> clear [member]` | Clears one slot. |
| `//sing clear aoe` | Clears the AoE list. |
| `//sing clear all` | Clears every member's Pianissimo songs. |
| `//sing clear <member>` | Clears one member's Pianissimo songs. |

### Pianissimo (single-target songs)
```
//sing <song type> [count] <member name | job>
```
For example, `//sing ballad 2 whm` gives the party's WHM two Ballads. You can name a **job instead of a character name**, and Singer finds that job in the party. `count` can be `off` (or 0) to remove the songs.

### AoE range checks
| Command | What it does |
|---|---|
| `//sing aoe on\|off` | Toggles all AoE range checks. |
| `//sing aoe <p1-p5\|name> on\|off` (also `add`/`+`/`watch`, `remove`/`-`/`ignore`) | Makes sure a party slot or member is in range before singing AoE, or ignores them. |

### Tuning
| Command | What it does |
|---|---|
| `//sing recast song\|buff <min> <max>` | Seconds before expiry to re-sing (default: songs 40–70, buffs 5–10). |
| `//sing ws > <tp>` / `//sing ws < <tp>` | Sets the min / max TP window for weapon-skilling between songs (default 20–99). |
| `//sing ws use on\|off` | Turns weapon-skilling on or off. A second word is required before `on`/`off`; it can be anything. |
| `//sing dummy<N> <song>` / `//sing dummy<N> remove` | Sets the dummy songs used to open extra song slots (default Puppet's and Scop's Operetta). |
| `//sing marcato <song>` | Song used with Marcato (default Honor March). |
| `//sing delay <sec>` / `//sing interval <sec>` | Delay between casts / main-loop interval. |
| `//sing clarion\|soul_voice\|nightingale\|troubadour\|nitro\|pianissimo\|timers on\|off` | Toggles each job ability or feature. |
| `p` / `n` / `t` / `pl` | Shortcuts for `pianissimo`, `nitro`, `troubadour`, `playlist`. |

---

## Playlists (`data/settings.lua`)

Playlists that match the run bots' content (load them yourself, or from your Multictrl stage setup; the bots themselves only call `sing pl melee` and `singer ballad …` directly):

| Playlist | Content | Songs |
|---|---|---|
| `odya` | Odyssey Sheol A, matching the **odya** bot (added in this fork) | Knight's Minne V, Honor March, Aria of Passion, Valor Minuet V, Valor Minuet IV |
| `odin` | Odin battlefield (**odin**) | Knight's Minne V, Honor March, Valor Minuet V/IV/III |
| `cait` | Champions of the Dawn (**palug**) | Blade Madrigal, Honor March, Sentinel's Scherzo, Light Carol, Light Carol II |
| `macro` | Qu'Bia Arena (**cosmic**) | Light Carol, Light Carol II, Valor Minuet V, Honor March, Blade Madrigal |
| `lilmnk`, `lilsb`, `lilsam` | Lilith fights, by party build (MNK, SB, SAM) | Ballad/Madrigal/March, Minuets, or Etudes depending on build |
| `melee` | Reisenjima farming (odin/malig/palug send `so sing pl melee`) | Valor Minuet V, IV, Honor March, Victory March, Valor Minuet III |

There are around 50 playlists in total (Sortie, Ambuscade, Odyssey NMs, tank, mage, ranged, and so on). Open `data/settings.lua` for the full list.

---

## Changes in this fork
- Sep 2024: added the `odya` playlist for the [odya](https://github.com/gregesposito/odya) Odyssey bot.

Upstream: [PeachBlossomWine/Singer](https://github.com/PeachBlossomWine/Singer).
