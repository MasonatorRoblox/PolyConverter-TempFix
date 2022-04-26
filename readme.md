# PolyConverter

This small program will convert Poly Bridge 2 level files (from the Sandbox or from regular bridges)
into an editable text format.

It will be helpful if you need to merge layouts together, or edit parts of your level
that can't normally be edited, such as object depth (Z coordinate).


### How to use

- Extract the 'polyconverter' folder inside the .zip to your Sandbox folder.
- Download .NET from https://dotnet.microsoft.com/download/dotnet/3.1/runtime (Click "Download x64" under the "Run console apps" section). Without this, PolyConverter will never open (Yes, I know, it's quite a lot more work than just using a single .exe, but at least this works).
- Edit the gamepath.txt folder in the 'polyconverter' folder to match the filepath of where the game is installed. Make sure to end the filepath at Poly Bridge 2 (Example: D:\SteamLibrary\steamapps\common\Poly Bridge 2).
- Place any files (.json, .slot, or .layout) you want to convert inside the 'polyconverter' folder 
- When you run it, the .layout and .slot files will be converted into .json files.  
- With the console window still open, if you press Enter to run the program again, all the changes you made in the .json files
will be applied to the .layout and/or .slot files (or vice-versa).
- A backup of the original file (before any changes) will be created if one doesn't exist.  
- You can keep applying new changes as many times as you want without having to close the window by pressing Enter.



# Explanations:
- If you try opening a .slot or .layout file in any text editor, it will show a lot of strange and missing symbols, instead of the actual code. However, this program converts it into a .json format that you can actually read and edit, and it's much easier to read than you'd think.

### Settings for Both File Types
- The "m_Version" setting doesn't control much, and there isn't really any point in editing it. However, PolyTech mods change this number into a negative if you save any mod data to the file, which makes it unopenable to anyone without PolyTechFramework enabled.
- "m_BridgeJoints" will have data inside the [] if the layout or slot was saved with pieces placed (Note that the first appearance of this setting may be empty, but there can still be a different m_BridgeJoints below). These will be formatted as { "m_Pos": { "x": [#], "y": [#], "z": [#] }, "m_IsAnchor": <true/false>, "m_IsSplit": <true/false>, "m_Guid": "<randomized-string-of-letters-and-numbers>" }. Most of these are self explanatory, except for "m_Guid", which is simply a random set of letters and numbers that give each joint something unique to be identified by. Changing the guid will likely cause problems due to the bridge pieces refrencing the joints by their guid.
- "m_BridgeEdges" contains data for every material you have placed (Note that the first appearance of this setting may be empty, but there can still be a different m_BridgeEdges below). It will be formatted as { "m_Material": [1-7,9], "m_NodeA_Guid": "<randomized-string-of-letters-and-numbers>", "m_NodeB_Guid": "<randomized-string-of-letters-and-numbers>", "m_JointAPart": [0/1], "m_JointBPart": [0/1] }. This may differ slightly with three-way split joints. "m_Material" determines the material of the beam, with 1 being road, 2 being reinforced road, 3 being wood, 4 being steel, 5 being hydraulics, 6 being rope, 7 being cable, and 9 being springs (8 is a scrapped material that was removed before release, and is a combination of springs and rope. There is actually a PolyTech mod that adds this back into the game!). "m_NodeA_Guid" and "m_NodeB_Guid" tell the game which two joints this beam is connected to.
- "m_BridgeSprings" contains the settings for each spring in your bridge, and is formatted as { "m_NormalizedValue": [0.000-1.000], "m_NodeA_Guid": "<randomized-string-of-letters-and-numbers>", "m_NodeB_Guid": "<randomized-string-of-letters-and-numbers>", "m_Guid": "<randomized-string-of-letters-and-numbers>" }. "m_NormalizedValue" simply holds the stretch/compress value of the spring, and the rest of the settings are the same as explained before.
- "m_Pistons" contains the settings for each hydraulic in your bridge, and is formatted exactly the same way as "m_BridgeSprings" is. "m_NormalizedValue" controls the expansion/contraction, with 0 being -50% and 1 being +50%.
- "m_HydraulicsController" contains the data for hydraulics in each hydraulic phase. I am too lazy to paste the formatting here.
- "m_Anchors" contains joint data for each red anchor point.
- "m_ZedAxisVehicles" conntains data for each boat/plane type vehicle, and is formatted as { "m_Pos": { "x": [#], "y": [#] }, "m_PrefabName": "<name-of-vehicle-as-refrenced-in-the-code>", "m_Guid": "<randomized-string-of-letters-and-numbers>", "m_UndoGuid": null, "m_TimeDelaySeconds": [#], "m_Speed": [#] }. The settings are self-explanatory.
- "m_Vehicles" contains the data for anything that drives on land, and is formatted as { "m_Pos": { "x": [#], "y": [#] }, "m_DisplayName": "", "m_Rot": { "x": [#], "y": [#], "z": [#], "w": [#] }, "m_PrefabName": "<name-of-vehicle-as-refrenced-in-the-code>", "m_TargetSpeed": [#], "m_Mass": [#], "m_BrakingForceMultiplier": [#], "m_StrengthMethod": [#], "m_Acceleration": [#], "m_MaxSlope": [#], "m_DesiredAcceleration": [#], "m_ShocksMultiplier": [#], "m_RotationDegrees": [#], "m_TimeDelaySeconds": [#], "m_IdleOnDownhill": <true/false>, "m_Flipped": <true/false>, "m_OrderedCheckpoints": <true/false>, "m_Guid": "<name-of-vehicle-as-refrenced-in-the-code>", "m_CheckpointGuids": [guid's-of-checkpoints-this-vehicle-has], "m_UndoGuid": null }


### Layout-Only Settings
- "m_ThemeStubKey" controls the theme of the level. One thing to note is that some theme names may differ from those of the world they are in. For example, Pine Mountains is called PineMountains, Glowing Gorge is Volcano, Serenity Valley is Savanna, Sanguine Gulch is Western, Serenity Valley is ZenGardens, and Steamtown is Steampunk.

### Slot-Only Settings
