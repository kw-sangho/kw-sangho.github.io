---
layout: post
title:  "coordinates"
---

### 좌표계(coordinate system)
좌표계는 2D와3D좌표계가 존재한다.

3D 좌표계: 월드좌표계, 카메라 좌표계   
2D 좌표게: 픽셀좌표계(영상좌표계), 정규좌표계(가상좌표계) 

위의 좌표계들은 영상기하학 에서 사용 하는 4개의 좌표계이다. (camera_geometry의 자세한 내용은 다음 글에서 이어진다)    

![좌표계](/assets/im/cordn.png)

#### 1) 월드 좌표계(World Coordinate System)
우리가 살고 있는 공간의 한 지점을 기준으로 한 좌표계로 우리가 평소에 쓰던 좌표계라고 생각하면 된다.   
월드좌표계는 일종의 약속이기 때문에 단위는 자유롭게 사용할 수 있다.

![CodeCogsEqn%20%281%29.gif](attachment:CodeCogsEqn%20%281%29.gif)

#### 2) 카메라 좌표계(Camera Coordinate System)
카메라를 기준으로 한 좌표계이다.   
카메라좌표계의 단위는 윌드 좌표게와 동일하게 설정한다. 

![CodeCogsEqn%20%282%29.gif](attachment:CodeCogsEqn%20%282%29.gif)

#### 3) 픽셀 좌표계(Pixel Image Coordinate System)
픽셀 좌표계는 우리의 눈으로 보는 영상에 대한 좌표계이다.   
다른말로 영상 좌표계 라고도 부른다.   
왼쪽 상단 모서리를 원점 오른쪽 방향을 +X 방향 아래 방향을 +Y 방향 이다.    
픽셀 좌표계의 의해 결정되는 평면을 이미지평면(Image plane)이라고 부른다.   
픽셀 좌표계의 단위는 픽셀이다.(픽셀의 관한 내용은 개요를 참조바란다.) 

![CodeCogsEqn.gif](attachment:CodeCogsEqn.gif)

#### 4) 정규 좌표계(Normalized Image Coordinate System)
정규좌표계는 편의상 도입된 가상의 좌표계로, 카메라의 내부 패러미터(intrinsic parameter)의 영향을 제거한 이미지 좌표계이다. (카메라 내부 패러미터는 카메라 캘리브레이션을 참조 바란다.)  
정규 좌표계는 좌표계의 단위를 없앤 정규화된 좌표계이며 카메라 초점과의 거리가 '1'인 지점으로 옮겨놓은 가상의 이미지 평면이라고 생각하면 된다.   
정규 이미지 평면의 중심이 원점이고 오른쪽 방향이 u 아래 방향을 v 방향이다.

![CodeCogsEqn%20%283%29.gif](attachment:CodeCogsEqn%20%283%29.gif)

카메라 내부 패러미터(A)를 알면 다음의 정규좌표계와 픽셀 좌표계 간 식을 세울 수 있다. 

![CodeCogsEqn%20%285%29.gif](attachment:CodeCogsEqn%20%285%29.gif)

정규좌표계를 도입한 이유는 동일한 장면을 동일한 위치,각도에서 찍더라도 다른 부가적인 이유들로 다른 영상을 얻게된다. 이러한 요소를 제거한 정규화된 이미지 평면에서 공통된 기하학적 특성 분석을 효과적으로 할 수 있기 때문이다.
