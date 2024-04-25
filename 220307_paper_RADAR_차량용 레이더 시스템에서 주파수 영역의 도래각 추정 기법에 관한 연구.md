
# [차량용 레이더 시스템에서 주파수 영역의 도래각 추정 기법에 관한 연구](https://www.koreascience.or.kr/article/JAKO201607433788642.pdf)
- The Journal of Korean Institute of Communications and Information Sciences '16-01 Vol.41 No.01


fmcw radar에서, 거리와 속도가 다른 물체들은 서로 다른 beat frequency를 가진다.  
MUSIC 알고리즘을 주파수 영역에서 적용하는 방법 제시  

- radar 종류
  - 펄스 도플러 레이더 : 송신된 펄스 신호가 전방의 차량에 반사되어 돌아오는 시간과 도플러 주파수를 측정하여 전방 차량의 거리와 속도를 추정  
  - 잡음 레이더 : 의사 잡음 신호를 송신하여 다중 경로를 통해 되돌아온 수신 신호의 지연 시간을 추출하여 전방 차량의 거리를 추정  
  - FMCW 레이더 : 정현파의 주파수를 변조하여 송신하고 전방 차량에 맞고 되돌아온 수신 신호와의 관계를 통해 전방 차량의 거리와 속도를 동시에 추정  

ㅁ 일반적으로, 단일 안테나를 적용한 레이더는 전방 물처의 각도를 추정할 수 없음  
→ 각도 추정을 위해서 위상배열 안테나와 도래각 추정 알고리듬(고해상도 알고리즘으로  
[MUSIC](https://ieeexplore.ieee.org/document/1164233), [ESPRIT](https://ieeexplore.ieee.org/document/127959) 등)을 통해 각도, 전파 지연 시간, 주파수 등 추정 가능  
→ 그러나, 타겟과 클러터를 구분하지 않고 각도를 추정하므로, 추정된 각도에서 인식해야 할 전방의 물체가 차량인지 고정 물체 등 불필요한 클러터인지 알 수 없다.

![img](https://latex.codecogs.com/gif.latex?%5CDelta%20t) 시간 동안 주파수 BW만큼 선형 주파수를 변조한 송신신호는  
![ㅑimg](https://latex.codecogs.com/gif.latex?y%28t%29%20%3D%20Acos%5Cleft%20%28%202%5Cpi%5Cleft%20%28%20f_c%20-%20%5Cfrac%7BBW%7D%7B2%7D%20%5Cright%20%29t%20&plus;%20%5Cfrac%7BBW%7D%7B2%5CDelta%20t%7Dt%5E2%20%5Cright%20%29)
여기서, A는 송신 신호의 크기,  
![img](https://latex.codecogs.com/gif.latex?f_c)는 반송 주파수, 그리고 BW는 주파수 변조폭 을 나타낸다.

다중 타겟에 의해 반사되어 수신된 신호는 
![img](https://latex.codecogs.com/gif.latex?r%28t%29%20%3D%20%5Csum_%7Bi%20%3D1%7D%5E%7BD%7DB_icos%5Cleft%20%282%5Cpi%20%5Cleft%20%28%20%5Cleft%20%28%20f_c%20-%20%5Cfrac%7BBW%7D%7B2%7D%20&plus;%20f_%7Bd%2Ci%7D%20%5Cright%20%29%20%28t%20-%20t_%7Bd%2Ci%7D%29%20&plus;%20%5Cfrac%7BBW%7D%7B2%5CDelta%20t%7D%20%28t-t_%7Bd%2Ci%7D%29%5E2%20%5Cright%20%29%20%5Cright%20%29%20&plus;%20n%28t%29)  
여기서, D는 타겟의 갯수, B는 수신 신호의 크기, t_d는 지연 시간, 그리고 f_d는 도플러 주파수.

송신 신호와 수신 신호는 믹서를 통과하면서 서로 곱해지고, 믹서 신호는 저역 필터를 통과하며 고주파 대역이 제거된다. 앞으로 믹서 신호는 저역 필터까지 통과한 신호를 뜻한다. 믹서 신호는  
![img](https://latex.codecogs.com/gif.latex?x%28t%29%20%3D%20%5Csum_%7Bi%20%3D1%7D%5E%7BD%7D%20C_i%20cos%5Cleft%20%282%5Cpi%20%5Cleft%20%28%20%5Cfrac%7BBW%7D%7B%5CDelta%20t%7Dt_%7Bd%2Ci%7D%20-%20f_%7Bd%2Ci%7D%20%5Cright%20%29%20t%20&plus;%20%5Cleft%20%28%202%5Cpi%20%5Cleft%20%28%20f_c%20-%20%5Cfrac%7BBW%7D%7B2%7D%20&plus;%20f_%7Bd%2Ci%7D%20%5Cright%20%29t_%7Bd%2Ci%7D%20-%20%5Cfrac%7B%5Cpi%20BW%7D%7B%5CDelta%20t%7Dt_%7Bd%2Ci%7D%5E2%20%5Cright%20%29%20%5Cright%20%29%20&plus;%20w%28t%29)
여기서, C는 믹서 신호의 크기를 나타내며 특히 ![img](https://latex.codecogs.com/gif.latex?%5Cfrac%7BBW%7D%7B%5CDelta%20t%7Dt_%7Bd%7D%20-%20f_%7Bd%7D)를 beat frequency (송신 신호와 수신 신호의 주파수 차, 관측 구간 동안 일정한 값을 가지며, 또한 target마다 서로 다른 일정한 값을 가짐)를 의미하며, 거리에 의한 지연 시간 성분과 속도차에 의한 도플러 주파수 성분으로 이루어져 있다.  

- 비트 주파수 검출은 믹서 신호의 푸리에 변환과 일정 [CFAR 알고리즘](https://ieeexplore.ieee.org/document/60107)을 통해 얻은 문턱 값들을 비교하여 문턱 값보다
높은 값에 해당하는 주파수를 비트 주파수로 추정
- 도플러 주파수의 영향으로 비트 주파수는 주파수 상향 변조구간과 주파수 하향 변조구간에서 각각 다르게 나타난다.  
![img](https://latex.codecogs.com/gif.latex?f_%7Bbu%7D%20%3D%20%5Cfrac%7BBW%20%5Ccdot%20t_d%7D%7B%5CDelta%20t%7Df_%7Bd%7D%2C%20f_%7Bbd%7D%20%3D%20%5Cfrac%7BBW%20%5Ccdot%20t_d%7D%7B%5CDelta%20t%7Df_%7Bd%7D)  
위 식을 거리에 의한 지연 시간 성분과 도플러 성분 ![img](https://latex.codecogs.com/gif.latex?f_%7Br%7D%2C%20f_d)으로 나누어 보면,  ![img](https://latex.codecogs.com/gif.latex?f_%7Br%7D%20%3D%20f_%7Bbu%7D%20&plus;%20f_d%20%3D%20f_%7Bbd%7D%20-%20f_d%20%3D%20%5Cfrac%7Bf_%7Bbu%7D%20&plus;%20f_%7Bbd%7D%7D%7B2%7D%2C%20f_d%20%3D%20%5Cfrac%7Bf_%7Bbu%7D%20-%20f_%7Bbd%7D%7D%7B2%7D)  
따라서, target의 거리는  
![img](https://latex.codecogs.com/gif.latex?R%20%3D%20%5Cfrac%7Bf_%7Br%7D%20%5Ccdot%20c%5CDelta%20t%7D%7B2BW%7D%20%3D%20%5Cfrac%7Bf_%7Bbu%7D%20&plus;%20f_%7Bbd%7D%20%5Ccdot%20%5CDelta%20t%7D%7B4BW%7D)  
속도는  
![img](https://latex.codecogs.com/gif.latex?V_r%20%3D%20%5Cfrac%7Bf_%7Bd%7D%20%7D%7B2f_c%7D%20c%20%3D%20%5Cfrac%7Bf_%7Bbu%7D%20-%20f_%7Bbd%7D%20%5Ccdot%20c%7D%7B4f_c%7D)  
와 깉이 추정할 수 있다(타겟의 추정 거리와 속도가 추정된 비트 주파수에 의해 결정되기 때문에, 비트 주파수를 얼마나 정확히 검출하느냐에 따라 타겟의 거리와 속도의 추정
정확도 결정됨)

