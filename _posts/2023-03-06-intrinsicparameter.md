---
title:  "calibration: Intrinsic parameter"
author:
  name: 강 상호
  link: https://github.com/kw-sangho
date: 2023-03-06 15:40:00 +0900
categories:  [computervision, calibration]
tags: []
---

#### Intrinsic parameters

카메라의 내부 파라미터로는 다음과 같은 것들이 있습니다.  

초점거리(focal length): fx, fy  
주점(principal point): cx, cy  
비대칭계수(skew coefficient): skew_c = tanα  

![intrinsicparameter.png](attachment:intrinsicparameter.png)

#### Focal Length(초점거리)

![foclalength.png](attachment:foclalength.png)

초점거리란 렌즈중심에서 이미지 센서(CCD, CMOS etc)까지의 거리이다.  
일반적으로 디지털 카메라 등에서 초점거리는 mm 단위로 표현되지만,    
카메라 모델에서 말하는 초점거리(f)는 픽셀(pixel) 단위로 표현하는데  
컴퓨터 비전 분야에서 카메라 초점거리를 물리단위(m, cm, mm, ...)가 아닌 픽셀단위로 표현하는 이유는  
이미지 픽셀과 동일한 단위로 초점거리를 표현함으로서 영상에서의 기하학적 해석을 용이하게 하기 위함이다.    

Pixel의 물리적 크기 = (이미지 센서의 cell 크기) × (Focal length)
  
이미지 센서를 구성하는 cell들의 x, y축 방향으로의 물리적 간격이 다를 수 있기 때문에 Focal length는 보통 fx, fy로 나누어서 생각합니다.  
그러나 요즘은 카메라를 잘 만들기 때문에 보통 fx=fy이다.

++ 이미지 센서와 이미지 평면(Image sensor / Image plane)   

Image sensor의 각 cell은 Image plane의 각 pixel와 대응됨

이미지센서의 cell 크기가 0.1 mm 이고, f (focal length)가 100(pixel) 이면, 이미지평면에서 각 pixel의 물리적 크기는 10 cm 입니다.

#### Principal point(주점)

카메라 렌즈 중심에서 이미지 센서로 내린 수선의 발의 영상좌표 (정확하다면 이미지 센서의 중심이어야 함 / 단위는 Pixel)

카메라의 조립 과정에서 센서의 수평이 어긋날 경우 Principal point(주점)와 Image center(영상의 중심점)는 다른 값을 가지게 됩니다.  
따라서 Principal point와 image center는 다른 의미로 해석되어야 합니다. 영상에서는 Principal point가 단순 image center보다 더 중요하며,  
모든 기하학적 해석을 Principal point를 이용해서 이루어집니다.

 

#### Skew coefficient(비대칭 계수)

이미지 센서의 cell array의 y축이 기울어진 정도

하지만, 요즘은 카메라를 잘 만들기 때문에 보통 skew_c = 0으로 간주합니다.

*본 포스팅은 주로 "다크 프로그래머"님의 블로그를 기반으로 작성한 글입니다.
