MAKE YOUR OWN WEAPON MOD USING CUSTOM MODEL


=========================================================================================
===I STRONGLY recommend reading this file using Visual Studio Code instead of notepad.===
=========================================================================================

(sorry if the guide is a bit messy, I am new to this tutorial making thing. if you have any suggestions leave them on template's nexus page, I appreciate feedback)

Software needed:
================

1. VS Code - IDE (text editor for programmers), you will need it for editing the mod's files (infinitely better than notepad++) - https://code.visualstudio.com/

2. Blender - For editing the weapon model - Get it from Steam or it's Official website - https://www.blender.org/

3. Collada Exporter for Blender 3.6 - To be able to export/import GR2 files using Blender - https://github.com/Norbyte/dos2de_collada_exporter (follow the tutorial on the github page for installation)

4. LsLib - Needed for the Blender plugin, has some other functions, but I don't use it - https://github.com/Norbyte/lslib

5. BG3 Modder's Multitool - Used for generating UUIDs and Handles, Packing/Unpacking mods and searching through the game files - https://github.com/ShinyHobo/BG3-Modders-Multitool

6. Some image editing software (I use Gimp and PaintDotNet)




Other tools:
===================
1. BG3 modding wiki - https://bg3.wiki/wiki/Category:Modding

2. BG3 Creator's Cauldron - "Lists" file - https://www.nexusmods.com/baldursgate3/mods/1808?tab=files
The "lists" file has some info about the spells, boosts, weapons, etc. which is handy when working with Weapon.txt 


Basics:
=========
Handles and UUIDs
- Handles are used in localization, they are used of the in-game text
- UUIDs are used to connect stuff between files and to make certain thing unique


BG3 cares a lot about your textures and models having the right format.
- Textures have to be .DDS not .dds
- Models have to be .GR2 not .gr2
(it won't work otherwise)


BG3 Modder's Multitool thing
- There are many files that have formats like .loca or .lsf that you cannot edit directly.
To work around this, you can call the files .loca.xml and .lsf.lsx so that you can edit them (I already did that in this template btw, just make sure not to change it).
Multitool will automatically convert those files to correct format when packing (.loca.xml ---> .loca   and   .lsf.lsx ---> .lsf).




Folder explanation:
===================

Mod Folder
	- Generated\Public\Shared\Assets\Weapons\Resources\
		- ModName
			- .GR2 (model) and .DDS (textures)
	- Localization
		- Language (Usually English)
			- .loca.xml file (Multitool automatically converts it to .loca when packing) - text that actually shows in-game is in this file
	- Mods
		- ModName
			- meta.lsx - basic info about your mod (for the game and mod manager)
	- Public
		- Game\GUI\Assets\
			- ControllerUIIcons		<--    	Your weapon icons
			- Tooltips\ItemIcons	<--		Your weapon icons
		- ModName
			- Assets
				- Textures
					- Icons
						- ModNameIcons.DDS File (your Icons)
			- Content
				- [PAK]_ModNameResource (dont forget to change the ModName part)
					- _merged.lsf.lsx <--- Loads the weapon model and weapon textures into the game (Multitool automatically converts it to .lsf when packing)
				- UI
					- [PAK]_UI
						- _merged.lsf.lsx <--- Loads the icon into the game (Multitool automatically converts it to .lsf when packing)
			- GUI
				- Icons_ModName.lsx <-- defines chunks of the ModNameIcons.DDS file in Assets\Textures\Icons\ (allows you to have multiple icons in single image file)
			- RootTemplates
				- _merged.lsf.lsx <-- defines your weapon's root template (stuff like in-game name and description, visual template (model) and more)
			- Stats
				- Generated
					- Data (The file name inside this folder is not important)
						- Weapon.txt <-- New items are created here (just check the file it's self explanatory)
					- TreasureTable.txt <-- Puts your weaon into in-game world (traders, chest's and so on)




My work flow:
===================
I usually make mods in 3 phases


1. Renaming - changing all the UUIDs that need to be unique, changing mod name, changing localizaiton and handles

2. Importing the model - Converting my model to GR2 format using the blender plugin (use the GR2 I added into generated folder as a base to get the position and rotation of your model right)

3. Changing stats - Here I just change the stats and item name in Weapon.txt, add passives, modify TreasureTable.txt


Step by step:
==============
1. Start by renaming the folders called ModName to whatever you want your mod to be called 
this is not visible to users, only to you, but it has to be unique from other mods so I recommend starting with your initials (for example: P33_YourModName)

2. Rename individual files within the folders (Replace ModName withing their names) - ModNameIcons.DDS ---> P33_YourModNameIcons.DDS
 
3. Open all the files in visual studio (Localization, Meta, all the files in public)

4. Modify the files based on instructions within
- Start with meta as it's the most important
- When Changing UUID/handle or replacing the "ModName" make sure to highlight it and click ctrl+F (Watch tutorial video 1 to see how, if you are unsure)
- You can generate UUIDs and Handles using multitool (to generate handles click the box next to the generate button)

4.5. Playtest
- I usually playtest once am done with this part, to make sure that mod works as intended

5. Import model
- To do this, follow the tutorial videos 2, make sure that _merged.lsf in "Public\ModName\Content\[PAK]_ModNameResource" is filled out correctly (texture names and paths, model and mesh name... according to stuff I wrote there)
- I usually import model, then playtest, then import textures and create material, then playtest again.

6. Pack the mod and play test it
- When packing the mod using multitool make sure you tick the "Pack .paks to Mods folder instead of zipping" square, make sure to enable the mod in mod manager like you do with other mods.


Trouble-shooting:
==================
If you have problem, check the wiki, spend five hours trying to fix it (I do this too often) or ask people on larian studious discord (in the modding channel).

