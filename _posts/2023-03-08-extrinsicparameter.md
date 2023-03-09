---
title:  "calibration: Extrinsic parameter"
author:
  name: 강 상호
  link: https://github.com/kw-sangho
date: 2023-03-08 20:50:00 +0900
categories:  [computervision, calibration]
tags: []
---

### Extrinsic parameters

카메라의 외부 파라미터는 카메라 좌표계와 월드 좌표계 사이의 변환 관계를 설명하는 파라미터로서, 두 좌표계 사이의  
회전 및 평행이동 변환으로 표현된다.  

카메라 외부 파라미터는 카메라 고유의 파라미터가 아니기 때문에 카메라를 어떤 위치에 어떤 방향으로 설치했는지 그리고   
월드 좌표계을 어떻게 정의했는지에 따라 달라진다.


카메라 외부 파라미터를 구하기 위해, 먼저 카메라 고유의 내부 파라미터들을 구한다.  
다음으로 미리 알고 있는 or sample로 뽑은 3d월드좌표-2d월드좌표 매칭 쌍들을 이용하여 변환행렬을 구한다.  

### 2D Transformation

기하연산(변환,transform)에 알아보자.  
영상의 기하학적 변환 (Geometric Transformation)이란 영상을 구성하는 픽셀이 배치된 구조를 변경함으로써 전체 영상의 모양을 바꾸는 작업을 뜻한다. 즉, 어떤 픽셀의 좌표가 다른 좌표로 이동되는 경우를 말한다.

2d 변환은 크게 
* 1. Rigid transform
* 2. Similarity transform
* 3. Affine transform   

로 분류 된다.  

#### 1) Rigid Transformation (강체 변환)
Rigid 변환은  회전(rotation)과 평행이동(translation)만을 허용하는 변환이다.  

##### 1.1 평행이동(translation)만을 허용한 경우  
영상 이동체 추적 문제에 있어서 추적 대상의 크기가 고정이고 회전도 일어나지 않는 경우에는 위치 변화만을 보면된다.

![slide1](/assets/img/extrinsic/1.1.png)

##### 1.2 회전(rotation)만을 허용한 경우
(x, y)를 반시계 방향으로 θ 라디안(radian)만큼 회전시키는 변환행렬은 다음과 같다. 단 회전변환에서 주의할 점은, 회전의 기준이 물체 중심이 아닌, 좌표계의 (0,0)을 기준으로 도는 것이다

![slide2](/assets/img/extrinsic/1.2.png)

##### 1.3 Rigid 변환
일반적인 rigid 변환을 행렬식으로 나타내면 다음과 같다.  
rigid 변환을 이용하면 이제 임의의 회전 및 위치이동이 가능해진다.  
예를 들어, 어떤 물체가 제자리에서 θ만큼 회전하는 경우는 먼저 영상 원점을 중심으로 θ만큼 회전한 후 원래 있던 자리로 평행이동해 오면 된다.

![slide3](/assets/img/extrinsic/1.3.png)

위 식에서 평행이동(translation) 부분을 [tx, ty]라 쓰지 않고 [c, d]라 한 이유는 [c, d]가 물체의 평행이동량 뿐만 아니라 회전변환으로 인한 이동량까지 같이 포함된 값이기 때문이다.

![slide4](/assets/img/extrinsic/1.4.png)

#### 2) Similarity Transformation (닮음 변환)
Similarity 변환 즉, 닮음 변환은 rigid 변환에 추가적으로 스케일 변화까지 허용한 변환이다.  
일반식은 다음과 같다. (단, a2+b2≠0) 

![slide5](/assets/img/extrinsic/2.png)

(a = s*cosθ, b = s*sinθ, s는 스케일).  
rotation만을 이용한 식을 변형하면 아래의 식이 나오는데, 최소자승법을 이용하여 a,b를 구할 수 있다. 

![slide6](/assets/img/extrinsic/2.2.png)

이렇게 a, b를 구하고 나면 스케일(scale) s와 회전각 θ는 다음과 같이 계산된다.

![slide7](/assets/img/extrinsic/2.3.png)

#### 3) Affine Transformation
Affine 변환은 회전, 평행이동, 스케일 뿐만 아니라 shearing, 반전(reflection)까지를 포함한 변환이다. 그 일반식은 다음과 같다.  

![slide8](/assets/img/extrinsic/3.1.png)

2D 평면에서의 affine 변환을 직관적으로 이해하는 한 방법은 임의의 삼각형을 임의의 삼각형으로 매핑시킬 수 있는 변환이 affine이다 (단, 평행성을 보존하면서) 라고 이해하는 것이다.

![slide9](/assets/img/extrinsic/3.2.png)

평행성을 보존한다는 의미는 예를 들어 위 그림과 같이 점 p1, p2, p3를 p1', p2', p3'으로 매핑시키는 affine 변환을 구했을 때, 이 affine 변환을 가지고 p4를 매핑시키면 p4'이 나와야 한다는 의미이다. 

#### Reflection Transformation (대칭 변환)

이미지의 대칭 변환은 크기 변환 + 이동 변환을 조합한 결과를 통해 만들어 낼 수 있다. 다음의 이미지를 참고바란다.

![slide10](/assets/img/extrinsic/3.3.png)


*본 포스팅은 주로 "다크 프로그래머"님의 블로그를 기반으로 작성한 글입니다.  
참고 https://gaussian37.github.io/vision-concept-image_transformation/