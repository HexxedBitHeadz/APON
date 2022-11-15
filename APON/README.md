# APON
Aromak's Pentesting Obsidian Notes <br />
***Hello and welcome!*** Please take a moment to finish this readme, as there is some really important things to go over.  Thanks!


## Important notes
***BE AWARE*** These are pentesting notes, therefore, will include malicious payloads and code!  Windows Defender will likely yell at you if these files are just downloaded.  Either setup in a Unix environment, or consider using an excluded space from antivirus for these notes on Windows.

The best way to use these notes is just how I demo'd, with Obsidian Notes or similar markdown tool.  There are already fantastic tutorials online for this tool, so I will not go over the basic usage, however, I will go over some configurations I set up within. 

- Settings > Editor > Readable line length
  - I disable this feature.  Having it enabled puts these large margins on the sides of your notes.

- Settings > Files & Links > Default location for new attachements
  - Set this to "In the folder specificed below".

- Settings > Files & Links > Attachement folder path
  - Set this to "zz._attachments".  This will now put any screenshots or other attachments out of the way, in 1 folder, instead of scattering them into whatever working directory you are currently in.
  
- Settings > Community plugins > Browse
  - I try to stay away from any plugins, but 2 I have to have are:
    - "Clear Unused Images", deletes all images that are no longer being used in your notes.
    - "Dangling links", exposes dead links in your notebook, you can either update correctly or remove.

- Ensure your file / folder sort order is set to "File name(A to Z)"

How to get the most out of this resource?
Every new engagement starts at 1._Pentesting_Setup > __.Steps > Assigning IP Variables.

This section is meant to set you up for the rest of the notebook.  Here, we assign the Kali IP to the variable KALI (pay attention to the network interface used), and then assigns the target IP to the variable TARGET.  We do this so that moving forward, we can utilize the power of variables and copy / paste scripts and commands faster and easier.  For example, for all of your nmap, msfvenom, etc commands are ready to go, no more manually entering IP address!


## Contact info
HexxedBitHeadz@gmail.com  <br />
