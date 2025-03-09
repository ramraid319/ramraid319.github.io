---
title: "[Unreal Engine 5] Timeline Component"
author: ramraid
date: 2025-02-22 10:30:00 +0800
categories: [Unreal Engine, Components]
tags: [Unreal Engine, Components, Programming, C++]
math: false
render_with_liquid: true
pin: false
---

# Overview

UE5_WakRoom 프로젝트를 진행중에 Tick을 이용한 사물제어는 퍼포먼스에 좋지 않다. 이를 개선하고자 Timeline Component를 사용한다.

## Documentation

UTimelineComponent는 keyframes에 대한 일련의 events, floats, vectors, colors를 가진다.

즉, Timeline의 keyframe으로 non-cinematic 애니메이션이나 빛의 색을 변화시키는 등의 표현을 interpolation을 통해 자연스럽게 나타낼 수 있다.

> Timeline에 따른 Keyframe로 보간된 value를 얻는 것이 level sequences와 비슷하다.
{: .prompt-info }

## Example

***DoorActor.h***

```cpp
protected:
  UPROPERTY(VisibleAnywhere, BlueprintReadWrite)
  UTimelineComponent* DoorTimelineComp;

public:
  UPROPERTY(EditAnywhere)
  UCurveFloat* DoorTimelineFloatCurve;

private:
  FOnTimelineFloat UpdateFunctionFloat;

  UFUNCTION()
  void UpdateTimelineComp(float Output);
```

> 참고로 바인딩할 함수는 UFUNCTION 매크로를 사용하여 선언해야한다.
{: .prompt-info }

***DoorActor.cpp***

```cpp
// Constructor
  DoorTimelineComp = CreateDefaultSubobject<UTimelineComponent>(TEXT("DoorTimelineComp"))

// BeginPlay
  // FName() 으로도 바인딩 가능
  UpdateFunctionFloat.BindDynamic(this, &ADoorActor::UpdateTimelineComp);

  if (DoorTimelineFloatCurve)
  {
    DoorTimelineComp->AddInterpFloat(DoorTimelineFloatCurve, UpdateFunctionFloat);
  }

// UpdateTimelineComp(float Output)
  // Implementation

// Something Opening Door Trigger Function
{
  DoorTimelineComp->Play();
}

// .. and Closing Door Trigger Function
{
  DoorTimelineComp->Reverse();
}
```

## Implementation

이걸 개인 프로젝트에서도 사용해봤다.

***DoorActor.h***

```cpp
protected:
	UPROPERTY(EditAnywhere, Category = "Wak|Property")
	UTimelineComponent* MoveTimeline;

	UPROPERTY(EditAnywhere, Category = "Wak|Property")
	UCurveFloat* LocationCurve;


public:
	UFUNCTION()
	void UpateItemLocation(float Value);

	UFUNCTION()
	void StartMoveToLocation(FVector NewLocation);

	UFUNCTION()
	void OnMoveTimelineFinished();

```

***DoorActor.cpp***

```cpp
// Constructor
	MoveTimeline = CreateDefaultSubobject<UTimelineComponent>(TEXT("MoveTimeline"));
	RotateTimeline = CreateDefaultSubobject<UTimelineComponent>(TEXT("RotateTimeline"));

// BeginPlay
	// initialize TimelineComponent
	if (LocationCurve)
	{
		FOnTimelineFloat MoveProgressFunction;
		MoveProgressFunction.BindUFunction(this, FName("UpateItemLocation"));
		MoveTimeline->AddInterpFloat(LocationCurve, MoveProgressFunction);

		FOnTimelineEvent MoveFinishFunction;
		MoveFinishFunction.BindUFunction(this, FName("OnMoveTimelineFinished"));
		MoveTimeline->SetTimelineFinishedFunc(MoveFinishFunction);  // Timeline이 완료 callback

		MoveTimeline->SetLooping(false);
		MoveTimeline->SetTimelineLength(1.f);
	}

void UWakPickableComponent::UpateItemLocation(float Value)
{
	if (!Owner) return;
	FVector NewLocation = FMath::Lerp(StartLocation, TargetLocation, Value);

	Owner->SetActorLocation(NewLocation);
}

void UWakPickableComponent::StartMoveToLocation(FVector NewLocation)
{
	if (!Owner || !MoveTimeline) return;

	StartLocation = Owner->GetActorLocation();
	TargetLocation = NewLocation;

	MoveTimeline->PlayFromStart();
}

void UWakPickableComponent::OnMoveTimelineFinished()
{
	DEBUG_MESSAGE(-1, TEXT("MoveTimeline Finished !!"));
}
```

Tick가 실행되지 않아도 잘 이동된다!

## reference

[timelines-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/timelines-in-unreal-engine)

[creating-timelines-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-timelines-in-unreal-engine)

[UTimelineComponent API](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Components/UTimelineComponent)
