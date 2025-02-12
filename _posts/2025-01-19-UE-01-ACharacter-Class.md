---
title: UE_01 ACharacter Class
author: ramraid
date: 2025-01-19 08:30:00 +0800
categories: [Unreal Engine, Unreal Engine Tutorial]
tags: [Unreal Engine, Class]
math: true
# image:
#     path: /assets/img/posts/
#     alt: Unreal Engine
render_with_liquid: false
pin: false
---

## 프로젝트 생성

![프로젝트 생성](/assets/img/posts/UnrealEngine/2025-01-19-UE-01-01.png)

- Third Person
- C++, Starter Content 추가

## Classes

![Classes](/assets/img/posts/UnrealEngine/2025-01-19-UE-01-02.png)

위 설정대로 프로젝트를 생성하게 되면, Character를 상속한 TutorialCharacter 클래스와 GameModeBase를 상속한 TutorialGameMode 클래스가 생성된다.

### TutorialCharacter

우선, 언리얼 엔진에서 제공하는 Actor 라는 클래스는 월드에 배치할 수 있는 오브젝트이다.

그 다음으로 Pawn 이라는 클래스는 **'Possessed'** 가능한, **Controller 로부터 input을 입력**받을 수 있는 Actor이다.

마지막으로 Character 이라는 클래스는 **'걸어다닐 수 있는'** Pawn 이다.

#### TutorialCharacter.h

생성된 Character 클래스를 살펴보자.

```cpp
// TutorialCharacter.h
// Copyright Epic Games, Inc. All Rights Reserved.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Character.h"
#include "Logging/LogMacros.h"
#include "TutorialCharacter.generated.h"

/* ATutorialCharacter 클래스에 필요한 클래스들을 Forward Declaration */
class USpringArmComponent;
class UCameraComponent;
class UInputMappingContext;
class UInputAction;
struct FInputActionValue;

DECLARE_LOG_CATEGORY_EXTERN(LogTemplateCharacter, Log, All);

UCLASS(config=Game)
class ATutorialCharacter : public ACharacter
{
	GENERATED_BODY()

	/* 카메라를 고정시킬 SpringArmComponent */
	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Camera, meta = (AllowPrivateAccess = "true"))
	USpringArmComponent* CameraBoom;

	/* CameraComponent */
	UPROPERTY(VisibleAnywhere, BlueprintReadOnly, Category = Camera, meta = (AllowPrivateAccess = "true"))
	UCameraComponent* FollowCamera;
	
	/* InputAction을 매핑할 InputMappingContext */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Input, meta = (AllowPrivateAccess = "true"))
	UInputMappingContext* DefaultMappingContext;

	/* Jump InputAction */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Input, meta = (AllowPrivateAccess = "true"))
	UInputAction* JumpAction;

	/* Move InputAction */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Input, meta = (AllowPrivateAccess = "true"))
	UInputAction* MoveAction;

	/* Look InputAction */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Input, meta = (AllowPrivateAccess = "true"))
	UInputAction* LookAction;

public:
	ATutorialCharacter();	

protected:
	/* Move Input 에 바인드할 Move 함수 */
	/* Parameter : InputAction의 Value 값 */
	void Move(const FInputActionValue& Value);

	/* Look Input 에 바인드할 Look 함수 */
	/* Parameter : InputAction의 Value 값 */
	void Look(const FInputActionValue& Value);

protected:

	virtual void NotifyControllerChanged() override;
	virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;

public:
	FORCEINLINE class USpringArmComponent* GetCameraBoom() const { return CameraBoom; }
	FORCEINLINE class UCameraComponent* GetFollowCamera() const { return FollowCamera; }
};

```

#### TutorialCharacter.cpp

```cpp
// TutorialCharacter.cpp
// Copyright Epic Games, Inc. All Rights Reserved.

#include "TutorialCharacter.h"
#include "Engine/LocalPlayer.h"
#include "Camera/CameraComponent.h"
#include "Components/CapsuleComponent.h"
#include "GameFramework/CharacterMovementComponent.h"
#include "GameFramework/SpringArmComponent.h"
#include "GameFramework/Controller.h"
#include "EnhancedInputComponent.h"
#include "EnhancedInputSubsystems.h"
#include "InputActionValue.h"

DEFINE_LOG_CATEGORY(LogTemplateCharacter);

//////////////////////////////////////////////////////////////////////////
// ATutorialCharacter

ATutorialCharacter::ATutorialCharacter()
{
	// Set size for collision capsule
	GetCapsuleComponent()->InitCapsuleSize(42.f, 96.0f);
		
	/* PlayerController에 의해 조종될 때... */
	/* true이면, Pawn이 Controller의 ControlRotation에 맞춰짐 */
	bUseControllerRotationPitch = false;
	bUseControllerRotationYaw = false;
	bUseControllerRotationRoll = false;

	/* true이면, RotationRate를 이용하여 Character가 가속되는 방향으로 회전, 더 자연스러운 회전 가능 */
	GetCharacterMovement()->bOrientRotationToMovement = true;
	GetCharacterMovement()->RotationRate = FRotator(0.0f, 500.0f, 0.0f);

	/* JumpZVelocity : 점프 속도 */
	/* AirControl : 낙하중 컨트롤이 가능한 정도 0-1 */
	/* MaxWalkSpeed : 최대 걷기 속도 */
	/* MinAnalogWalkSpeed : 아날로그 스틱을 기울일 때의 최소 걷기 속도 */
	/* BrakingDecelerationWalking : 걷기의 감속 정도 */
	/* BrakingDecelerationFalling : 낙하중 감속 정도 */
	GetCharacterMovement()->JumpZVelocity = 700.f;
	GetCharacterMovement()->AirControl = 0.35f;
	GetCharacterMovement()->MaxWalkSpeed = 500.f;
	GetCharacterMovement()->MinAnalogWalkSpeed = 20.f;
	GetCharacterMovement()->BrakingDecelerationWalking = 2000.f;
	GetCharacterMovement()->BrakingDecelerationFalling = 1500.0f;

	// CameraBoom라는 SpringArmComponent 인스턴스를 생성 및 부착
	CameraBoom = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraBoom"));
	CameraBoom->SetupAttachment(RootComponent);
	// CameraBoom의 길이
	CameraBoom->TargetArmLength = 400.0f;
	// CameraBoom이 컨트롤러에 의해 회전하도록
	CameraBoom->bUsePawnControlRotation = true;

	// FollowCamera라는 CameraComponent 인스턴스를 생성 및 부착
	FollowCamera = CreateDefaultSubobject<UCameraComponent>(TEXT("FollowCamera"));
	FollowCamera->SetupAttachment(CameraBoom, USpringArmComponent::SocketName);
	// FollowCamera는 SpringArm과 Relative하게 회전하지 않음
	FollowCamera->bUsePawnControlRotation = false;
}

//////////////////////////////////////////////////////////////////////////
// Input

// Pawn 의 Controller가 바뀔 때 자동으로 호출된다.
void ATutorialCharacter::NotifyControllerChanged()
{
	Super::NotifyControllerChanged();

	// Pawn의 Controller를 PlayerController로 Cast
	if (APlayerController* PlayerController = Cast<APlayerController>(Controller))
	{
                // 각 LocalPlayer의 EnhancedInputLocalPlayerSubSystem 클래스를 가져와 MappingContext에 매핑
		if (UEnhancedInputLocalPlayerSubsystem* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PlayerController->GetLocalPlayer()))
		{
			Subsystem->AddMappingContext(DefaultMappingContext, 0);
		}
	}
}

// Pawn이 PlayerController에 소유될 때 호출
void ATutorialCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
	// PlayerInputComponent를 EnhancedInputComponent로 Cast
	if (UEnhancedInputComponent* EnhancedInputComponent = Cast<UEnhancedInputComponent>(PlayerInputComponent)) {
		
		// 각 InputAction을 EnhancedInputComponent에 바인딩
		EnhancedInputComponent->BindAction(JumpAction, ETriggerEvent::Started, this, &ACharacter::Jump);
		EnhancedInputComponent->BindAction(JumpAction, ETriggerEvent::Completed, this, &ACharacter::StopJumping);
		EnhancedInputComponent->BindAction(MoveAction, ETriggerEvent::Triggered, this, &ATutorialCharacter::Move);
		EnhancedInputComponent->BindAction(LookAction, ETriggerEvent::Triggered, this, &ATutorialCharacter::Look);
	}
	else
	{
		UE_LOG(LogTemplateCharacter, Error, TEXT("'%s' Failed to find an Enhanced Input component! This template is built to use the Enhanced Input system. If you intend to use the legacy system, then you will need to update this C++ file."), *GetNameSafe(this));
	}
}

void ATutorialCharacter::Move(const FInputActionValue& Value)
{
	// MoveAction의 InputActionValue는 Vector2D 로 설정되어있다.
	FVector2D MovementVector = Value.Get<FVector2D>();

	if (Controller != nullptr)
	{
		// 정면 계산
		const FRotator Rotation = Controller->GetControlRotation();
		const FRotator YawRotation(0, Rotation.Yaw, 0);

		// 정면의 unit vector 계산
		const FVector ForwardDirection = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::X);
	
		// 우측면의 unit vector 계산
		const FVector RightDirection = FRotationMatrix(YawRotation).GetUnitAxis(EAxis::Y);

		// movement의 방향, 크기
		AddMovementInput(ForwardDirection, MovementVector.Y);
		AddMovementInput(RightDirection, MovementVector.X);
	}
}

void ATutorialCharacter::Look(const FInputActionValue& Value)
{
	// LookAction의 InputActionValue 역시 Vector2D
	FVector2D LookAxisVector = Value.Get<FVector2D>();

	if (Controller != nullptr)
	{
		// controller 회전 크기
		AddControllerYawInput(LookAxisVector.X);
		AddControllerPitchInput(LookAxisVector.Y);
	}
}
```

### GameModeBase

점수 계산 방식, 어떤 Character로 플레이 할지, 승리 조건 등 게임의 룰에 대한 클래스이다.
GameMode 클래스는 Server에만 존재하고, Client에는 존재하지 않는다.

#### GameModeBase.h

```cpp
// Copyright Epic Games, Inc. All Rights Reserved.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/GameModeBase.h"
#include "TutorialGameMode.generated.h"

UCLASS(minimalapi)
class ATutorialGameMode : public AGameModeBase
{
	GENERATED_BODY()

public:
	ATutorialGameMode();
};
```
아직 아무것도 없다..

#### GameModeBase.cpp

```cpp
// Copyright Epic Games, Inc. All Rights Reserved.

#include "TutorialGameMode.h"
#include "TutorialCharacter.h"
#include "UObject/ConstructorHelpers.h"

ATutorialGameMode::ATutorialGameMode()
{
	// DefaultPawnClass 지정
	static ConstructorHelpers::FClassFinder<APawn> PlayerPawnBPClass(TEXT("/Game/ThirdPerson/Blueprints/BP_ThirdPersonCharacter"));
	if (PlayerPawnBPClass.Class != NULL)
	{
		DefaultPawnClass = PlayerPawnBPClass.Class;
	}
}
```