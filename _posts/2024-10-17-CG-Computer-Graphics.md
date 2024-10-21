---
title: "[CG] Computer Graphics"
author: ramraid
date: 2024-10-17 20:00:00 +0800
categories: [Computer Graphics]
tags: [Computer Graphics]
toc: true
comments: true
math: true
mermaid: false
pin: false
---

## Computer Graphics

컴퓨터를 렌더링 도구로 사용하여 이미지를 생성, 조작하는 것 (Image Synthesis)

객체의 3D 표현을 입력받고, 계산을 수행하여 프레임을 생성
게임과 같은 실시간 그래픽의 알고리즘은 오프라인 그래픽과 다르다.

**Imaging**
- 2D: 사진, 이미지 처리, 합성
- 3D: 텍스쳐 맵핑, 볼륨 이미징

**Modeling**
- 2D: Page Description (e.g. PDF), 타이포그래피, User Interface
- 3D: 오브젝트, 캐릭터, 씬

**Rendering**
- 2D: Shape 그리기, 모션 블러, Art Materials 시뮬레이팅
- 3D: Realistic Rendering, Non-photorealistic Rendering

**Animation**
- 2D: User Interface, Titles, 2D Animated filsm
- 3D: Technical Illustration, 애니메이션, Visual Effects, 게임

### Modeling

- 어떻게 현실을 표현할 것인가
  - Geometry: 곡선, 표면, 볼륨
  - Photometry: 빛, 색, 반사
- 이 표현들을 어떻게 만들 것인가
  - Interactive: 조각
  - Algorithmic: 프랙탈, 추출
  - Scanning: 3D 스캔
- 기본 형태 생성
  - 선, 삼각형, 사각형, patches
  - 원통, 구
  - 고차 기본 형태

### Rendering

- 이미지는 결국 필름 위의 빛 분포
- 이미지를 어떻게 표현하고 저장할 것인가
  - 픽셀들의 샘플링된 배열
- 씬에서 이미지를 어떻게 만들 것인가
  - Input: 씬이나 카메라의 3D Description
  - 카메라의 시점을 project
  - Illumination

### Animation

- 모델이 어떻게 움직이는가
- 오브젝트와 카메라, 빛의 position, orientation, direction 등이 일시적으로 변하는 것