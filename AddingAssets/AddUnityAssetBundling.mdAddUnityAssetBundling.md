# Bundling 3d models into UnityAssetBundles for Tabletop Simulator

If you have your 3d models set up, positioned and scaled properly ( [as detailed here](https://github.com/ScornMandark/gundam-tts-assets/blob/main/AddingAssets/3dModelPrepInstructions.md) ), then we're ready to start the unity import process.

# Things you'll need:
- One or more 3d models set up for import as .obj or .fbx
- [Unity version 2019.1.14f1](https://unity3d.com/unity/whats-new/2019.1.14) (other 2019.1 releases may work with the 3.0 mod release, but this is the one that works for me)
- [Berserk Games TTS project for Unity v3.0](https://github.com/Berserk-Games/Tabletop-Simulator-Modding/releases/tag/v3.0) (there's a newer update that I haven't tried yet, and I'll update this once I do), but this one works)
- More patience...

# Step 0: Follow the TTS Unity tutorial
[TTS Custom AssetBundle Walkthrough](https://kb.tabletopsimulator.com/custom-content/custom-assetbundle/) This will walk you through the whole process of installation, project folder finding, making a basic asset, and getting it into TTS.  If you can finish the tutorial, you'll be nearly there, honestly.

# Step 1: Organizing
Now that the project opened nicely, we need to set up some files.  In the 'Tabletop-Simulator-Modding\Assets' folder, make a new folder called 'Gundam'.  Take the folder with the clump of files, materials, and texture images you put together and copy it to the '\Tabletop-Simulator-Modding\Assets\Gundam' folder.  It's really important to keep the files for each unit separate, or it'll become a nightmare really quickly.

# Step 2: Begin
In Unity, in the Heirarchy tab on the left, right click and 'Create Empty'.  Rename the new GameObject however you want, but I like to use the name of the unit.  
![Unity02CreateEmpty](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/eaf16577-f177-4169-86b0-3f9aedeaf019)

On the right hand side, in the Inspector tab, reset the Position Transforms to X = 0, Y = 0, Z = 0.  Make sure the Rotations are all 0 as well, and the Scales are all 1.

![Unity03ResetTransforms](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/61897bc0-e8ef-47a6-ab15-897ab5a67842)

# Step 3: Bring in the models
Now that we've got the structure set up, we can bring in the models.  In the bottom left Project tab, scroll down to the 'Assets\Gundam' folder, then to the unit folder you copied in.  Each model in that folder will have a little thumbnail image with a small arrow pointing to the right.  That arrow expands the file structure to show the mesh, materials, etc.  
![Unity04LocateFiles](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/163040fc-bc78-48ff-b3eb-2664584cef52)

Drag the main thumbnail of each model you want to use onto the GameObject Empty object you created in the last step.  You should see the name of the object pop into the window as a child object, and the mesh itself should show up in the Scene window.  Repeat for all models, but not the collider.

# Step 4: Alignment
Most of the time the objects you bring in aren't at 0,0,0 either, so for each model, select it in the Heirarchy tab, then in the Inspector tab reset the transforms like you did for the empty object.

# Step 5: Collider
Select the parent empty object again and go to the Inspector tab.  Below the Transforms, click 'Add Component', select 'Physics' then 'Mesh Collider'.  
![Unity06Collider](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/2af7ce7d-f8dd-4b41-875a-591054c4e6af)

In your project folder, expand the Collider box you made.  The third item in the list should look like a plain grey box with trianglulated sides, called 'default'.  Drag that object to the Mesh Collider tab and drop it in the box for the 'Mesh' (curretly labeled 'None (Mesh)').  (You can check Convex if you want - it speeds up colliding calculations, but it's not really necessary with a box collider.)  Alternately you can create a simple box in Unity itself.
![Unity06aColliderMesh](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/ab3e9667-86e2-4d60-8553-f21962e070d9)

# Step 6: Textures (optional, or if illumination needed)
I often try to remap the objects to use a single material texture - it cuts down the file size pretty decently.  Also, if you want any kind of self illumination, you'll need to do this.  Create a new material in the project folder, call it whatever you want.
![015 NewMat create](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/d36392a8-73c7-4a95-ba72-1cfc4d29f980)

When you have a material created, drag the texture material to the albedo map input (the small box to the left of Albedo).
![016 Mat to Albedo](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/76b19bc4-a153-449d-94a2-ed8b59e403f5)

Then just drag said material to the MS of your choice.
![017 Applied](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/1bd70b7e-35d1-43a5-8454-995d25f764ab)


If it looks really dark, you may need to rotate the light in the scene from Y = -30 to Y = +150.
![Unity05bRotateLight](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/e115a2c3-fc19-4503-b4fd-683a0fbb7ca7)

Here's where you can adjust options like metallic and smoothness to get the sheen and finish you want.  I tend to make it very low smoothness and metallic to get a nice matte finish, but up to you!  If you create a glow map (just isolate the glowing parts on the texture map and really darken the rest, save as a new file), then just select Emission active and use the glow texture as the map input to Emission.  There's some tricks to get transparency active, but short answer is that it's really tricky.

# Step 7: The Options
Here's where we set up the model for use (and multi-pose if you've got it).  Under the 'Mesh Collider' box, click 'Add Component', select 'Scripts' then 'TTS Asset Bundle Effects'.  It will have 2 options - Bundle Effects and Trigger Effects.  
![Unity07ScriptEffects](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/04c86cd9-f78f-4c9a-97de-406b193f9168)

- For now, set 'Trigger EFfects -> Size' to 0.  
- Set 'Bundle Effects -> Size' to however many poses you have and hit Enter.  It can be 1, it can be at least 40, so go to town.  
- - Each 'Element' will need to be given a name.  I tend to name each one after the option displayed ("Beam Rifle", "Machine Gun", "Bazooka", "Chobham + Beam Rifle", etc).  The name will be a tooltip that shows when you hover over each effect option.
- - Each 'Element/Game Options' will need to be set to 1 if each of your meshes are combined alraedy, then press enter.
- - Each time you set a Game Option to 1, a new entry in the tree opens for 'Element #/Game Object' with a box next to Game Object.
- - Drag the 'default' object from each model in the heirarchy to the appropriate Element (you did remember to name them all sensibly, right?)

![Unity07aScriptEffectsExample](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/eab591d5-9f2d-4172-895d-4af15af91a18)

# Step 8: Save
If you haven't already, save the file.  (It'll be a .unity file.)

# Step 9: Asset Bundle
In the Project tab, go to 'Assets\Examples\Prefabs'. Drag the parent GameObject into the Prefabs folder in the Projects tab, and you'll see an preview icon pop up there.  In the Inspector tab to the right, go to the bottom tab "Asset Label".  Open the AssetBundle dropdown under the 3d preview, and select 'New'.  Then, name it in numbers and lower case letters only, no spaces, only hyphens and underscores as special characters.  I tend to use serial numbers when available, like msn-03, gat-x-105, etc.  You can't use brackets or slashes, so I either just remove them or turn them into hyphens.  Then, right click in the Prefabs project window, and select 'Build AssetBundles'.  This can take a while, since you can't selectively build one asset, Unity rebuilds all the AssetBundles in the folder.  As far as I can tell, having them in sub folders doesn't help.  
![Unity08AssetBundle](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/ce1009e0-b969-4509-8692-135511ad912c)


# Step 10: Fresh AssetBundle
In your file structure, the new AssetBundle will be in the 'Tabletop-Simulator-Modding\AssetBundles' folder, named whatever you labeled the asset in the previous step.  Something like 'gx-9901-dx.unity3d'.  
![Unity09FreshAssetBundle](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/3451e44f-27f7-4b77-82f5-2e5a83e5939b)

Now it's ready to be imported to TTS!  Go ahead and open TTS, start a game.  Click 'Object', then 'Custom', then 'Asset Bundle'.  Place the cube somewhere, then hit escape to stop placing.  A menu will pop up:
- Main: select the .unity3d file you just made!
- - I usually select local storage for this test, since it's just a test.
- Secondary: usually not needed.
- Type: I usually use figurine, so it stands back up when you pick it up.
- Material:  Doesn't matter too much, I use plastic most often.

Now test it out!  It should just show one pose.  Right click on it, and check the 'Looping Effect' option.  It should show one or more options, with a mouseover tooltip.  Selecting each option should insta switch it to a different mode/equipment.  Hopefully it works the first time!  If not, my usual problem is assigning the wrong model in the Effects modifier.  Trace back to the step where you need to fix it, then repeat the rest of the steps to make sure it works again.
![Unity10PartyOn](https://github.com/ScornMandark/gundam-tts-assets/assets/7913700/46ae1d92-a46f-4f2f-b3b4-2011d0cd1806)

After it's all set, [then it's time to get it into the repository.](https://github.com/ScornMandark/gundam-tts-assets/blob/main/AddAssets/AddingAssetsToTheRepository.md)

NOTE:  Unity Asset Bundles are intensely powerful tools, with motion triggered animations, looping idle poses, particle effects, and more.  I just scratched the surface here.

