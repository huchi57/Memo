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

#### Some hotkeys
- `C`: Comment (selecting nodes will automatically encapsulates them)
- `G`: Toggle outlines
- `F8` (When playing): Unpocess the character
- `Mouse Left Click` combinations:
  - `B`: Branch
  - `D`: Delay
- When dragging a variable:
  - `Ctrl`: Get
  - `Alt`: Set

#### Common nodes (keywords)
- Increment (++)
- Decrement (--)
- Flip Flop
- Do Once
- Branch
- Switch
- Cast
- Is Valid
- Construct Object from Class
- Spawn Actor from Class
- Get Outer Object
- Add Movement Input
- Add Controller Pitch / Yaw Input
- Get Actor Forward / Right / Up Vector 

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
