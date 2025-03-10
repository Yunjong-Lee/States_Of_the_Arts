# Remote Monitoring of Human Vital Signs Using mm-Wave FMCW Radar  
- [IEEE Access, vol. 7, pp. 54958-54968, 2019.](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8695699)

## 1-1. Abstract
> advanced phase unwrapping signal processing
   compare ref sensor
   acoustic waves could not travel a long distance and they are easily interfered with any mechanical movements, and they need a medium for propagation.  
   EM waves can propagate without medium for propagation and can penetrate through obstacles and do not have the limitations of acoustic waves.
   
## 1-2. Related Works
+ Applications 
> vital signs such as heart rate (HR), breathing rate (BR), blood oxygen density etc 
   &emsp; - HR & BR can detect chest wall movement

+ impulse radar[^impulse_radar]에서 Heart rate 추출(with reduce noise)을 위한 time-varying filter 제안[^0105]
  - 절차: 
  ```mermaid
  graph LR
  A(Find respiration)-->B(Received Signal Derivation)
  B-->C(Time-varying Filter)
  C-->D(Heart rate Estimation)
  ```
  > Issue : 실험 장미 및 설정에 대한 설명과 Ref sensor에 대한 정확도가 report되지 않음

+ FMCW Radar의 Doppler 정확도의 포괄적인 분석이 없음. 논문 [4]에서 FMCW 생성에서 비-이상성(non-idealities)을 고려하여 range 정확도를 조사함. 인위적으로 비선형성과 위상 noise를 추가하여 range detection에 미치는 영향을 평가하기 위해 DDS 사용 (As we are interested in using FMCW radar it is important to notice that there is no comprehensive analysis for the Doppler accuracy of FMCW radars. But in [4], authors investigated the range accuracy considering non-idealities in FMCW generation. This is the first paper using direct digital synthesizer (DDS) for artificially adding non-linearities and phase noise to evaluate their effects on the range detection.)  

+ FMCW 신호 생성시 일종의 위상 무작위성 (위상 노이즈라고 하며, 위상 노이즈는 FMCW radars의 accuracy를 떨어뜨림)이 나타난다.

+ 수신기에서 에코 신호와 전송 신호가 혼합되면 위상 잡음 자기상관은 전송된 위상 잡음 자기상관 함수가 되고, 이것을 범위상관효과라고한다. [^0106] 
  > 범위상관효과는 대상의 범위가 증가함에 따라 모든 레이더 시스템의 range 감지에서 피사체의 range가 증가할수록 위상 노이즈 효과가 증가
    vital sign detection의 경우, 피사체와 레이더의 거리가 가깝기 때문에 거리 상관 효가가 매우 적다
    [6에서,  1) 피부 표면 아래의 혈액 관류로 인해 피부 임피던스 변화 → 2) 피부/신체 표면 움직임이 발생

+ main reason for reflecting an EM wave from a body(신체의 EM파를 반사하는 주된 이유)[^0107]
  > 피부 임피던스 변화로 이어지는 피부 표면 아래의 혈액 관류, 
     피부/신체 표면 움직임. 몇 가지 실험을 설계함으로써 그들은 신체 변위가 피부 표면의 임피던스 변화보다 신호 반사의 영향이 크다.

+ FMCW 레이더를 이용하여 Vital sign 감지[^0108]
  > 레이더는 다양한 범위의 반사를 구별할 수 있기 때문에 잠재적으로 다중 대상 생명 징후 감지에 사용될 수 있음(FMCW의 main advantage)
    높은 전파감쇄는 수신안테나가 에코신호를 수신할 가능성을 줄인다.
    CW 레이더는 모든 가시 범위에서 모든 물체의 모든 반사를 하나의 정현파 신호로 수집하기 때문에 다중 경로 페이딩 발생
+ FMCW 레이더를 사용하여 유사한 위상 획득(80 GHz) [9] 
> 표적의 거리를 알고있다고 가정함
   대상이 앉은 상태에서 앞/뒤/좌/우측에 Radar 거치 후 test 진행  
   &emsp; - phase unwrapping 미 적용(but, FMCW Radar에서는 필요)
   
## 1-3. System Model
+ FMCW Radar
  > CW Radar의 경우, 하나의 정현파 신호로 모든 가시 범위에 존재하는 물체의 신호(echo 신호)를 수집하므로, multi-path fading과 같은 문제 발생  
  AM 신호에 비해 noise에 강함  
  생체 신호 정보는 수신된 위상(FM 신호와 유사)으로 인코딩된다. 그러므로, impulse radar에 비해 noise에 영향을 덜 받는다.

Block diagram of an FMCW radar   

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/6287639/8600701/8695699/aliza1-2912956-large.gif)
- 송신기와 수신기의 전력 증폭기(PA)와 저잡음 전력 증폭기(LNA)는 비선형 구성 요소이나, FMCW 신호는 PAPR이 0dB인 일정한 포락선 신호이므로 증폭기가 선형영역에서 작동할 수 있다.  

- FMCW 생성기 출력의 각 chirp은 Freq.가 $f_{min}$ ~ $f_{max}$ 사이에서 slope $K$와 주기 $T_r$로 linear하게 sweap되는 정현파 신호이다.  
  > sweeping bandwidth $= f_{max} - f_{min} = KT_r$

- rx ANT.의 output port에서 수신된 신호는 amplitude되고, tx signal와 correlated(beat signal 생성)  
  &emsp; - 결과적으로, beat signal이 생성됨, beat signal에는 object의 정보 존재 (반사된 신호의 delay는 송/수신된 chirp 사이의 순간 주파수 차이)
  > linear operation을 위해  time-varying delays 추가가 필요함(time varying delay는 $T_r$보다 크며, BB에서 매우 작은 Doppler shift로 니타님)

Transmitted and received chirp sequences   

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/6287639/8600701/8695699/aliza2-2912956-small.gif)

- complex chirp signal:
  > $s(t) = A_t exp(j(2 \pi f_{min} t + \pi K T^2))$,  &emsp; $0 < t < T_r$  

  > * $f_{min}$ : start frequency  
  > * $A_t$ : magnitude related to the transmit power  

  > single small object situated at the distance of $R_0$ (moving around $R_0$, 거리가 변함)
   $R(t) = R_0 + x(t)$
  > * $x(t)$ : 거리 변화를 나타내는 함수  
  > 물체로부터 반사된 신호는 신호의 왕복시간($t_d = 2R(t)/c$)을 가지는 $s(t)$의 지연된 버전  

- 하나의 chirp 주기에 대한 IF 신호 $y(t)$는  
  &emsp; &emsp; $= s(t) \hat{A} - s^*(t-t_d)$  
  &emsp; &emsp; $= A_t A_r exp(j(\phi(t)-\phi(t-t_d)))$, &emsp; $t_d < t < T_r ... (2)$  

  > thermal noise와 other channel considerations는 무시(단순화)  

- best signal $y(t) = A_t A_r exp(j(2\pi f_{min} t_d + 2\pi Kt_d t - \pi Kt_{d}^2))$  

  &emsp; &emsp; &emsp; &emsp; $\approx A_t A_r exp(j(2\pi f_{min} t_d + 2\pi Kt_d t))$  
  &emsp; &emsp; &emsp; &emsp; $= A_t A_r exp(j(\Psi(t) + \omega_b t))$  
  &emsp; &emsp; $y(t) \approx A_t A_r exp(j(\Psi(t) + \omega_b t)) ... (3)$  
  $\Psi(t) = 4\pi \frac{R_0 + x(t)}{\lambda_{max}}, \omega_b = 4\pi \frac{K R_0}{c} ... (4)$  

  > (3)에서 두 번째 근사 등식은, 세 번째 항목을 무시(매우 작은 값을 가지므로)하면 얻어진다. 세 번째 항목은 $K$가 $10^{12} Hz/s$ order이고, $t_d = 1ns$로 $10^{-6}$으로 매우 작은 값을 가지므로 무시한다.  
  > (4)는 $t$가 $1us$이고, $x(t)$가 하나의 chirp에 대해 거의 일정하기 때문에, $t_d$를 (3)으로 대체하고, $x(t)t$항을 무시하면 얻을 수 있음   
  > $\Psi(t)$는 $x(t)$($\lambda_{max}$에 상대적임)에 따라 변한다.  
  > 최대 파장 규모의 위상 변화는 beat signal의 위상이 크게 변할 수 있다.  
  > 예를 들어, 6GHz 레이더는 60GHz 레이더에 비해 민감도가 10배 낮다. 따라서 동일한 물리적 변위량에 대한 위상 전력은 mm파 단위로 20dB 더 높다.  

- object는 1 [mm/chirp] 이상 움직이지 않으므로($1 [mm/1μs] = 10^3 [m/s]$에 해당) $x(t)$는 하나의 chirp에서 거의 일정하므로 $\Psi(t)$는 $x(t)$를 sampling하여 근사화 가능  

$\Psi(t) = 4 \pi \frac{R_0 + x(t_0)}{\lambda_{max}} ... (5)$
  > $t_0$는 $[R_d, T_r]$ 내에서 임의의 시간  
  > 식(5)로 $R_0$의 거리를 detect  
  > chirp sample에 대해 FFT를 수행하면, beat signal의 spectrum(다양한 range 해당하는 object의 peak)이 얻어진다  
  > FFT는 range 정보를 나타냄(range FFT)  
  > 각각의 range FFT bin은 $\Psi(t)$와 유사한 위상과 연관된 실제 거리를 나타낸다.  
  > PA/LNA에 의해 발생된 delay로 인해 $\omega_b$에서 적은 shift가 발생할 수 있음  
  > 식(5)에는 $x(t)$의 변화에 대한 정보가 없음. 변화 관찰을 위해서는 여러 개의 chirp을 순서대로 전송해야한다($x(t)$의 sampling과 유사)   
  > $x(t)$가 $T_c$(frame 주기) 마다 sampling된다고 거정하면  
    - $T_c ≥ T_r$ 및 $x(t)$는 목표 거리에 해당하는 범위 빈의 위상 내에 나타난다
    - 따라서, $x(t)$의 spectrum 정보를 얻기 위해 해당 범위의 쉬상 sample에 대해 FFT를 수행(vibration frequency를 제공하므로, vibration FFT)

- $x(t)$는 흉벽 변위를 모델링하는 함수(심장 박동과 호흡으로 인해 진동하는 주기적인 기능임)로, $x(t)$의 spectrum에는 진동의 기본 주파수 $f_v$와 동일한 간격의 피크 포함
- 진동이 있는 경우 물체의 범위와 진동 주파수는 수식 (5)의 $\omega_b$와 $\Psi(f)$(범위 위상 스펙트럼의 최대값)를 구하여 추정  
- SNR 제한이 없는 경우 최대 감지 가능 범위는 $f_b$의 허용 가능한 최대 베이스밴드 주파수에 대한 제한을 설정하는 Nyquist sampling theory에 의해 결정  
- 최소 범위 감지는 $\frac{c}{2B}$, B는 스위핑 대역폭[12]  
- 보다 실용적인 범위 분해능 관계는 표 1 참조(처프에 N개의 샘플이 있음을 의미하는 N 크기의 범위 FFT 분해능도 고려)  
- 진동의 최대 주파수는 위상 ψ(t)가 샘플링되는 프레임 속도 $frac{1}{T_c}$와 관련  
- 나이퀴스트 샘플링 원리는 최대 가시 $f_v$ 제한  
- min $f_v$은 진동 FFT 포인트 수 M에 의해 결정(전체 진동 스펙트럼이 M개의 빈으로 동일하게 분할되기 때문)  

## 1-4. Proposed Algorithm  

![](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/6287639/8600701/8695699/aliza3-2912956-small.gif)  
- 심호흡수 감지에 사용되는 신호 처리 체인  

+ $f_{b,max}$로 비트 신호 샘플링 → range FFT를 각각의 spl에 적용 → 적용 결과로 vector(complex range profile)를 얻음  
  > sampling된 beat signal을 FFT하면, range에 대한 profile을 얻을 수 있음(range FFT)  
  > 여러 chirp에서 연속적으로 complex range profile 수집 → 행 방정식으로 행렬에 배치 → M행을 가지는 range-slow time matrix 구성(M: chirp 의 수)  

+ 수신된 complex signal의 angle 계산 하기 전 비선형성, 왜곡 등(동위상 직교위상의 DC value 제거 필요) 제거 확인해야 한다.
+ 복소 신호의 I/Q component의 DC 값은 위상성분에 영향을 주기때문에 제거되어야 한다.

+ complex range bin의 Im/Re part를 다음과 같이 가정
$I(t) + dc_i$, $R(t) + dc_r$
$\phi(t) = arctan \frac{I(t) + dc_i}{R(t) + dc_r} \neq \Psi(t)$  
$dc_i $와 $dc_r$은 Imaginary와 Real parts의 DC 값  
- 흉부 진동으로 인한 위상 변조가 많은 DC 항과 고조파를 생성한다[^0113] 
  > DC 항은 target의 변위에 대한 정보를 가지고 있기 때문에 위상 품질 저하 없음.
  > Tx와 Rx의 leakage는 DC 성분을 생성할 수 있음
  > target motion이 아닌 경우로 인한 DC 성분이 있다면, $\phi(t)$와 $\Psi(t)$는 같지 않다
  > - complex plane에서, 수신된 신호의 성상도(constellation)는 원점에서 $[dc_r dc_i]^T$로 이동된다. 

-  cloud의 중심과 반경은 NLLS(nonlinear least square estimation)를 기반으로 추정할 수 있으며, 이 추정은 white Gaussian noise일 때 ML(maximum liklehood) 관점에서 최적. 
- 수학적으로 간략화를 진행한 뒤에 problem은 LLSE(linear least square estimator)로 변환된다.

  $y^* = arg &ensp; min \parallel A_y - b \parallel^2$ &ensp; &ensp; &ensp; &ensp; (7)
  &ensp; &ensp; &ensp; &ensp; &ensp; $^y$
  > A, b are defined in the Appendix A
  > $y = [R &ensp; c_r &ensp; c_i]^T$는 R이 중심점과 반경의 함수인 미지수의 벡터
  > - $c_r, c_i$는 중심점 x의 Re/Im parts

- 흉부 움직임에 대한 위상 변화는 mm 급 민감도에 의해 크게 변화한다.

- DC compensation 뒤, matrix에서 각 column의 위상은 출력위상이 $[-\pi, \pi]$로 wrapping되도록 $tan^{-1}(.)$을 이용하여 계산

- 위상은 위와 대조적으로 $x(t)$때문에 $\pm \pi$ 범위 이상으로 변할 수 있다.  물리적 변위는 $\frac {\lambda _{max}}{4}$보다 클 수 있음. 그러므로 $\pi$ 이상의 위상을 wnrap할 수 있는 mechanism이 필요함

- 식(5)의 $\Psi(t)$가 $t_c$의 적절한 sampling time으로 sampling되면, 두 연속 sample간의 위상차를 $\pi$보다 작게 유지할 수 있음

- 등가적으로, $x(t)$는 $T_c$ 주기내에서 $\frac {\lambda _{max}}{4}$이상 변화할 수 없다. 이 가정이 만족되면, $\pi$보다 큰 위상 변화는 $2 \pi$를 더하거나 빼는 위상 수정(phase unwrapping이라고 하며, range-slow time matrix column에 대해 각각 실행) 과정 필요

- 각 column의 DC 값은 static clutter를 제거하기 위한 phase unwrapping 후에 제거된다. 그 다음에 진동 주파수를 찾기 위해 2번째 FFT가 각각의 column에 적용되면 각 range bin에 대한 진동이 포함된 matrix(range-vibration map이라고 한다)가 생성된다.
- range-vibration map은 심폐수 추정 오류를 최소화하는 best한 range bin을 찾는데 이용된다.
- rate estimation이 ref 센서의 그것과 가장 근접 하도록 최상의 range-bin or column이 선택됨. 실험 section 참고
- best range를 선택 한 후, 진동 주파수의 index와 2개의 이웃 차수를 이용하여 interpolate(보간)하므로써 미세한 진동 주파수를 찾는다(세 가지 진동 지수에 대한 스펙트럼이 가우스 함수와 유사하게 동작한다고 가정하여, 가우스 보간법 채택)

## 1-5. Experimental results  
- 77 GHz에서 $\lambda _{max}$는 3.9[mm], 수식 (5)에서 $x(t)$의 변화는 거의 감지되지 않는다. 일반 성인 경우, 호흡과 심장박동으로 인한 가슴의 움직임은 각각 1~12mm, 0.01~0.5mm 정도임[^0117]

---  

# References


[^0105]: S. M. A. T. Hosseini and H. Amindavar, "UWB radar signal processing in measurement of heartbeat features," in Proc. IEEE Int. Conf. Acoust., Speech Signal Process. (ICASSP), Mar. 2017, pp. 10041007.  
[^0106]: M. C. Budge and M. P. Burt, "Range correlation effects in radars," in Proc. Rec. IEEE Nat. Radar Conf., Apr. 1993, pp. 212216.  
[^0107]: S. M. A. T. Hosseini and H. Amindavar, "UWB radar signal processing in measurement of heartbeat features," in Proc. IEEE Int. Conf. Acoust., Speech Signal Process. (ICASSP), Mar. 2017, pp. 10041007.  
[^0108]: S. Ayhan, S. Scherr, A. Bhutani, B. Fischbach, M. Pauli, and T. Zwick, "Impact of frequency ramp nonlinearity, phase noise, and SNR on FMCW radar accuracy," IEEE Trans. Microw. Theory Techn., vol. 64, no. 10, pp. 32903301, Oct. 2016.  
[^9]: L. Anitori, A. de Jong, and F. Nennie, "FMCW radar for life-sign detection," in Proc. IEEE Radar Conf., May 2009, pp. 16.  
[^impulse_radar]: https://core.ac.uk/download/pdf/483501222.pdf  
[^0113]: C. Li and J. Lin, "Random body movement cancellation in Doppler radar vital sign detection," IEEE Trans. Microw. Theory Techn., vol. 56, no. 12, pp. 3143–3152, Dec. 2008.  
[^0117]: A. D. Droitcour, "Non-contact measurement of heart and respiration rates with single chip microwave Doppler radar", 2006.  




