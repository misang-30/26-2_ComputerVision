## 0. 카메라의 역사


- **카메라 옵스큐라 (Camera Obscura):** 어두운 방이나 상자에 작은 구멍을 뚫어 외부 풍경이 반대로 맺히도록 하는 최초의 카메라 원리입니다.
![[옵스큐라.png]]

---

## 1. 핀홀 카메라

### 0). 개념
- **핀홀 카메라 (Pinhole Camera):** 구멍(Aperture)을 작게 만들어 초점을 맞추는 방식입니다.
    
    - **장점:** 구멍이 작아질수록 이미지가 선명해지지만, 빛의 양이 줄어들어 어두워진다. (Blurring 줄어든다.)
    - **한계** : 회절(Diffraction) 현상으로 인해 다시 번지는 한계가 있습니다.
	- 회절 : 파동(빛)이 장애물이나 작은 구멍(핀홀)을 지날 때 직선으로 진행하지 않고 구멍 뒤편까지 넓게 퍼져 나가는 현상을 의미합니다.

### 1). 핀홀의 문제점



---

## 2. 렌즈의 사용과 한계

핀홀의 빛 부족 문제를 해결하기 위해 렌즈를 사용하여 모으는 빛의 양을 늘리고 Sharp한 초점을 구현합니다. 하지만 렌즈 사용 시 다음과 같은 광학적 문제가 발생합니다:

- **구면 수차 (Spherical Aberration):** 렌즈의 구면 형태로 인해 빛이 한 점에 모이지 않는 현상 (비구면 렌즈나 다중 렌즈로 보정).
    
- **색수차 (Chromatic Aberration):** 빛의 파장(색상)에 따라 굴절률이 달라 색상이 번지는 현상.
    
- **비네팅 (Vignetting):** 다중 렌즈 가림 등으로 인해 외곽부 빛이 차단되어 이미지 주변부가 어두워지는 현상.
    
- **렌즈 왜곡 (Lens Distortion):**
    
    - **방사 왜곡 (Radial Distortion):** 광학 축에서의 거리에 따라 배율이 변함 (배 모양의 **Barrel distortion**, 핀쿠션 모양의 **Pincushion distortion**).
        
    - **접선 왜곡 (Tangential Distortion):** 렌즈와 센서의 평행이 맞지 않아 발생.

## 3. Perspective Projection (원근 투영 모델)

3차원 공간상의 점 $(x, y, z)$이 2차원 이미지 평면 $(u, v)$에 투영되는 수학적 모델을 다룹니다.

- **핀홀 카메라 모델 수학 공식:**
    
    $$u' = \frac{fx}{z}, \quad v' = \frac{fy}{z}$$
    
    (여기서 $f$는 렌즈의 초점거리 Focal Length)
    
- **동일 차원 좌표계 (Homogeneous Coordinates):** 행렬 연산을 용이하게 하기 위해 좌표계를 확장하여 선형 투영(Linear Projection)으로 표현합니다.

## 4. 카메라 매개변수 
- Camera Parameters

3차원 월드 좌표계의 점을 2차원 이미지 좌표계로 변환하는 기하학적 매행렬 $P = K[R \vert{} t]$을 정의합니다.

1. **내부 파라미터 (Intrinsic Parameters, $K$):** 카메라 자체의 고유 특성
    
    - 초점거리 ($f, \alpha, \beta$)
        
    - 주점 / 중심점 ($u_0, v_0$: Principal Point)
        
    - 픽셀 단위 변환 파라미터
        
2. **외부 파라미터 (Extrinsic Parameters, $[R \vert{} t]$):** 월드 좌표계 기준 카메라의 위치와 방향
    
    - 회전 행렬 ($R$: Rotation)
        
    - 이동 벡터 ($t$: Translation)
