# Upload Game To Steam

## Terminology
- Depot
- Build
- Branch
- Package


## Depot
A collection of files Steam deliver to devices.

Usually only one Depot that contains the latest version of the game is needed.

We can decide which players have access to which Depots.

### Situations for more Depots:
- **Multiple Platforms:** One Depot for Windows version, one Depot for Mac version...
- **DLCs:** One Depot for DLC1, one Depot for DLC2...
- **Other Files:** One Depot for soundtracks...


## Build
A Build is a collection of Depots.

When Depots are uploaded to Steam, a Build is created.

We can have as many Builds as we want.

For example, a Build can have the 1.0 version of the game, while another can have the 1.1 version of the game.

Think of different Builds as different version numbers.


## Branch
A Branch defines which Build of the game the players will get.

By default, all games have just one default Branch.

All players will get the same Build from the same Branch.

A new Branch can be created that, for example, contains the newer Beta version, and a few players have that access.

We can decide how many Branches there are, and which Build is active on which Branch.


## Package
Packages are how players can have access to games.

The simplest way players can do so is by buying the game on the Steam page.

It means that they buy the default store Package, and they gain accesses to that Package.

More Packages can be defined to set what applications and/or what Depots each Package contains.

For example, a Package that contains the main game, and another that contains the main game + DLC.


## Uploading to Steam
### I. Prerequisite
1. Download SteamworksSDK and extract the folders.
2. Also extract `sdk\tools\SteamPipeGUI.zip`.

### II. Steps for Uploading a Depot Using SteamPipeGUI (on Windows)
1. Go to `sdk\tools\ContentBuilder\content\` and create a new folder (any name) for each Depots.
2. Copy all the build files of the game to this folder.
3. Run `SteamPipeGUI.exe`.
4. Fill in `AppID` with the game's AppID.
5. Fill in `Build Description` with an appropriate description.
   - Example: *AppName_Platform_VersionDescription*.
6. Add Depot lists that to be uploaded in the `Depot Configuration` section, and add folder paths to the list.
   - `Depot ID` should be filled automatically, but it can also be checked in the game's Depot page on the Steamworks page.
7. Fill in the path of the `ContentBuilder` and login credentials.
8. Press `Generate VDFs` if this is the first time building the game.
   - This is only needed if new Depots have been added, or if the configuration files have been lost.
9. Press `Upload` and follow the steps on the pop-up command line window.

### III. Steps on the Steamworks Website
1. (TODO)
