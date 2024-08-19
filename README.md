# SBQ-Dialogue
A repository meant for public contributions of dialogue or translations of dialogue for the Starbecue mod

Download this repository and place in mods folder alongside Starbecue for it to overwrite/add on to text within Starbecue. The version of Starbecue it was last updated for will be the version in the metadata, It likely is compatible with future versions as long as no major changes to dialogue have occurred.

If being used for translations, a branch will be created for each language seperately.

All `.config` `.dialogue` and `.dialogueTree` files are to be read as UTF-8 JSONC, however, SBQ-Engine lets Starbound's Json parsing allow trailing commas.

Do not change the keys or things will not work! only change the values!

Most SBQ text strings will print their key with a preceding colon `:` in place of their value if it is missing from the file.

## Gui Strings
The bulk of GUI player facing text is contained in a single file `sbqStrings.config`

## NPC Dialogue Strings
The Base NPC dialogue is located at `npcs/sbq/dialogue/default.dialogue` other personality variants are in the same folder.

OC NPC dialogue is located at paths `npcs/sbq/(Owner)/(OC Name)/npc.dialogue`

Unless you are adding in dialogue for unused/unimplemented dialogue triggers, you will not need to modify the `.dialogueTree` file for the respective dialogue! There should be no player facing text contained in the tree, if there is, it should be moved into the dialogue file and the entry in the tree should be replaced with a reference.

After making any dialogue changes it is reccommended to at the very least run the dialogue verification script before pushing a commit. (If you don't understand how to, thats fine)

# Scripts
I have included three utility scripts I use for doing bulk work, mainly sort or verify one's work is correct.

### Dependencies
- https://nodejs.org/en/download
- https://www.npmjs.com/package/comment-json

## Sort Dialogue
`node sortDialogue.js  (path to .dialogueTree)  (path to .dialogue)  (opt base .dialogue file)`

Is used to read a dialogue tree and paired dialouge file, sorting it's contents by where it is used in the dialogue tree, noting any instances the dialogue tree references a piece of dialogue that is missing, as well as putting unused pieces of dialogue at the bottom of the dialogue file.

One can supply a third optional argument for a secondary base dialogue file to reference and point missing lines to rather than simply noting they are missing. Most useful when working on personality variant dialogue, and simply using the default as a base to use for missing lines.

## Verify Dialogue
`node  verifyDialogue.js`

Is used to verify all dialogue is valid, contain no circular reference loops, and that duplicate instances of the same group of dialogue lines are instead a reference to the first unique instance. Will note if there are any missing pieces of dialogue that are being referenced.

The script is preloaded with a list of dialogue files to check and verify, if more dialogue is being added, just add it to the list inside it.

## Un-Reference Dialogue
`node  unReferenceDialogue.js`

Simply goes through its list of dialogue files, and replaces paths used to reference dialogue elsewhere in the file or in other files, with just the group of text being referenced.

I simply use this to make writing an individual character's unique dialogue easier while still being able to look at the base dialogue as an example, I reccommend always running the verify script once more afterwards.
