WIP Version can be downloaded from releases page or by going to blender branch. Currently it needs to overwrite the default extension and does not differentiate itself in the blender UI

**For texturing to work you need to export materials and models from fmodel as json format! The model must be in the same folder as the uemodel export and materials must be in the appropriate relative folder**

Yes this sucks because fmodel exports are extremely inconsistent, don't actually list which files were exported, sometimes export things to Game and sometimes to GameName/Content, etc. Even so this addon will save you a ton of time if you just make sure to merge your folders.

I will resolve this somehow before I make a pull request. Possibilities include: adding a few options to set corresponding paths in blender, more expensive filesystem searching, an fmodel update to auto export properties and/or fix export process in general, or most likely a cue4parse update to embed the textures or at minimum embed the texture names in uemodels. 

Alternatively I could require ueassets to be present but at that point I may as well just ditch uemodel format and make a new addon that uses cue4parse and/or uassetapi. then you could just use repak to extract an entire game. blender imports would probably be longer but idk seems kind of worth it. Might do that 


<div align="center">

# UEFormat

A model and animation export format created for Unreal Engine game asset extraction. The export format is currently supported by [FortnitePorting](https://github.com/h4lfheart/FortnitePorting), [FModel](https://github.com/4sval/FModel) and [CUE4Parse](https://github.com/FabianFG/CUE4Parse).

</div>

## Plugins
- [Blender](https://github.com/h4lfheart/UEFormat/tree/blender)
- [Unreal Engine](https://github.com/h4lfheart/UEFormat/tree/unreal)

## Format Specification
- [Generic](https://github.com/h4lfheart/UEFormat/tree/master/docs/generic.md)
- [UEModel](https://github.com/h4lfheart/UEFormat/tree/master/docs/uemodel.md)
- [UEAnim](https://github.com/h4lfheart/UEFormat/tree/master/docs/ueanim.md)
