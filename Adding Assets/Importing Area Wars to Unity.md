
# Getting 3d models from Area Wars FBX to TTS through Unity 3d

If you want to add models to the repository, I'd love your help!  Here are the basics of getting some models ready to build into a Unity Asset Bundle, which will be a separate how to.

## Things you'll need:
- For this tutorial, the Gundam Area Wars model repository, and a unit of your choosing.
- An FBX previewer is really helpful, as it will let you preview the models and sometimes animations if that's included.  I like Autodesk FBX Review, it's lightweight and stable.  [Get it here.](https://www.autodesk.com/products/fbx/fbx-review)
- Blender (or other 3d modeling program, I'll use Blender as a reference though.) [Stable Release](https://www.blender.org/download/)
- [Unity version 2019.1.14f1](https://unity3d.com/unity/whats-new/2019.1.14) (other 2019.1 releases may work with the 3.0 mod release, but this is the one that works for me)
- [Berserk Games TTS project for Unity v3.0](https://github.com/Berserk-Games/Tabletop-Simulator-Modding/releases/tag/v3.0) (there's a newer update that I haven't tried yet, and I'll update this once I do), but this one works)
- Patience...

# Part 1: Area Wars to Blender

## Step 1: Pick a unit
This seems kind of basic, but it can take time to find the model you're after, even with the spreadsheet unit name converter.  I have spent hours renaming folders and organizing them and I'm only maybe a third of the way through it.  Some units have lots of pose options, which makes getting a variety of poses easy.

## Step 2: Import your model into Blender.  
Open blender, and you'll be greeted with the standard Blender intro scene.  Hitting A, X, D (in that order) will clear the scene so you can get going on the good stuff.
![001 Blender Blank](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/3bc64ea4-dfbe-41b1-9779-4ccfdf5e2cbc)

We need to import the model(s) of your choosing, and Blender makes that very easy.  Import -> FBX
![002 Import FBX](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/557a009a-c6a8-4e87-9483-09242812e132)

You can even grab multiples if you already know which ones have the poses you want.
![003 Import multiple FBX](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/b55976e5-0296-4f97-97c6-307fb4eb926b)

## Step 3: Check the scaling.
Area Wars models come with the root node scaled down to 0.01 scale. Hit n to see the transform window pop up on the screen, and it'll show you the scale.
![004 MS for ants](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/d21d9891-4693-4d44-ab50-9e59aef17c9c)

To scale it up properly, make sure you've got the top level of the model selected in the navigator, then hit S, 100.  That will bring it up to 1/1000 scale in mm in system units.  Do it to all of the models you've brought in.
![005 woah](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/c360b74c-baed-40a9-869d-b7af1f5b3bb9)

Do a sanity check the Z height of the model.  If it's about right, then we're good.  If not, then a quick scale will fix it.  Divide the suit height by the z height to find your new scaling factor.  e.g., if the imported height is 36, and the Gundam is 18, 18/36 = 0.5, and just scale all the imported models by 0.5. (usually models imported from the same source have the same scaling.

Next, move your models (making sure you've still got the top level of the model selected in the navigator for each model).  Select one and hit G, Y, 30.  Then the next G, Y, 60, etc.
![006 Closer](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/3480c63b-5e99-43f7-b6a3-96a89cf0e7ae)

## Step 4: Check the textures.
One thing you may run into is textures looking backwards or otherwise weird. This is easily fixed with changing the texture blend mode to opaque - select a model itself, select the little globe icon tab on the right, and scroll down to Settings.  Change Blend Mode to Opaque, and it'll be just fine.
![007 Inside Out](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/6d6c084e-35d3-45f0-97e6-9d9bc8f55791)

## Step 5: Export.
You can export as either .obj or .fbx, Unity can handle either.  I prefer using .obj if I'm not doing an animation, but it's up to you.  Select and export each model separately, naming each one so that you can tell what it is on import.  
![008 Ikimasu](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/f0273319-54b0-49b0-b452-6022edd2d0e4)

The important parts here are make sure 'Include -> Selection Only' is checked, and 'Transform -> Scale' is set to 0.273.  This will make sure you're only exporting one pose per .obj, and it is pre-scaled to 1/144 in inches in TTS.
![009 Ikimashou](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/49fc4c60-3f25-4a6a-88d7-65caefb5075a)

Some meshes are rigged with animations.  I haven't cracked the animation code yet, but in blender you can scrub through the animation timeline by grabbing the little box down by the bottom of the screen and dragging it through the keyframes until you find one you like.  Then just export as .obj and it'll grab it from that timestamp pose.
![010 Mata Ikimashou](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/b5acc907-6e83-43f1-a28c-b5aa6d5d7bba)

### Note on separated units like funnels
For units with funnels and other sorts of separated objects, we need to treat them a little differently.
![011 Funnel Pose](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/a4e4d874-ed40-42e7-956a-1a37a3641608)

We just need to export one of them, not all of them, and we can bundle it directly in Unity.
![012 Just one](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/5fe7a356-b292-4e30-8d02-b6fe46006017)

# Part 2: Blender to Unity

## Step 0: Follow the TTS Unity tutorial
[TTS Custom AssetBundle Walkthrough](https://kb.tabletopsimulator.com/custom-content/custom-assetbundle/) This will walk you through the whole process of installation, project folder finding, making a basic asset, and getting it into TTS.  If you can finish the tutorial, you'll be nearly there, honestly.

## Step 1: Organizing
Now that the project opened nicely, we need to set up some files.  In the 'Tabletop-Simulator-Modding\Assets' folder, make a new folder called 'Gundam', and a subfolder named for the unit you're working on.  Take the folder with the clump of files, materials, and texture images you put together and copy it to the '\Tabletop-Simulator-Modding\Assets\Gundam\\[UNIT]' folder.  It's really important to keep the files for each unit separate, or it'll become a nightmare really quickly.

## Step 2: Setup
Go to the Assets folder in the project navigator on the bottom left and navigate to your project folder.
