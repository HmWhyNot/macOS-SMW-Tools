asar 		by Alcar
GUI/Addon 	by JackTheSpades

Version 1.00

A simple tool which can be used to apply ASM patches with asar, but instead of the command
line interface, it provides a GUI.
This tool can function as both, stand alone and Lunar Magic addon, though honestly, there is
not much point in using it as stand alone instead of the CLI, as you have to go through more steps
whereas the CLI you can just drag drop the files into it. So, better use it as addon :P

---------------------------------------------------

How to addon?
Dump Asar Addon.exe and asar.dll in some folder you don't care about, where it isn't in the way.
Like C:\Programs or something.
I personally made a subfolder where I keep Lunar Magic.

Go to the folder where you keep "Lunar Magic.exe" and create a file called "usertoolbar.txt" (minus quotes)
In that file, put the following text:

***START***
LM_SPACER
***START***
"path to asar addon.exe, keep the quotes" "%1"
0,Asar Addon to apply ASM patches
LM_CLOSE_ON_CLOSE
'a',VK_CONTROL
***END***

This will add the addon to your toolbar and asign the combination CTRL+A to start it. Seek Lunar Magic's help file for more information on how to handle custom toolbars.

---------------------------------------------------

What to concider?
When using this, you should always patch right after opening it.
That is to say, don't open it, make edits to your level and then apply a patch, as it will overwrite
all changes made after it was opened.

The tool creates a file called ROMNAME.pda where your ROM is, DO NOT delete this file, it is
where a list of all inserted patches and the bytes they changed is stored.
If you lose this file, restoring will become impossible (at least using the tool)

Note, this tool has not been tested on SA1 roms. As far as patching is concerned, everything should
work just like the normal command line version, however, all the other features such as collision detection
and removing/exporting of patches, is to be handled with care.

---------------------------------------------------

What does it do for me?
It applies patches (duh) and keeps track of all the changes it did to the ROM.
Not, it only registers actual changes. If you apply a patch that uses 100 bytes of freespace but
only writes $00 to all of them, it will not recognice the changes, it will only list 8 changed bytes
(The RATS tag).

It warns of collisions with already installed patches.
In this case, patching should be aborted (you have the option to contineu) as it will mess up both your ROM
and the tools tracking.

It allows to remove patches. For this it uses the sysLMRestore clean ROM. If you do not have the restore ROM,
you'll have to point it to a clean ROM when it asks you to.

You can export all your patches to an ASM file. This is tricky, as the tool is unaware of the mapping you ROM
uses, it simply exports the data with their PC address.
So, if you export your edits as an ASM, make sure to only apply it to ROMs that use the same mapping type
(eg, don't apply something you exportet from an sa1 ROM to one that uses lorom (default))