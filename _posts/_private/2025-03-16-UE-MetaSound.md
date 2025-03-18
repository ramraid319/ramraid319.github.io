---
title: "[Unreal Engine 5] MetaSound"
author: ramraid
date: 2025-03-16 00:30:00 +0800
categories: [Unreal Engine, Component]
tags: [Unreal Engine, Components, Programming, C++]
math: false
render_with_liquid: true
pin: false
image:
    path: ../assets/img/posts/UnrealEngine/2025-03-16-UE-MetaSound-01.png
    alt: MetaSound
---

# Overview

MetaSound는 언리얼 엔진의 새로운 high-performance의 오디오 시스템이다.
기존 Sound Cue와는 달리 MetaSound는 기본적으로 Digital Signal Processing (DSP) 렌더링 그래프다.

즉, 강력한 procedural audio system을 활용하여 샘플 타이밍 정확성을 제공한다.
예를 들면, sample rate 가 48000일 때, 1/48000 초 단위로 컨트롤할 수 있다는 것이다.

## reference

[what is anim montage and do I need it?](https://www.reddit.com/r/unrealengine/comments/hhhj4b/what_is_anim_montage_and_do_i_need_it/?rdt=46909)

[UAnimMontage](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Animation/UAnimMontage)
