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

#### Some hotkeys
- `C`: Comment (selecting nodes will automatically encapsulates them)
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
- Construct Object from Class
- Spawn Actor from Class
- Get Outer Object

### Classes
#### Inheritence Hierarchy for Common Classes
- Object
  - Actor
    - Pawn
      - Character
    - Controller *(cannot be placed)*
      - Player Controller
