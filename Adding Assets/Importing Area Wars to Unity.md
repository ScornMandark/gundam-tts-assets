
# Getting 3d models from Area Wars FBX to TTS through Unity 3d

If you want to add models to the repository, I'd love your help!  Here are the basics of getting some models ready to build into a Unity Asset Bundle, which will be a separate how to.

## Things you'll need:
- For this tutorial, the Gundam Area Wars model repository, and a unit of your choosing.
- An FBX previewer is really helpful, as it will let you preview the models and sometimes animations if that's included.  I like Autodesk FBX Review, it's lightweight and stable.  [Get it here.](https://www.autodesk.com/products/fbx/fbx-review)
- Blender (or other 3d modeling program, I'll use Blender as a reference though.) [Stable Release](https://www.blender.org/download/)
- [Unity version 2019.1.14f1](https://unity3d.com/unity/whats-new/2019.1.14) (other 2019.1 releases may work with the 3.0 mod release, but this is the one that works for me)
- [Berserk Games TTS project for Unity v3.0](https://github.com/Berserk-Games/Tabletop-Simulator-Modding/releases/tag/v3.0) (there's a newer update that I haven't tried yet, and I'll update this once I do), but this one works)
- Patience...

## Navigator
- [Part 1: Area Wars to Blender](https://github.com/ScornMandark/gundam-tts-assets/blob/main/Adding%20Assets/Importing%20Area%20Wars%20to%20Unity.md#part-1-area-wars-to-blender)
- [Part 2: Blender to Unity](https://github.com/ScornMandark/gundam-tts-assets/blob/main/Adding%20Assets/Importing%20Area%20Wars%20to%20Unity.md#part-2-blender-to-unity)
- [Part 3: Unity to GitHub](https://github.com/ScornMandark/gundam-tts-assets/blob/main/Adding%20Assets/Importing%20Area%20Wars%20to%20Unity.md#part-3-unity-to-github)

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

[Back to top](https://github.com/ScornMandark/gundam-tts-assets/blob/main/Adding%20Assets/Importing%20Area%20Wars%20to%20Unity.md#navigator)

# Part 2: Blender to Unity

## Step 0: Follow the TTS Unity tutorial
[TTS Custom AssetBundle Walkthrough](https://kb.tabletopsimulator.com/custom-content/custom-assetbundle/) This will walk you through the whole process of installation, project folder finding, making a basic asset, and getting it into TTS.  If you can finish the tutorial, you'll be nearly there, honestly.

## Step 1: Organizing
Now that the project opened nicely, we need to set up some files.  In the 'Tabletop-Simulator-Modding\Assets' folder, make a new folder called 'Gundam', and a subfolder named for the unit you're working on.  Take the folder with the clump of files, materials, and texture images you put together and copy it to the '\Tabletop-Simulator-Modding\Assets\Gundam\\[UNIT]' folder.  It's really important to keep the files for each unit separate, or it'll become a nightmare really quickly.

## Step 2: Import Settings
Go to the Assets folder in the project navigator on the bottom left and navigate to your unit folder.  Select each object you're planning to use, and make sure that the Read/Write Enabled option is checked in the inspector to the right.  If you click it on, make sure to Apply.  
![013 Read Write](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/78bfcade-0818-4cec-864f-9d588681d559)

## Step 3: Setup
Drag each object you want to use to the heirarchy window on the left, and make sure each one is set to position 0,0,0 (back in the inspector on the right).  Don't worry if the texture looks like it didn't make it, we're getting there.
![014 NewMat](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/b194fad1-d8fa-4dc4-a30a-a55a666c3f61)


## Step 4: Materials
Create a new material in the project folder.
![015 NewMat create](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/3cc02c4f-8a52-45bb-8d2c-b71cf4a076bc)

Name it something sensible, then drag your main texture map image to the Albedo map input (the little box to the left of Albedo in the inspector).  (If you've got emissive maps or bump maps or anything, here is where they get mapped as well.) 
![016 Mat to Albedo](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/7fc1c3d0-e733-4844-b299-27704fa53dd3)

Then drag the new material to each of the units you are using in the heirarchy.  If you don't like the shininess or glossiness or anything, here's where we can tweak some of those sliders to make it look how we like.  I tend to push metallic and smooth pretty down, I like the matte look it gets.
![017 Applied](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/018ea248-0b29-43f3-a6d6-e8655c348ae0)

## Step 5: Create Empty GameObject
Right click in the heirarchy and Create Empty.  Name it something sensible here, like the name of the unit or a serial number.
![021 Emptyness](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/77c339b1-b5de-4838-bec9-6c98c583182c)

It often comes in off center, so make sure it's relocated in the inspector.
![022 Centering](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/b6a93acb-8c31-4792-8177-1b6bb7d579e3)

Drag the objects from the heirarchy to the GameObject, making them child objects of the object.
![023 Together](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/6fb48747-6d33-4578-a813-cd95386b3e67)

## Step 6: Save
I tend to keep the save files in the Gundam folder rather than the asset folders, but it doesn't really matter.  Just save it.

## Step 7: Collider
With the GameObject selected, go to Add Component in the inspector, then pick Physics -> Box Collider.  I tend to get it pretty close to the body and legs sized, if you get too accurate it can slow things down and really make it hard to actually position the units.  In this case, I went with a 5x5x5 cube.  You need to make sure you shift the cube up to have the bottom at y=0 or you'll have all kinds of clipping headaches.  Just divide the Y height by 2 and move it up that much.
![024 Collider](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/01fa1c63-91b7-4f6c-af96-f94d197e7179)

## Step 8: Prefab
Almost there.  Add another component, this time a Script -> TTS Asset Bundle Effects.
![025 Bundle](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/9c9f93ac-d853-4e7f-a2a0-569c72395ea5)

Set the Trigger Effects to 0 for now, that's outside the scope of this tut.  Set Looping Effects to whatever number you plan on using - in this case, I'm using 3.  I name each one something meaningful, since that is what TTS will display as a tooltip when you hover over the options in game; Gun, Shield, Sword.  For each effect, I set the Game Objects Size to however many parts it uses.  Gun and Shield use 1 each, Sword uses 3 (I broke the blade up to use different texture maps).  Drag the appropriate child object of the game object from the heirarchy to the appropriate slot in the inspector.
![027 Parts](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/5f7952be-3eab-463c-b27a-4b189c53d475)

In the project navigator on the bottom left, go to Assets -> Examples -> Prefabs.  Drag your GameObject to the folder, and it should pop right in.  Select it, then go to the AssetBundle dropdown on the bottom right and give it a new name.  The first time you click New, it'll give you a blank area to type but won't respond.  Click on a different one, then back, then name it.  I dunno.  Make sure to use the unit serial number, all lowercase, dashes instead of spaces.  That'll make all of our lives easier later.
![028 Prefab Setup](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/70c8d8da-477e-4b53-87de-fa894a92c05c)

## Step 9: Save
Just do it.

## Step 10: Build AssetBundles
Right click in the Prefab folder and select Build AssetBundles.  Unity only builds the entire folder each time, so depending on how many you've made, it'll take some time.  Go to the TTS project folder, and go to AssetBundles.  It should be there, named msn-04-ii.unity3d (or whatever else, as appropriate).
![029 Prefab Build](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/1f370267-bafd-4a1b-92ea-fc44d5b347cf)

## Step 11: TTS Test!
Before you close out Unity, fire up TTS and create a solo game.  Add a Game Object, Component, Custom, AssetBundle.  Navigate to the unit unity3d file, and choose local storage.  We're just making sure it works.  It should load to the table, with the looping effect options we specified in the unity file.  Make sure each one looks the way you expect.  If it got messed up, double check your game object assignments in the Effects Script.  Otherwise, nice one!  On to the GitHub Repo.
![030 TTS custom asset bundle test](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/d0f8212d-5b70-467f-b984-06f0a9d8aeb2)

## Step 12: Optional Funnels, etc.
Take the funnel/whatever file and bring it in.  Create an empty as above, making sure it's centered, then arrange the funnel until it's right about centered on the unit itself.  Duplicate it several times, however many you need in a single group.
![031 Getting Funnels in place](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/53f55783-cad3-4e83-b172-1eba934135fd)

Arrange them in an artistic manner, keeping in mind it should stay centered on the MS in general, not in front of it.
![032 arranging](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/2bd8d871-39ac-4da7-adf3-cbadd62e8b9d)
![032a arranging](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/466cefe3-9e23-4cf5-8f96-11ec07d00113)

Add them to the empty, create a relatively small box collider, and create a script effect.  Make as many effects as you've got funnels, assuming you're using them as an HP counter or something.  I'd recommend starting with 1 funnel, then the second one being 2 funnels, etc.  It'll make it more natural when you're using the effects menu in game. Give each effect as many game objects as funnels, and then decide which ones go to which setting.
![033 Effects](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/2a44eb3c-bef2-48aa-8d4b-2843eb161b60)

Create and build a prefab, naming it [unit]-funnel.
![034 naming](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/fa19e17a-a0fe-4b8a-8792-2f099731c3f7)

Then test it in game.  You're done!
![035 success](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/27a64f38-12e7-4acc-a39f-68d96beffd4c)


[Back to top](https://github.com/ScornMandark/gundam-tts-assets/blob/main/Adding%20Assets/Importing%20Area%20Wars%20to%20Unity.md#navigator)

# Part 3: Unity to GitHub

## Make sure the faction has a folder
This should be pretty straightforward, since most factions should be set already.  If not, flag it as an issue and I'll get it set up.
[Double Check!](https://github.com/ScornMandark/gundam-tts-assets/)

## Upload the Bundle
Go to the universe/faction folder, then 'Add File -> Upload File'.  
![GitHub01Upload](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/68e6961f-0be5-40b3-8b6f-7d4b6e018fc1)
It will probably prompt you to create a Pull Request, which is what we want.
![GitHub02PullRequest](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/8175918e-61a9-40b4-9a22-31c663f677ee)

## Notes for the Pull Request
Please detail the model(s) you're uploading in the notes, with faction info as well.  When I merge the request, I'll update the MS menu to pick those units.

![GitHub03PullRequestSubmit](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/74c31fe3-c4d6-420b-8c7f-3fddabc07998)

## Final
Thanks for all your help growing this tool into new places!
![GitHub04EventuallySuccess](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/a0ff8207-9438-4fe2-871a-4721a77d34de)

## Unit Sheets
For MSSk sheets, I export each PDF page to a .png at 300 dpi (2481 x 3508, A4).  Then, go to the appropriate faction folder, go to the appropriate game folder, and add it as a file there.  As long as it's named exactly the same as the .unity3d model, no notes are needed, and I'll approve the merge request.

[Back to top](https://github.com/ScornMandark/gundam-tts-assets/blob/main/Adding%20Assets/Importing%20Area%20Wars%20to%20Unity.md#navigator)
