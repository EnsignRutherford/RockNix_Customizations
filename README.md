# RockNix Customimzations

This is an autostart script written for the Retroid Pocket 5 version of RockNix which adds some customizations and fixes that are not part of the main code branch.

When executed at startup it performs these steps:

1. Copies the last systems config for EmulationStation over the existing one.  Makes a backup of the original.  
2. Mounts a new `theme.xml` over the existing one fixing an issue with customization of new systems that aren't in the base theme.  This seems to be a unique issue to the Retroid Pocket 5
3. Add "Start Eden" emulator to Tools menu with an image and edit the `gamelist.xml`
4. Copy missing cores from the base install of RockNix to `/tmp/cores`, IF they don't exist.

If the supporting files do not exist in the `CUSTOMIZATIONS_HOME` folder nothing happens.