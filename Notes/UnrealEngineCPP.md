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

## Print String
```
GEngine->AddOnScreenDebugMessage(
  uint64 Key,
  float TimeToDisplay,
  FColor DisplayColor,
  const FString& Debug Message,
  bool bNewerOnTop = true,
  const FVector2D& TextScale = UE::Math::TVector2<double>::UnitVector
)
```
- Example:
```
GEngine->AddOnScreenDebugMessage(-1, 10.0f, FColor::Red, TEXT("Hello"));
```
