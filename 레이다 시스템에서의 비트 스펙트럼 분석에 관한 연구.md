
# [레이다 시스템에서의 비트 스펙트럼 분석에 관한 연구](https://www.dbpia.co.kr/pdf/pdfView.do?nodeId=NODE02251491&googleIPSandBox=false&mark=0&ipRange=false&b2cLoginYN=false&aiChatView=A&readTime=10-15&isPDFSizeAllowed=true&accessgl=Y&language=ko_KR&hasTopBanner=true)

* beat frequency ($f_b$) : f_b = \frac{2}{c} [sR - f_c v], \tag{1}    
   $f_b = \LARGE{ \frac{2}{c}[sR - f_c v] }$ (1)
   - s : 선형 주파수 변조에서 기울기  
   - R : 목표물의 거리  
   - v : 레이더 시선 방향의 속도
   - $f_c$ : 송신 중심 주파수
* 반사신호는 rayleigh 분포로 가정, 잡음은 AWGN으로 가정할 경우 beat 신호의 전력 스펙트럼 모델은  
  $P(f) = \displaystyle\sum_{i=0}^{n}{\frac{a_i}{\sqrt 2 \pi \sigma_i}} \exp[ \frac{-(f - f_i)^2}{2\sigma_i^2} ] +N_0, \tag{2}$
   - $a_i$ = 각 전력 스펙트럼의 크기로, 클러터 및 목표물들에 의한 비트신호의 상대적인 크기
   - $f_i, \sigma_i$ = 각각 신호의 중심주파수 및 전력스펙트럼의 분산 정도를 나타낸다.
   - $N_0$ = 잡음 전력 밀도
  식 (2)에 대한 역푸리에 변환을 통해 시간영역에서의 I, Q 데이터를 얻을 수 있다.
  따라서, 모델 파라미터 값들을 조정하면 다양한 환경을 고려한 target의 beat signal을 생성할 수 있다.
  
* FFT 기반 스펙트럼 분석의 단점
  수신신호의 특성, 클러터 및 잡음환경 등을 고려한 적절한 가중치 윈도우를 적용하지 않을 경우 신호의 누설에 의한 큰 부엽이나 주파수 해상도 감소, 처리손실 등 발생
  (→ 목표물 들의 탐지 및 정보추출에 문제 발생 가능성 증가)  
  - 가중치 윈도우
    : 레이더 시스템에 수신되는 반사신호는 안테나의 dwell time(수신신호의 획득 시간)동안 얻어짐.
    : dwell time 미적용(또는 짧은 dwell time을 가지는) 경우 rectangle window가 적용된 경우가 될 것임.
    : 이 경우, 매우 큰 부엽을 발생시킨다. ractangle window는 주파수 영역애서 다음과 같이 표현된다.  
    - $W_R(n) = 1.0,\quad n = 0, 1, ... N-1\\ W_R(\omega) = \exp(-j\omega\frac{N-1}{2})\frac{\sin(N\omega/2)}{\sin(\omega/2)}, \tag{3}$  
      + 첫 번째 부엽의 크기는 첨두치에 비하여 약 13dB 정도 낮다(부엽들의 크기 감소도 구형 윈도우의 종단 불연속성 때문에 옥타브(octave) 당 -6dB 정도)  
      + 그러나, 해상도와 관련이 있는 주엽의 폭은 상대적으로 좁고 크기가 높게 나타나는 특성을 보인다. ← 해밍윈도우 적용(부엽의 큭기를 낮출 수 있음) 
        :해밍 윈도우는 해닝 윈도우의 변형된 형태(첫 번째 부엽의 크기를 낮추기 위하여 해닝 윈도우 커널들의 부엽 상쇄효과를 이용하는 방식).  
        :따라서 해밍 윈도우는 다음과 같이 표시되는 가중치 적용방식의 윈도우이다.
