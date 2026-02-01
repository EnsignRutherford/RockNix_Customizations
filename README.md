# RockNix Customimzations

This is an autostart script written for the Retroid Pocket 5 version of RockNix which adds some customizations and fixes that are not part of the main code branch.

When executed at startup it performs these steps:

1. Copies the last systems config for EmulationStation over the existing one.  Makes a backup of the original.  
2. Mounts a new `theme.xml` over the existing one fixing an issue with customization of new systems that aren't in the base theme.  This seems to be a unique issue to the Retroid Pocket 5
3. Add "Start Eden" emulator to Tools menu with an image and edit the `gamelist.xml`
4. Copy missing cores from the base install of RockNix to `/tmp/cores`, IF they don't exist.

If the supporting files do not exist in the `CUSTOMIZATIONS_HOME` folder nothing happens.

## Cores

The repo's customizations script is meant to automate a large part of this process, as installing updates to RockNix will break/wipe out some of the changes and require re-applying them. If you don't intend to update frequently or would like to try out individual cores, you can install them manually using this process:

1. Set up your RockNix device to allow remote access by SSH/SFTP.
2. Copy the desired core(s) from this repo to `/tmp/cores` using your preferred method.
3. SSH into the device and use `chmod +x` to make the cores executable.
4. Find the file `/storage/.emulationstation/es_systems.cfg`. It's a symbolic link -- download a copy of the target file from your RockNix device to your other device to edit, and remove the symlink using `unlink /storage/.emulationstation/es_systems.cfg`.
5. Update your copied `es_systems.cfg` to add the core(s) you would like to use, link this example using Puzzlescript:
   ```xml
    <system>
        <name>puzzlescript</name>
        <fullname>PuzzleScript!</fullname>
        <path>/storage/roms/puzzlescript</path>
        <extension>.pz</extension>
        <command>/usr/bin/runemu.sh %ROM% -P%SYSTEM% --core=%CORE% --emulator=%EMULATOR% --controllers="%CONTROLLERSCONFIG%"</command>
        <platform>puzzlescript</platform>
        <theme>puzzlescript</theme>
        <emulators>
            <emulator name="retroarch">
                <cores>
                    <core default="true">puzzlescript</core>
                </cores>
            </emulator>
        </emulators>
    </system>
   ```
6. Copy the updated XML document back to `/storage/.emulationstation/es_systems.cfg`.
7. Create the path registered in the XML under `/storage` for your roms, e.g. `/storage/roms/puzzlescript` using the above example, and add your roms.
8. Restart EmulationStation and verify that the new cores and roms appear as expected.

### Puzzlescript

To run Puzzlescript games using the core in this repo, save the Puzzlescript source to a text file with the extension `.pz`. Some Puzzlescript features are not supported and some games will not run correctly, or run with graphical glitches that may make them unplayable.