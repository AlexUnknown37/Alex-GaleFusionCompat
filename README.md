# GaleFusionCompat

Fixes Voices of the Void closing right after launch when you use **NynrahGhost-Fusion** with the **Gale** mod manager. The same mods work in r2modman.

## The problem

Fusion reads a file called `mods.yml` from your profile folder. r2modman creates that file automatically. Gale doesn't, so Fusion crashes with:

```
FileNotFoundException: Could not find file '...\profiles\<name>\mods.yml'
   at FileUtils.GetFoldersToIgnore()
```

FusionPatch_P is never built, and the game closes. See [Gale issue #740](https://github.com/Kesomannen/gale/issues/740).

## What this mod does

Each time the game starts, it writes `mods.yml` into your profile from the packages installed there, including which ones you've disabled.

- In Gale, it refreshes the file on every launch, so it stays correct when you add, remove or disable mods.
- In r2modman, it never overwrites the file r2modman made.

## Install

Install it with your mod manager, alongside Fusion.

**On the very first launch after installing, the game may still close.** Fusion can start reading before this mod has written the file. Launch again and it will work from then on.

## Notes

- Pure Lua, runs inside UE4SS. No exe, nothing downloaded.
- Writes a single file: `<profile>\mods.yml`. Uninstalling the mod leaves the file in place, which is harmless.
- If Gale ever starts writing `mods.yml` itself, you can uninstall this mod.