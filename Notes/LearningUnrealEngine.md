# Learning Unreal Engine

Video link: [Unreal Engine 5 - Full Course for Beginners](https://youtu.be/6UlU_FsicK8?si=ij3Eyv43fkOmPQps)

### Editor Basics
- `N` to snap object to ground
- Hold `Mouse Right Button` + `WASD` keys to move camera. Use `Scroll Wheel` to speed up/down camera.
- When using landpscapes, hold `Shift` to invert functions.
- Landscapes: ramps are useful for creating, well, ramps.

### Blueprints
#### Some Concepts
- `Macro` vs `Function`:
  - Macros will be converted to in-line nodes in compile time.
- A `Function` can have `Pure` enabled or disabled:
  - Pure functions do not have exec wires.
  - Pure functions do not modify states and class members.
  - Pure functions are usually getter functions.
- Right click on a Cast node and select `Convert to pure cast` to make it a pure cast (assuming a cast always success).
- Right click on a variable node and select `Convert to Validated Get` to get validated in one node.
- Variables can have `Private`, `Instance Editable`, and `Expose on Spawn` enabled/disabled.

#### Some hotkeys
- `C`: Comment (selecting nodes will automatically encapsulates them)
- `G`: Toggle gizmos
- `F8` (When playing): Unpocess the character
- `F11`: Fullscreen
- `Mouse Left Click` combinations:
  - `B`: Branch
  - `D`: Delay
- When dragging a variable:
  - `Ctrl`: Get
  - `Alt`: Set

### Common Blueprint Nodes (keywords)
#### C++-ish Nodes
- Increment (++)
- Decrement (--)
- Flip Flop
- Do Once
- Branch
- Switch
- Cast
- Is Valid

#### Constructors
- Construct Object from Class
- Spawn Actor from Class

#### Debug and Texts
- Line Trace ...
- Draw Debug ... (shape)
- Format Text
- Make Literal String

- ActorBeginOverlap
- ActorEndOverlap
- Get Actor Location
- Get Overlapping Actors
- Get Outer Object
- Get Player Camera Manager
- Add Movement Input
- Add Impulse
- Add Controller Pitch / Yaw Input
- Add Custom Event
- Add to Viewport
- Get Actor Forward / Right / Up Vector
- Set Timer ...
- Clear and Invalidate Timer by Handle
- Open Level (by Name / Object Reference)
- Set Input Mode ... (mode name)

### Classes
#### Inheritence Hierarchy for Common Classes
- Object
  - Actor
    - Pawn
      - Character
    - Controller *(cannot be placed)*
      - Player Controller *(pocesses the Character)*

### Inputs
1. Project Settings > Engine > Input
2. Action Mappings and Axis Mappings
3. In the Blueprint Editor, create a new node and type in the input name.

### Edit Default World Settings
1. Create a Game Mode inherited from Game Mode Base.
2. In the World Settings panel, set the `GameMode Override` to the new Game Mode.
3. Set other overrides like Player Controller.
   - Player Controller persists even when the Character dies.

### Timer
1. Create a function.
2. Create a node `Set Timer by Function Name` and connect from `BeginPlay`.
3. Promote the return value to be a `Timer Handler`.
4. In the function, drag the `Timer Handler` variable and add it with a node `Clear and Invalidate Timer by Handle`.

### UI
1. Create a Widget Blueprint by: right click in the Content panel > User Interface > Widget Blueprint.
2. In the Widget Blueprint, create a Canvas.
3. Usually in the Game Controller, add custom event > `Create Widget` > `Add to Viewport`.
   - A widget created has to be added to viewport to be visible.

- `Show Mouse Cursor` is set in the `Player Controller`.

### Blueprint Function Libraries

### C++: Inheritence Hierarchy
- UObject
  - AActor
    - APawn
      - ACharacter
    - AController
      - APlayerController
    - AInfo
      - AGameModeBase
        - AGameMode *(Exist only on servers)*
      - AGameStateBase
        - AGameState *(Exists both on servers and players)*
      - APlayerState
  - UGameInstance
  - ... UUserWidget

### C++ and Blueprint
For example, we want to create a character. It is essential to have basic game logic (mission critical stuffs) set up in a C++ class. After that, create a Blueprint class inherit from that C++ class, and that Blueprint will inherit all properties from the C++ class.
