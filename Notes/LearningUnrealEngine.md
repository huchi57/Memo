# Learning Unreal Engine

Video link: [Unreal Engine 5 - Full Course for Beginners](https://youtu.be/6UlU_FsicK8?si=ij3Eyv43fkOmPQps)

## Editor Basics
- `N` to snap object to ground
- Hold `Mouse Right Button` + `WASD` keys to move camera. Use `Scroll Wheel` to speed up/down camera.
- When using landpscapes, hold `Shift` to invert functions.
- Landscapes: ramps are useful for creating, well, ramps.

## Blueprints
### Some Concepts
- `Macro` vs `Function`:
  - Macros will be converted to in-line nodes in compile time.
- A `Function` can have `Pure` enabled or disabled:
  - Pure functions do not have exec wires.
  - Pure functions do not modify states and class members.
  - Pure functions are usually getter functions.
- Right click on a Cast node and select `Convert to pure cast` to make it a pure cast (assuming a cast always success).
- Right click on a variable node and select `Convert to Validated Get` to get validated in one node.
- Variables can have `Private`, `Instance Editable`, and `Expose on Spawn` enabled/disabled.

### Some hotkeys
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
- `Ctrl` + `F`: Find

## Common Blueprint Nodes (keywords)
### C++-ish Nodes
- Increment (++)
- Decrement (--)
- Flip Flop
- Do Once
- Branch
- Switch
- Cast
- Is Valid

### Constructors
- Construct Object from Class
- Spawn Actor from Class

### Debug and Texts
- Line Trace ...
- Draw Debug ... (shape)
- Format Text
- Make Literal String

### Others
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
- Set members in ... (type name)
- Set Timer ...
- Clear and Invalidate Timer by Handle
- Open Level (by Name / Object Reference)
- Set Input Mode ... (mode name)

## Classes
### Inheritence Hierarchy for Common Classes
- Object
  - Actor
    - Pawn
      - Character
    - Controller *(cannot be placed)*
      - Player Controller *(pocesses the Character)*

## Inputs
1. Project Settings > Engine > Input
2. Action Mappings and Axis Mappings
3. In the Blueprint Editor, create a new node and type in the input name.

## Edit Default World Settings
1. Create a Game Mode inherited from Game Mode Base.
2. In the World Settings panel, set the `GameMode Override` to the new Game Mode.
3. Set other overrides like Player Controller.
   - Player Controller persists even when the Character dies.

## Blueprint Example: Timer
1. Create a function.
2. Create a node `Set Timer by Function Name` and connect from `BeginPlay`.
3. Promote the return value to be a `Timer Handler`.
4. In the function, drag the `Timer Handler` variable and add it with a node `Clear and Invalidate Timer by Handle`.

## UI
1. Create a Widget Blueprint by: right click in the Content panel > User Interface > Widget Blueprint.
2. In the Widget Blueprint, create a Canvas.
3. Usually in the Game Controller, add custom event > `Create Widget` > `Add to Viewport`.
   - A widget created has to be added to viewport to be visible.

- `Show Mouse Cursor` is set in the `Player Controller`.

## Blueprint Function Libraries
Useful for creating helper functions.

## C++: Inheritence Hierarchy
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

## C++ and Blueprint
For example, we want to create a character. It is essential to have basic game logic (mission critical stuffs) set up in a C++ class. After that, create a Blueprint class inherit from that C++ class, and that Blueprint will inherit all properties from the C++ class.

## C++ Example: UObject

- Create a new C++ class called `CPP_Object` inherited from Object, a header file and a cpp file will be created.
- A prefix will be added to the file name according to the inherited class.

```
UCLASS(Blueprintable)
class BEGINNERPROJECT_API UCPP_Object : public UObject
{
	GENERATED_BODY()
	
private:
	int PrivateIntValue;

public:
	UPROPERTY(BlueprintReadWrite, EditAnywhere)
		FString PublicStringValue;

	UPROPERTY(BlueprintReadWrite, EditAnywhere)
		int PublicIntValue;

	UFUNCTION(BlueprintCallable)
		void SetPrivateIntValue(int Value);

	UFUNCTION(BlueprintPure)
		int GetPrivateIntValue();
};
```

- `GENERATED_BODY()` is required for objects.
- Instead of `std::stinrg`, Unreal uses `FString` to store strings in the Blueprint.
- Alternatively, the `SetPrivateIntValue` function can be rewritten as follows:

```
  UFUNCTION(BlueprintCallable)
    void SetPrivateIntValue(UPARAM(ref)int& Value);
```

### UCLASS
- Examples:
  - `Blueprintable`: Makes this class creatable in Blueprints. Default: `UObject`: not included (emitted), `UActor`: included.

### UPROPERTY
- Examples:
  - `BlueprintReadWrite`: Makes this property read/wriatable in the Blueprint editor.
  - `BlueprintReadOnly`: Makes this property read-only in the Blueprint editor.
  - `EditAnywhere`: Include this to make the property to be also editable in the Blueprint editor.

### UFUNCTION
- `UFUNCTION` does not support function overloadings.
- Examples:
  - `BlueprintCallable`: Makes this function callable in the Blueprint editor.
  - `BlueprintPure`: Marks it as a pure function (green node, it will have no exec wires).
  - `BlueprintImplementableEvent`: Makes this as an implementable event (red node) in the Blueprint editor.
  - `BlueprintNativeEvent`: For situations where you provide default C++ implementation but give opportunity to override it in Blueprints.

### UPARAM
- Examples:
  - `ref`: Makes the parameter a reference in the Blueprint editor.
  - `(UPARAM(ref)int& Value)` in function parameter declarations will make this parameter a *input reference*.
  - `(&int Value)` in function parameter declarations will make it an *output* in the Blueprint editor. (This is how Blueprint handles multiple return values.)

## C++ Example: enum

```
UENUM(BlueprintType)
enum FruitType
{
	Lingo UMETA(DisplayName = "Apple"),
	Banana,
	Mango
};
```

## C++ Example: struct

```
USTRUCT(BlueprintType)
struct FBook
{
	GENERATED_USTRUCT_BODY()

	UPROPERTY(BlueprintReadOnly, EditAnywhere)
		FString Name;

	UPROPERTY(BlueprintReadWrite, EditAnywhere)
		int Pages;

	UPROPERTY(BlueprintReadWrite, EditAnywhere)
		float Price;
};
```

- `GENERATED_USTRUCT_BODY()` is required for structs.
- All structs should have an `F` prefix to be used in Blueprints.
- Structs do not support `UFUNCTION`s.
  - Workarounds: add functions in function library classes, or defined in other object classes.

## Blueprint Interface
1. Create a Blueprint Interface asset.
2. In the Blueprint that wants to implement the interface, go to Class Settings, and implement the interface.

## C++ Interface
1. Create an interface inherited from Unreal Interface.
2. Make functions to be implemeted `virtual`.
3. Include the header file in classes that wants to implement this interface.
