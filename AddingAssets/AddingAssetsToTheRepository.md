# Adding Assets to the Repository

Now that you've got your fresh and tested AssetBundle ( [detailed here](https://github.com/ScornMandark/gundam-tts-assets/blob/main/AddingAssets/AddUnityAssetBundling.md) ), now it's time to get it into the repository for Haro to create.

## Make sure the faction has a folder
This should be pretty straightforward, since most factions should be set already.  If not, flag it as an issue and I'll get it set up.

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
Make sure your unit sheet is padded with transparency to be square.  For MSSk sheets, for example, I export each PDF page to a .png at 300 dpi (2481 x 3508, A4), then pad the sides with transparent pixels so that each image is 3508 x 3508 (GIMP, ImageMagick, etc).  Then, go to the appropriate faction folder, go to the appropriate game folder, and add it as a file there.  As long as it's named exactly the same as the .unity3d model, no notes are needed.
