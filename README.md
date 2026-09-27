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

## Install

```bash
cd modules
git clone https://github.com/buildthehomelab/wow-mod-learn-spells.git mod-learn-spells
# reconfigure CMake, rebuild, copy conf.dist → conf, restart worldserver
```

Upstream credit: AzerothCore catalogue module authors.
