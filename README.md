# 🖥️👨‍🔬: 대학원 연구 성과
> 아주대학교 대학원에서 석사과정 중 진행한 연구에 대한 내용과 성과들을 정리했습니다.

</br>

## 1. 연구

* UWB 무선 통신 기술을 활용한 실내 측위 연구
  <details open>
  <summary> UWB란?</summary>
    
  - **넓은 대역폭** : UWB(Ultra Wideband)는 말 그대로 초광대역을 사용하는 무선 통신입니다. 500MHz 이상의 대역폭을 사용합니다.
    - 넓은 대역폭의 장점은 전파 신호의 펄스의 시간을 매우 잘게 쪼개서 확인할 수 있고, 정밀한 시간 측정이 가능한 것입니다.
    - 대개 UWB 무선 통신을 활용한 거리 측정한 논문들과 기술서들을 확인하면, 거리 오차가 10~30cm까지 난다고 말합니다.
    - UWB 전파 이동 속도는 빛과 같고, 이 빛의 속도가 1ns(나노초)에 대략 30cm 이동합니다.
    - 다양한 다른 이유도 있지만, 기본적으로 정말한 시간 측정과 전파의 이동속도로 계산되는 오차라고 생각하시면 됩니다.
    
  - 시간 기반 측정 : UWB는 시간에 기반한 거리 측정 방식을 사용합니다.
    - Anchor와 Tag 중 Initiator에서 전송된 신호가 Receiver에 도달하는 데 걸리는 시간을 측정합니다.
    - 이 시간 정보를 거리 계산에 활용합니다. 도달 시간을 매우 정밀하게 측정함으로써 거리 오차를 최소화할 수 있습니다.
    - 이를 위해 동기화, 다중 앵커, 다중 태그 등 여러 방법을 사용합니다.
 
  - 짧은 펄스 신호 : UWB 신호는 매우 짧은 펄스 형태로 전송됩니다.
    - 짧은 펄스는 높은 시간 해상도를 제공하고, 신호 간 간섭을 줄입니다.
    - 직진성이 매우 강하므로 멀티패스에 강한 내성을 가지는 것도 이러한 신호 특성 때문입니다.
  ![uwb1](https://github.com/havingforlunch/-Research-results/assets/105187310/33081af2-03a5-499d-b447-cfd3690c5301)
 <Abbasi, Qammer Hussain. Radio channel characterisation and system-level modelling for ultra wideband body-centric wireless communications. Diss. Queen Mary University of London, 2012.>  </details>

* 기존 측위 시스템들은 대부분 3개 이상의 앵커를 사용하였습니다.

![다중앵커 측위](https://github.com/havingforlunch/-Research-results/assets/105187310/b1f2b3ea-f407-4ff1-8a28-f29ff1bde2e2)


  - 3개 이상의 앵커를 사용할 때의 장점은 정확도가 높은 것입니다.
    1) 정확도 증가 : 앵커의 수가 늘어날수록, 각 앵커와 태그의 거리 값을 많이 측정하여 높은 정확도로 태그의 위치를 추정할 수 있습니다.
    2) 넓은 커버리지 : 또한, 더 넓은 범위에 있는 태그를 찾을 수 있습니다.
    3) 이러한 이유로, 공장, 물류창고, 자동화 산업 등 다양한 분야에서 광범위하게 사용되고 있습니다.
       
  - 그러나, 단점도 존재합니다.
    1) 비용 증가 : 많은 앵커를 구매하기 위한 비용이 증가합니다.
    2) 시스템 복잡도 증가 : 여러 앵커 간 동기화와 스케쥴링을 관리해야 하기 때문에, 시스템의 복잡도가 증가합니다.
    3) 유지 보수 : 많은 앵커가 필요한 것은 많은 유지 보수가 필요하게 됩니다. 이는, 시스템의 운용 비용을 증가시킬 수 있습니다.
       

* 이러한 이유로 단일 앵커에 대한 연구 필요성을 느꼈습니다.

  - 방같은 좁은 공간, 지진같은 재난 상황에서 정확도가 너무 높지 않아도, 빠르게 설치할 수 있고 시스템의 복잡도를 줄일 방법을 찾아 보았습니다.
  - 단일 앵커만 존재하는 시스템은 부족한 데이터로 인해 태그의 위치를 추정하기 어렵습니다.
  - 그렇기 때문에, 기존 연구들은 IMU, 카메라 등 다양한 센서와 Sensor Fusion 시스템을 구현하여 태그의 위치를 추정했습니다.
  - 다양한 센서를 결합하는 것도 비용이 증가하게 되고, Sensor Fusion 시스템을 구현하는 것에 복잡도가 증가하기 때문에, 단순화하기 위해 단일 UWB 만을 사용한 측위 방법을 찾기 위해 노력했습니다.
   - UWB는 여러 안테나를 통해 AoA(Angle of Arrival)을 측정할 수 있었습니다.
   - AoA는 다양한 영향으로 오차가 발생하게 됩니다. 이러한 오차를 줄이게 된다면, 태그 위치 추정 정확도가 오를 것이라 생각했습니다.
   - AoA의 오차를 보정하기 위해, Extended Kalman Filter를 사용했습니다.
   - 태그가 움직일 때, 다양한 영향으로 오차가 발생하여 선형적이지 않은 AoA 값들을 선형화하기 위함이었습니다.

## 2. 연구 성과

- 논문 성과
  1. [Single-Anchor UWB 측위 알고리즘 - 2023년도 한국통신학회 하계종합학술발표회](https://github.com/havingforlunch/-Research-results/blob/main/Single-Anchor%20UWB%20%EC%B8%A1%EC%9C%84%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.pdf)
  2. [AoA 기법을 이용한 단일 앵커 기반 UWB 측위 기술 - 2023년도 대한전자공학회 추계학술대회 논문집](https://github.com/havingforlunch/-Research-results/blob/main/AoA%20%EA%B8%B0%EB%B2%95%EC%9D%84%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%EB%8B%A8%EC%9D%BC%20%EC%95%B5%EC%BB%A4%20%EA%B8%B0%EB%B0%98%20UWB%20%EC%B8%A1%EC%9C%84%20%EA%B8%B0%EC%88%A0.pdf)
  3. [IMU-Free UWB 기반 단일 앵커 측위 시스템 - 2024년도 vol 49. 4호 한국통신학회 논문지](https://github.com/havingforlunch/-Research-results/blob/main/IMU-Free%20UWB%20%EA%B8%B0%EB%B0%98%20%EB%8B%A8%EC%9D%BC%20%EC%95%B5%EC%BB%A4%20%EC%B8%A1%EC%9C%84%20%EC%8B%9C%EC%8A%A4%ED%85%9C.pdf)
  4. [단일 앵커 기반 UWB 실내 측위 알고리즘 설계 및 구현 - 석사학위 논문](https://github.com/havingforlunch/-Research-results/blob/main/%EC%98%A4%EC%9D%80%EC%84%AD_%EC%95%84%EC%A3%BC%EB%8C%80%ED%95%99%EA%B5%90_%EC%84%9D%EC%82%AC%20%ED%95%99%EC%9C%84%20%EB%85%BC%EB%AC%B8.pdf)
     
- 기타 성과
  1. [UWB 기반 iOS 모바일기기 상대측위용 소프트웨어 - 소프트웨어 등록(2023.12)](https://github.com/havingforlunch/-Research-results/blob/main/%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4%20%EC%9E%90%EC%82%B0%EB%93%B1%EB%A1%9D%EC%A6%9D_ASSET_0011277.pdf)
