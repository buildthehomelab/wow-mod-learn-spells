# mod-learn-spells (Aldrynth)

Fork of [azerothcore/mod-learn-spells](https://github.com/azerothcore/mod-learn-spells) for the Aldrynth realm.

## Behaviour

- Auto-learns normal **trainer** class spells on level-up through **`LearnSpells.MaxLevel` (55)**.
- Levels **56–80**: train from class trainers as usual (talent resets unchanged).
- **Quest mounts** and **rare trainer-book ranks** are **not** auto-taught — complete quests / farm books as blizzlike.
- **Class quests are kept** (`LearnSpells.KeepClassQuests`): spells a quest teaches are learned from the quest, not on level-up. The first time it runs, the module reads every quest's reward spell (following the "teach" spell to what it learns) and never auto-learns those: Bear Form, Aquatic Form, Cure Poison, Voidwalker / Succubus / Felhunter, Defensive / Berserker Stance, shaman totems, Tame Beast and pet training, Redemption, ...
- Finishing a class quest immediately teaches the higher ranks of that spell you skipped while it was missing (e.g. Healing Stream Totem ranks after *Call of Water*).
- Shamans only get free totem items on first login when `KeepClassQuests = 0`.

## Conf defaults

| Key | Value |
|-----|-------|
| `LearnSpells.Enable` | `1` |
| `LearnSpells.Announce` | `0` |
| `LearnSpells.OnFirstLogin` | `0` |
| `LearnSpells.MaxLevel` | `55` |
| `LearnSpells.KeepClassQuests` | `1` |

## Scrub list (Aldrynth)

Removed from `m_additionalSpells` (and added to `m_ignoreSpells` where relevant):

| Spell IDs | Reason |
|-----------|--------|
| 5784 Felsteed, 23161 Dreadsteed | Warlock mount quests |
| 13819 / 34769 Warhorse, 23214 / 34767 Charger | Paladin mount quests |
| 25306 Fireball R12 | Rare trainer book |
| 40120 Swift Flight Form | Druid quest (also level > 55) |
| All `m_additionalSpells` buckets level **> 55** | Defense in depth with MaxLevel |

Kept trainer-style extras ≤55 (parry, dual wield, pet basics, mail/plate, capital teleports/portals, Redemption / Life Tap trainer ranks, etc.).

## Requirements

- [AzerothCore](https://www.azerothcore.org/) wotlk (master) and a WoW 3.3.5a (12340) client.
- No SQL, no client patch and no other module.

## Install

```bash
cd modules
git clone https://github.com/buildthehomelab/wow-mod-learn-spells.git mod-learn-spells
# reconfigure CMake, rebuild, copy conf.dist → conf, restart worldserver
```

## Troubleshooting

- **A character didn't get a spell at level 56 or above.** Auto-learning stops at
  `LearnSpells.MaxLevel` (55). Train from the class trainer as usual.
- **Bear Form, Voidwalker, a stance or a totem wasn't learned on level-up.** With
  `LearnSpells.KeepClassQuests = 1` those come from the class quest. Set it to 0 to auto-learn
  them like upstream.
- **A mount or a rare spell rank is missing.** Quest mounts and rare trainer-book ranks are left
  out on purpose; complete the quest or find the book.
- **A new character starts with no spells.** `LearnSpells.OnFirstLogin` is 0 by default; set it
  to 1 to give a new character its spells on first login.

## Credits

Author: [buildthehomelab](https://github.com/buildthehomelab)

Based on [VenomekPL/mod-learn-spells](https://github.com/VenomekPL/mod-learn-spells) (the
Aldrynth fork: auto-learn through level 55, quest mounts and books left out), which is a fork of
[azerothcore/mod-learn-spells](https://github.com/azerothcore/mod-learn-spells) by the
AzerothCore community. Changes here: `LearnSpells.KeepClassQuests`, which keeps class quests
meaningful.

## License

GNU Affero General Public License v3.0, see [LICENSE.md](LICENSE.md).
