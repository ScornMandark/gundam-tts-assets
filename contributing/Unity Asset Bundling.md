# Bundling 3d models into UnityAssetBundles for Tabletop Simulator

If you have your 3d models set up, positioned and scaled properly ( [as detailed here](https://github.com/ScornMandark/gundam-tts-assets/blob/main/contributing/3d%20Model%20Prep%20Instructions.md) ), then we're ready to start the unity import process.

# Things you'll need:
- One or more 3d models set up for import as .obj or .fbx
- [Unity version 2019.1.14f1]{https://unity3d.com/unity/whats-new/2019.1.14} (other 2019.1 releases may work with the 3.0 mod release, but this is the one that works for me)
- [Berserk Games TTS project for Unity v3.0](https://github.com/Berserk-Games/Tabletop-Simulator-Modding/releases/tag/v3.0) (there's a newer update that I haven't tried yet, and I'll update this once I do), but this one works)
- More patience...

# Step 1: Installation
First thing is to make sure you've got Unity installed, then you can download the project file for the TTS mod.  The project isn't installed, just put it somewhere you can find it easily.

# Step 2: Opening The Project
Open Unity, and then open the TTS project.  In 'File -> Open Project', go to the folder that the TTS project file unzipped to.  So for me, that might be 'Z:\Gundams\Tabletop-Simulator-Modding\' - not a particular file, just the folder.

# Step 3: Organizing
Now that the project opened nicely, we need to set up some files.  In the 'Tabletop-Simulator-Modding\Assets' folder, make a new folder called 'Gundam'.  Take the folder with the clump of files, materials, and textures you put together and copy it to the '\Tabletop-Simulator-Modding\Assets\Gundam' folder.  It's really important to keep the files for each unit separate, or it'll become a nightmare really quickly.

# Step 4: Begin
In Unity, in the Heirarchy tab on the left, right click and 'Create Empty'.  Rename the new GameObject however you want, but I like to use the serial number or name of the unit.  On the right hand side, in the Inspector tab, reset the Position Transforms to X = 0, Y = 0, Z = 0.  Make sure the Rotations are all 0 as well, and the Scales are all 1.

# Step 5: Bring in the models
Now that we've got the structure set up, we can bring in the models.  In the bottom left Project tab, scroll down to the 'Assets\Gundam' folder, then to the unit folder you copied in.  Each model in that folder will have a little thumbnail image with a small arrow pointing to the right.  That arrow expands the file structure to show the mesh, materials, etc.  Drag the main thumbnail of each model you want to use onto the GameObject Empty object you created in the last step.  You should see the name of the object pop into the window as a child object, and the mesh itself should show up in the Scene window.  Repeat for all models, but not the collider.

# Step 6: Alignment
Most of the time the objects you bring in aren't at 0,0,0 either, so for each model, select it in the Heirarchy tab, then in the Inspector tab reset the transforms like you did for the empty object.

# Step 7: Collider
Select the parent empty object again and go to the Inspector tab.  Below the Transforms, click 'Add Component', select 'Physics' then 'Mesh Collider'.  In your project folder, expand the Collider box you made.  The third item in the list should look like a plain grey box with trianglulated sides, called 'default'.  Drag that object to the Mesh Collider tab and drop it in the box for the 'Mesh' (curretly labeled 'None (Mesh)').  (You can check Convex if you want - it speeds up colliding calculations, but it's not really necessary with a box collider.)

# Step 8: The Options
Here's where we set up the model for use (and multi-pose if you've got it).  Under the 'Mesh Collider' box, click 'Add Component', select 'Scripts' then 'TTS Asset Bundle Effects'.
