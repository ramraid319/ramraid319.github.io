---
title: "[CG] Ray Tracing"
author: ramraid
date: 2024-11-16 20:30:00 +0800
categories: [Computer Graphics, Ray Tracing]
tags: [Computer Graphics, Ray Tracing]
math: true
image:
    path: /assets/img/posts/ComputerGraphics/Lerp.png
    alt: Lerp
render_with_liquid: false
pin: false
---

# Ray Tracing

## ray class

![Lerp](/assets/img/posts/ComputerGraphics/Lerp.png)

Ray는 $P(t)=A+tb$ 로 표현할 수 있다. 이 함수는 3D 공간 상에서 position을 결정한다.
$A$는 ray의 처음 위치 (origin)이고, $b$는 ray의 방향 벡터다.
$t$는 ray parameter라고 하며, 이 값에 따라 ray 3D 직선 상에서 위치가 변한다.

```cpp
#ifndef RAY_H
#define RAY_H

#include "vec3.h"

class ray {

public:
    ray() {}

    ray(const point3& origin, const vec3& direction) : orig(origin), dir(direction) {}

    const point3& origin() const { return orig; }
    const vec3& direction() const { return dir; }

    point3 at(double t) const {
        return orig + t * dir;
    }

private:
    point3 orig;
    vec3 dir;
};

#endif
```

## Sending Rays Into the Scene

Ray Tracer의 핵심은 Ray Tracer가 픽셀을 통해 Rays를 보내면, 해당 direction에서 봤을 때의 색상을 계산한다는 것이다. 그러기 위해서는 아래 순서를 따른다.

1. eye로부터 픽셀까지의 ray를 계산
2. 어떤 오브젝트가 ray와 겹치는지 (intersect) 결정
3. 가장 가까운 intersection point의 색상을 계산

### Simple Camera

Ray Tracer의 예제를 위해 먼저 간단한 카메라를 구현한다.
이전 예제에서는 x, y transpose 연산이 부담스러워 Square 이미지를 만들었었다.

하지만, Non-Sqare 이미지를 사용한다고 하면, 흔히 16:9 aspect ratio 이미지를 사용한다.

#### Aspect Ratio and Viewport

$$width / height = 16 / 9 = 1.7778$$

```cpp
auto aspect_ratio = 16.0 / 9.0;
int image_width = 1024;
int image_height = int(image_width / aspect_ratio);
image_height = (image_height < 1) ? 1 : image_height;
```

위와 같이 image_width를 기준으로 aspect ratio가 image_height를 결정한다.
이렇게 하면 비율이 망가지지 않게 image_width만 키우거나 줄여서 이미지 크기 조절이 가능하다.

추가적으로, 렌더링된 이미지의 pixel dimension을 설정하기 위해, scene rays를 통과할 가상의 viewport가 필요하다.
viewport는 이미지 픽셀의 위치를 위한 grid를 가지는 가상의 직육면체다.

만약 픽셀이 수직, 수평으로 동일한 거리만큼 떨어져 있을 때, viewport의 경계에는 aspect ratio와 같은 비율의 픽셀이 있을 것이다.
그 두 픽셀 사이의 거리를 **pixel spacing**이라고 한다.

```cpp
auto viewport_height = 2.0;
auto viewport_width = viewport_height * (double(image_width)/image_height);
```

여기서 왜 viewport_width를 계산할 때, asepct_ratio를 직접 사용하지 않는지 의아할 수 있는데, aspect_ratio는 이상적인 수치(16.0/9.0)이고, 실제 image_width와 image_height로 계산한 비율 int(image_width/aspect_ratio) 과는 약간의 차이가 있기 때문이다.

int 타입으로 변환하는 과정에서 round될 수도 있고, image_height가 1이상이 되게 만들었기 때문에 차이가 발생한다.

#### Camera

Camera Center를 3D 공간에서의 점으로 정의한다.
이 때, Camera Center에서 viewport center는 수직을 이룬다.

초기에는 이 두 점 사이의 거리를 1 unit으로 설정할 것이고, 우리는 이 거리를 focal length라고 한다.

그리고 우수법을 쓴다는 가정 하에, x-axis는 오른쪽, y-axis는 위쪽 방향이다.

![CameraCenter](/assets/img/posts/ComputerGraphics/Camera-Center.png)

대개 coordinates를 이렇게 사용하긴 하지만, 만약에 좌측 상단을 zeroth 픽셀로 두려면, y-axis가 invert된 coordinate를 사용해야 한다.

이미지를 스캔할 때도, 좌측 상단을 zeroth로 하면,

좌우 벡터를 $V_u$, 상하 벡터를 $V_v$ 라고 할 수 있다.

![Viewport](/assets/img/posts/ComputerGraphics/Viewport.png)

#### Reference

[RayTracingOneWeekend](https://raytracing.github.io/books/RayTracingInOneWeekend.html)
