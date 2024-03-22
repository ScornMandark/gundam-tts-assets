Used TTRPDFToJPG3_2_Windows to batch convert pdf cards to png.
3x scale, png export, separate folder

Removed duplicate card backs from most horizontal cards (Core, Support, Upgrades)
Vertical cards do not have duplicate backs (Characters, Stat)
Used Powershell to batch rename files in each folder [ref]$i = 1; gci -file | Rename-Item -NewName {'{0:D}.png' -f $i.Value++, $_}
