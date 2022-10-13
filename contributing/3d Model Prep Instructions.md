# Getting 3d models ready to bundle

If you want to add models to the repository, I'd love your help!  Here are the basics of getting some models ready to build into a Unity Asset Bundle, which will be a separate how to.

## Things you'll need:
- 3d model of a mobile suit.  If it's got multiple weapon options or modes, having those as well will help!
- Blender (or other 3d modeling program, I'll use Blender as a reference though.)
- Patience...

## Step 1: Import your model into Blender.  
Blender can import a wide variety of file types, and most of the 3d models you come across are either in .obj or .fbx format.  Blender can import these directly, just go to File -> Import -> [filetype]

## Step 2: Reorient.
Different models come in oriented differently, but usually aligned to the x-y-z axes pretty well.  We need our models to have the top pointing at the Z+ axis, and facing the Y- axis, with the bottom of their feet at Z=0.  The basic grab and rotate functions will make this straightforward.  (if you have multiple poses, import them all before you reorient, then you can do them all at once.)  After it's oriented properly, Apply the transformations.

## Step 3: Check the scaling.
Many 3d models come in 1:1000 scale - that is, an 18m Gundam will be 18 Blender Units high (which is usually associated as mm).  Once the model is imported and reoriented, check the Z height of the model.  If it's about right, then we're good.  If not, then a quick scale will fix it.  Divide the suit height by the z height to find your new scaling factor.  e.g., if the imported height is 36, and the Gundam is 18, 18/36 = 0.5, and just scale all the imported models by 0.5.

### Step 3a: Posing.
If you've got a single rigged model, you can duplicate it and pose each one separately.  I highly recommend this as opposed to posing, exporting, reposing, reexporting, etc.

## Step 4: Check the textures.
Unity/TTS require each object to have a single texture map, preferably square.  If the model has separate color, bump, and emmissive maps, even better.  If not, you'll need to do some texture manipulation and remapping.  Usually it's combining the separate color textures into a bigger square one, then scaling the UV maps and shifting them around.  

## Step 5: Make a basic collider box.
Create a cube, then scale it until it's bottom is at z=0 and it covers the main part of the body.  You don't need to get too crazy here, just a basic block is fine.  In fact, the more accurate the collider is, the more trouble you'll probably have placing it on the board.  We just need something to keep it from falling throught the table.

## Step 6: Export.
You can export as either .obj or .fbx, Unity can handle either.  I like using .obj, but it's up to you.  Export each model separately (don't forget the collider), naming each one so that you can tell what it is on import.  The important parts here are make sure 'Include -> Selection Only' is checked, and 'Transform -> Scale' is set to 0.273.  This will make sure you're only exporting one pose per .obj, and it is pre-scaled to 1/144 in inches in TTS.

## Step 7: Head to Unity.
Head to Unity for [the bundling process.](https://github.com/ScornMandark/gundam-tts-assets/blob/main/contributing/Unity%20Asset%20Bundling.md)
