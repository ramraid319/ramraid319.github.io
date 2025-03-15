---
title: "[Unreal Engine 5] Delegates"
author: ramraid
date: 2025-03-06 10:30:00 +0800
categories: [Unreal Engine, Programming]
tags: [Unreal Engine, Components, Programming, C++]
math: false
render_with_liquid: true
pin: false
---

# Overview

Delegate는 함수 포인터를 이용해 특정 함수를 직접 호출하지 않고도 실행할 수 있도록 하는 개념

| 특정 이벤트가 발생했을 때 자동으로 callback 함수를 실행

이벤트 기반, 특정 버튼을 눌렀을 때, 어떤 오브젝트의 체력이 0이 되었을 때, 특정 시간이 지났을 때 등

불필요하게 Tick에서 조건을 체크하지 않아도 원하는 타이밍에 함수가 실행된다.

1. Delegate 선언 - 특정 함수 시그니처를 가지는 Delegate를 선언
`DECLARE_DELEGATE_RetVal_TwoRarams(float, FExampleDelegate, float)`
2. Delegate 바인딩 - 특정 객체의 특정 함수를 Delegate에 연결
`AddFloatDelegate.BindSP(MyAdder, &FExample::Adder);`
3. Delegate 실행 - Delegate가 바인딩되어 있다면 실행
`float Result = AddFloatDelegate.Execute(3.5f, 2.5f)`;

## Delegate 종류

| Delegate 종류                | 설명                                                    |
| ---------------------------- | ------------------------------------------------------- |
| `DECLARE_DELEGATE`           | 표준 Delegate 선언                                      |
| `DECLARE_DELEGATE_OneParam`  | 하나의 매개변수가 있는 Delegate                         |
| `DECLARE_DELEGATE_RetVal`    | return 이 있는 Delegate                                 |
| `DECLARE_DYNAMIC_DELEGATE`   | Serialize 가능한 Delegate. 일반 Delegate보다 느림       |
| `DECLARE_MULTICAST_DELEGATE` | 여러 개의 함수를 바인딩시켜 Delegate가 모든 함수를 호출 |

## Declaration

- `DECLARE_DELEGATE_RetVal_OneParam( RetValType, DelegateName, Param1Type )`
- `DECLARE_DYNAMIC_DELEGATE[_RetVal, ...]\( DelegateName \)`
- `DECLARE_MULTICAST_DELEGATE[_RetVal, ...]\( DelegateName \)`

## Binding

UObject나 Shared Pointer에 Delegate를 바인딩하면 그 오브젝트에 대한 약 레퍼런스를 유지, 델리게이트에서 오브젝트가 소멸되면, `IsBound()` 나 `ExecuteIfBound()` 로 처리.

### Binding Delegate

- `Bind()` : 델리게이트 오브젝트에 바인딩
- `BindStatic()` : raw C++ 포인터 글로벌 함수 델리게이트를 바인딩
- `BindRaw()` : raw C++ 포인터 델리게이트에 바인딩. 레퍼런스를 사용하지 않아 오브젝트가 삭제된 경우 호출하는 것이 안전하지 않을 수 있음.
`Execute()` 호출시에 조심해야한다.
- `BindSP()` : Shared-Pointer 기반 멤버 함수 델리게이트에 바인딩. 약 레퍼런스 유지. `ExecuteIfBound()`로 호출할 수 있음
- `BindUObject()` : UObject 기반 멤버 함수 델리게이트를 바인딩. 약 레퍼런스 유지
`ExecuteIfBound()`로 호출할 수 있음
- `UnBind()` : 델리게이트 바인딩 해제

## Execute Delegate

- `Execute()`
- `ExecuteIfBound()`
- `IsBound()`

## Example

```cpp
// Example.h

DECLARE_DELEGATE_RetVal_TwoParams( float, FExampleDelegate, float, float )

class FExample
{
 public:
  float Adder( float A, float B) { return A + B; };
}

// Other.h

#include "Example.h"

class FOther
{
 public:
  FExampleDelegate AddFloatDelegate;    // 함수 시그니처
}

// Other.cpp

TSharedRef< FExample > FloatAdder(new FExample);
AddFloatDelegate.BindSP( FloatAdder, &FExample::Adder );

AddFloatDelegate.Execute(3.5f, 2.5f);
AddFloatDelegate.ExecuteIfBound(5.5f, 1.5f);
```

## Multi-Cast Delegate

- `Add()` : 델리케이트의 실행 목록에 함수 델리게이트 추가
- `AddStatic()` : raw C++ 포인터 글로벌 함수 델리게이트 추가
- `AddRaw()` : raw C++ 포인터 델리게이트 추가. 레퍼런스 사용 X
- `AddSP()` : Shared-Pointer 기반 멤버 함수 델리게이트 추가
- `AddUObject()` : UObject 기반 멤버 함수 델리게이트 추가
- `Remove()` : 멀티캐스트 델리게이트의 실행 목록에서 함수 제거
- `RemoveAll()` : 실행 목록에서 모든 함수 제거
- `Brodacast()` : (만료되었을 수 있는 것을 제외하고) 바인딩된 모든 오브젝트에 Broadcast

### Dynamic Delegate

- `BindDynamic( userObject, FuncName )` : 바인드 매크로, 함수 이름 문자열 자동 생성
- `AddDynamic( UserObject, FuncName )` : 다이나믹 **멀티캐스트 ****델리게이트에서 AddDynamic 호출 매크로, 함수 이름 문자열 자동 생성
- `RemoveDynamic( UserObject, FuncName )` : 다이나믹 **멀티캐스트 ****델리게이트에서 RemoveDynamic 호출 매크로, 함수 이름 문자열 자동 생성

## reference

[Delegates](https://dev.epicgames.com/documentation/en-us/unreal-engine/delegates-and-lamba-functions-in-unreal-engine)

[Multi-cast Delegates](https://dev.epicgames.com/documentation/en-us/unreal-engine/multicast-delegates-in-unreal-engine)

[Dynamic Delegates](https://dev.epicgames.com/documentation/en-us/unreal-engine/dynamic-delegates-in-unreal-engine)
