# Unreal Property System (Reflection)

## UPROPERTY
- `EditAnywhere`
- `BlueprintReadWrite`
- `BlueprintReadOnly`
- `VisibleAnywhere`
- `Transient`: Always initialized to default values, and not serialized to disk.
- `Category = "[Category Name]`
- ...

## UFUNCTION
- `BlueprintCallable`
- `BlueprintImplementableEvent`: It can be implemented in Blueprints. No implementation from C++.
- `BlueprintNativeEvent`: Cam be both implemented in C++ and Blueprints.
  - Create a function with `_Implementation()` prefix to implement in C++.
- ...
