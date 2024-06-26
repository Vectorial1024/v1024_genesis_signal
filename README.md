# Genesis Signal
Unified Mission Director cues for correctly detecting X4 Foundations game start events.

- Our GitHub repository: https://github.com/Vectorial1024/v1024_genesis_signal
- Our EgoSoft Forums page: https://forum.egosoft.com/viewtopic.php?t=463558
- Our Steam Workshop page: https://steamcommunity.com/sharedfiles/filedetails/?id=3275279686
- Our Nexus page: (WIP)

---

For a long time in the modern X-game engine (X: Rebirth, and X4: Foundations), it has always been possible to start the game in so-called "alternate universes". This feature is later extensively used in X4 Foundations:
- Tutorial levels
- Station Design Simulator
- 7.0 Timelines DLC

Mods that listen to game start events may be triggered when e.g. visiting the Station Design Simulator. These usually can be overlooked, but mods starting inside the Facility in the Timelines DLC is simply going too far. This mod therefore provides some unified signals for such mods to listen to, so that the Timelines DLC is not tampered with (at least not so obviously).

Alternate universes that may also be considered "canon" (e.g. the Star Wars overhaul universe) should patch their universe information into this mod to unify the start up sequence.

## How to listen to the proper "universe started" events?

Perhaps you are trying to initialize something when the universe starts.

If you would normally be listening for `<event_cue_signalled cue="md.Setup.Start" />`, then it is simple:

```xml
<conditions>
    <!-- This is triggered only when the universe is a known Open Universe -->
    <event_cue_signalled cue="md.GenesisSignal.Start" />
</conditions>
```

It is probably rarer to need to listen for `<event_cue_complete cue="md.Setup.Start" />`, but it is still doable:

```xml
<conditions>
    <event_cue_complete cue="md.Setup.Start" />
    <!-- if true, then it is an Open Universe game -->
    <check_value value="@global.$isOpenUniverse" />
</conditions>
```

This showcases the global variable for Open Universe checking, which may be used in regular MD scripts and AI scripts.

## How to patch my alternate universe into Genesis Signal?

Example of alternate universe from the community: Star Wars Interworlds.

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
        <check_value value="player.galaxy.macro.ismacro.{macro.your_open_universe_here}" />
    </add>
</diff>
```

Optionally, declare dependency on Genesis Signal by editing your `content.xml`:

```xml
<content>
    <dependency id="ws_3275279686" name="Genesis Signal"/>
</content>
```
