# load3DModel

> 내용

- 자동차 3D 모델을 불러와서 움직임을 구현함.	
- 모델: https://skfb.ly/6VtZu

---

> 핵심 내용 정리

- three.js 관련된 모듈들을 불러올 때 버전에 따라서 작동하지 않는 모듈들이 있을 수 있다.

- 씬, 카메라,  renderer을 만들어 준다. 필요에 따라 빛을 추가할 수 있다.

- gltf의 경우 계층 구조를 가지고 있어서, 전체 모델을 불러와서 부분적인 모델들을 조작할 수 있다.

- 모델을 불러온 후 모델의 로컬 좌표 기준으로 설정해야 조작하기 편리하다.

  - 회전, 이동 등

  - ```javascript
    Math.sin()
    Math.cos()
    ```

  - 위 코드를 이용하여 회전을 구현할 수 있다.

  - 자동차의 회전은 크게 2부분으로, 자동차 자체의 회전과 자동차 바퀴의 회전으로 나눌 수 있다.

- ```requestAnimationFrame(animate)```를 통해 2D에서 사용하던 ```setInterval()``` 처럼 업데이트를 담당한다.

- ```document.addEventListener()```를 사용하여 key event를 구현함.

## 2021-12-31
---
+ 카메라 변경 기능 추가 -> 1번과 2번으로 변경 가능
+ 가끔 후진 시 멈추는 버그 수정 -> l_tire_angle과 r_tire_angle의 값이 소수점으로 너무 커져서 발생한 것으로 판단됨.
  - ``` l_tire_angle = parseFloat(l_tire_angle.toFixed(1))
        r_tire_angle = parseFloat(r_tire_angle.toFixed(1))```를 통해 소수점 자리를 제한함.
+ 후진을 THREE.JS에 있는 ```Object3D.translateZ()``` 사용 -> 회전이 좀 더 자연스럽게 느껴짐.
+ 2번 카메라는 자동차를 따라다니는 카메라로, ```camera2.lookAt( car.position );```을 통해 카메라가 오브젝트를 바라보도록 한다.
