# Genesis Signal
Unified Mission Director cues for correctly detecting X4 Foundations game start events.

(links etc)

---

For a long time in the modern X-game engine (X: Rebirth, and X4: Foundations), it has always been possible to start the game in so-called "alternate universes". This feature is later prominently used in X4 Foundations:
- Tutorial levels
- Station Design Simulator
- 7.0 Timelines DLC

Mods that listen to game start events may be triggered when e.g. visiting the Station Design Simulator. These usually can be overlooked, but mods starting inside the Facility in the Timelines DLC is simply going too far. This mod therefore provides some unified signals for such mods to listen to, so that the Timelines DLC is not tampered with (at least not so obviously).

Alternate universes that may also be considered "canon" (e.g. the Star Wars overhaul universe) should patch their universe information into this mod to unify the start up sequence.

## How to listen to the proper "universe started" events?

(WIP)

## How to patch my alternative universe into Genesis Signal?

Your mod structure:

```
/content.xml
/libraries/[...]
/extensions/v1024_genesis_signal/md/v1024_genesissignal.md
```

Inside `/extensions/v1024_genesis_signal/md/genesissignal.md`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<diff>
    <add sel="/mdscript/cues/cue[@name='Start']/conditions/check_any">
        <!-- Your open universe here -->
        <check_value value="player.galaxy.macro == macro.your_open_universe_here" />
    </add>
</diff>
```
