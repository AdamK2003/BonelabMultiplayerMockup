# BonelabMultiplayerMockup

Bonelab multiplayer mod which uses steam networking + Discord invites to connect players.

This fork uses the [SpaceWar](https://partner.steamgames.com/doc/sdk/api/example) appid (480) instead of the original BONELAB appid in order to enable users with the Oculus version of BONELAB to use this mod.

### Simple install

Grab the zip from the release, extract it to your Bonelab game directory, and run the game. Make sure you have MelonLoader and BoneLib installed.

### Build and install instructions

- Clone the repository
- Open the solution in Visual Studio (2022 worked for me)
- Right click solution and select "Restore NuGet Packages"
- Run the game at least once with MelonLoader active
- Copy files to `bin/Debug` (`BONELAB` is (obviously) the game directory):
  - everything from `BONELAB/MelonLoader/Managed`
  - `0Harmony.dll` and `MelonLoader.dll` from `BONELAB/MelonLoader`
  - `BoneLib.dll` from [BoneLib](https://bonelab.thunderstore.io/package/gnonme/BoneLib/)
- Build the solution
- Make sure you have MelonLoader and BoneLib installed
- Copy `BonelabMultiplayerMockupSteamNetwork.dll` to `BONELAB/MelonLoader/Mods`
- Copy `packages/Facepunch.Steamworks.[version]/lib/net46/Facepunch.Steamworks.dll` to `BONELAB/Plugins`
- Copy `steam_api64.dll` from (probably) any Steam game to `BONELAB/Plugins` (possibly optional, it doesn't seem to load anyways)
- Run the game, enjoy!

### Patching the binary

- Install [dnSpy](https://github.com/dnSpy/dnSpy/releases)
- Remove all the loaded assemblies from the sidebar (select all, hit Delete) (optional)
- Load the BLMP assembly (you can drag and drop or use File/Open...)
- Expand entries until you get to `[assemblyName]/[assemblyName]/BonelabMultiplayerMockup/SteamIntegration`, click it to open it in the decompiler
- Find the `gameAppId` variable (the value is going to be `1592190U`)
- Right click it, hit `Edit IL Instructions...`
- Change the `Operand` of the `ldc.i4` instruction at offset 0000 from `0x184B7E` (Bonelab's appid) to `0x1E0` or `480` (SpaceWar's appid)
- Hit OK
- Save the modified assembly using `File/Save Module...`
- Copy the modified assembly into your MelonLoader `Mods` folder for Bonelab, make sure you have all other required files (BoneLib, Steamworks plugin, probably steam_api64.dll)
- Enjoy!
