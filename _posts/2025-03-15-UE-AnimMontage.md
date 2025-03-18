---
title: "[Unreal Engine 5] AnimMontage"
author: ramraid
date: 2025-03-15 10:30:00 +0800
categories: [Unreal Engine, Component]
tags: [Unreal Engine, Components, Programming, C++]
math: false
render_with_liquid: true
pin: false
image:
    path: ../assets/img/posts/UnrealEngine/2025-03-15-UE-AnimMontage-01.png
    alt: AnimMontage
---

# Overview

같은 액션에 대해 여러 애니메이션을 사용하기 위한 일종의 컨테이너.
주로 공격 (1타, 2타, 3타), 스킬, 피니시 액션 (무기에 따른 애니메이션), 감정 표현 (😀, 😂, 🥰) 등 특정 액션을 트리거할 때 사용.

Blend in/out 기능을 가지고있어, 매번 새로운 Blendspace를 필요로 하지 않는다.

## Features

1. 여러 애니메이션을 한 개의 `AnimMontage`에 포함 가능
2. `플레이어 input`, `AI Event` 등 특정 상황에서 애니메이션 실행 가능
3. `Section & Branching` : 특정 입력에 따라 다른 섹션으로 이동하는 Branching 설정
4. `Blend In & Blend Out` : 애니메이션의 시작/끝에서 기존/다음 애니메이션과 얼마나 부드럽게 Blend되는지 설정
5. `AnimNotify`를 이용해 함수나 사운드의 실행 시점을 설정

## Example

```cpp
void AOpenPlayerCharacter::Attack()
{
	DEBUG_MESSAGE(TEXT("Attack Called !"));
	UAnimInstance* AnimInstance = GetMesh()->GetAnimInstance();
	if (AnimInstance && AttackMontage)
	{
		AnimInstance->Montage_Play(AttackMontage);
		int32 Selection = FMath::RandRange(0, 1);
		FName SectionName = FName();
		switch (Selection)
		{
		case 0:
			SectionName = FName("Attack1");
			break;
		case 1:
			SectionName = FName("Attack2");
			break;
		default:
			break;
		}
		AnimInstance->Montage_JumpToSection(SectionName, AttackMontage);
	}
}
```

## reference

[what is anim montage and do I need it?](https://www.reddit.com/r/unrealengine/comments/hhhj4b/what_is_anim_montage_and_do_i_need_it/?rdt=46909)

[UAnimMontage](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Animation/UAnimMontage)
