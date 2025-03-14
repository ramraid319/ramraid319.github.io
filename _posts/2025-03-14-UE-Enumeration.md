---
title: "[Unreal Engine 5] Enumeration"
author: ramraid
date: 2025-03-14 10:30:00 +0800
categories: [Unreal Engine, Programming]
tags: [Unreal Engine, Components, Programming, C++]
math: false
render_with_liquid: true
pin: false
---

# Overview

C++에서 Enumeration는 제한된 값 범위를 가지는 고유 Type이다.

## C++ Example

```cpp
enum Color { red, green, blue };
Color r = red;
 
switch(r)
{
    case red  : std::cout << "red\n";   break;
    case green: std::cout << "green\n"; break;
    case blue : std::cout << "blue\n";  break;
}
```

일반적으로 C++ 에서 이런 식으로 사용할 수 있다.

## Unreal Engine 5 Example

```cpp
UENUM(BlueprintType)
enum class ECharacterState : uint8 {
    ECS_Unequipped              UMETA(DisplayName = "Unequipped"),
    ECS_EquippedOneHandWeapon   UMETA(DisplayName = "EquippedOneHandWeapon"),
    ECS_EquippedTwoHandWeapon   UMETA(DisplayName = "EquippedTwoHandWeapon")
}
```

하지만 언리얼 엔진에서는 몇 가지 규칙이 있다.

1. `ECharaacterState` 와 같이 Enum 클래스의 접두사로 `E` 를 붙이는 것이 관례이다.
2. `ECharacterState` 의 Value라면, `ECS_Unequipped` 와 같이 그 약어을 접두사로 붙여야 한다.
3. 언리얼 엔진에서는 `uint8` 의 Enum Class를 지원한다.
4. `UENUM()` 매크로를 추가하여 Reflection System에 노출될 수 있도록 한다.
5. `UMETA()` 매크로를 추가하여 meta data를 추가한다.


## reference

[Enumeration declaration](https://en.cppreference.com/w/cpp/language/enum)

[Multi-cast Delegates](https://dev.epicgames.com/documentation/en-us/unreal-engine/multicast-delegates-in-unreal-engine)
