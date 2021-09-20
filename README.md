# HL2 SDK - Team Fortress 2 (2013)
The Half-Life 2 TF2 SDK Mirror merged with Source SDK 2013.

## Why does this exist?
Currently, the [`tf2` branch](https://github.com/alliedmodders/hl2sdk/tree/tf2) maintains the HL2 SDK that dates all the way back to the Orange Box update; it has only been modified enough towards the needs of SourceMod and its extensions. Aside from those modifications, everything else is out of date.

This fork attempts to solve that problem by merging both the SDK 2013 code and the specific changes made on that branch, allowing SourceMod extensions to utilize a *slightly* more updated SDK that is usable for modding TF2.

NOTE: Since the goal is for SourceMod extensions only, only the `tier1` and `mathlib` static libraries are meant to be compilable, while `tier0` and `vstdlib` were directly imported from SDK 2013. This project is not meant to be compilable as a whole.

## Building extensions
You can execute your build script normally just like with the original TF2 SDK branch. There's only one change that needs to be done.

Scroll down to this section in your build script:
```python
    if sdk.name in ['sdk2013', 'bms'] and compiler.like('gcc'):
      # The 2013 SDK already has these in public/tier0/basetypes.h
      compiler.defines.remove('stricmp=strcasecmp')
      compiler.defines.remove('_stricmp=strcasecmp')
      compiler.defines.remove('_snprintf=snprintf')
      compiler.defines.remove('_vsnprintf=vsnprintf')
```

Change the first line to:
```python
    if sdk.name in ['sdk2013', 'bms', 'tf2'] and compiler.like('gcc'):
```
