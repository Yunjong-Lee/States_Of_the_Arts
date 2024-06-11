---
date: 2024-05-10 09:56:11
layout: post
---

# [Noncontact Vital Sign Detection With an FMCW mm-Wave Radar](https://ieeexplore.ieee.org/abstract/document/10058900)
- IEEE Sensors Journal, Volume: 23, Issue: 8, 15 April 2023

# Abstract
- commodity devices로부터 Wi-Fi (2.4/5 GHz) 신호를 추출할 수 있음(Wi-Fi 기반 비접촉 센싱은 다양한 응용(호흡감지, 위치추정, 동작 인식 등) 가능
  
  &ensp; - But, Wi-Fi는 성능 제한이 있음  
  &ensp; &ensp; + narrow bandwidth, small(갯수) Ant., large wavelength.  
  &ensp; &ensp; + Wi-Fi의 wavelength가 심장의 움직임에 의해 만들어지는 흉벽 움직임 보다 크기 때문에 heartbeat에 의한 tiny pulse 변화를 capture하기 어렵다.  
  &ensp; &ensp; &ensp; ㅁ 심장의 움직임은 0.2–0.5 mm [^13], Wi-Fi의 wavelength는 60–120 mm
  
  &ensp; - CW doppler radar는 전력 소모는 적으나, range 정보는 제공할 수 없음
  
  &ensp; - UWB pulse radar and FMCW radar는 wideband를 이용하므로 object와 device간의 거리 측정 가능  
  &ensp; &ensp; + UWB는 high hardware cost and system complexity  
  &ensp; &ensp; + mmwave FMCW는 wide bandwidth와 narrow beamwidth를 가지므로 다른 물체의 반사를 구분하는데 도움이 되며, 크기도 소형.
  
- 기존 신호 처리 기술  
  &ensp; - FFT(Fast Fourier Transform) [^18] , STFT(Short-Time Fourier Transform) [^19] , CWT(CW Transform) [^20] 등 주파수 영역 변환 기법을 직접 활용
  
  &ensp; - RR 및 HR 추정  
  &ensp; &ensp; + 앙상블 경험적 모드 분해(EEMD) [^21] , 자기상관 [^22] 및 적응 필터 [^23] 와 같은 시간 영역 신호 처리 기술 사용  
  &ensp; &ensp;  : RR 감지의 경우, 간단하고 제어된 시나리오에서 작동 OK.  
  &ensp; &ensp;  : 그러나 간섭(호흡 고조파, 잡음, 클러터 등)으로 인해 HR 감지 정확도가 낮다  
  &ensp; &ensp; &ensp; ... 다양한 물체(예: 벽, 문, 책상, 가구)에 의해 반사된 신호가 심장 박동 신호를 압도할 수 있다  
  &ensp; &ensp; &ensp; ... 호흡으로 인한 흉벽 변위가 심장 박동으로 인한 것보다 훨씬 더 클 수 있다(호흡 고조파는 심장 박동 신호에 가깝거나 압도하여 피크 선택이 잘못될 수 있다)  

- 이 과제를 해결(tackle)하기 위해 4개의 function module을 구성  
  &ensp; - VS extraction module : VS신호를 추출하기 위해 clutter를 제거하고 VS 신호가 강한 body에 해당하는 range bin 결정. 그 다음에 느린 시간에 따라 생체신호를 추출하여 클러터 간섭 제거
  
  &ensp; - differential enhancement module : ~~HR 추정에 대한 호흡 고조파 및 잡음의 영향을 줄여 1차 시간차에 의해 heartbeat component를 향상시키는 역할~~  1차 시간차를 사용하여 타동 강화 모듈의 심장 박동 구성 요소를 강화하고 호흡 고조파 및 소음의 간섭 완화
  
  &ensp; - 신호 분해 모듈(signal decomposition module) : wavelet packet decomposition(WPD)를 통해 호흡 신호와 심박 신호를 분리하여 심박 신호의 호흡 고조파 및 고주파 노이즈 억제
  
  &ensp; - VS 비율 재구성 모듈(vital sign rate reconstruction module) : VS 비율의 희소 스펙트럼 재구성(sparse spectrum reconstruction, SSR)은 적응형 필터에 mapping되고, 제로 유인 부호 지수 망각 최소 평균 제곱 (zero attracting sign exponentially forgetting least mean square, ZA-SEFLMS) algorithm은 고해상도 희소 스펙트럼을 이용하여 VS 비율 재구성
  
  &ensp; &ensp; + 주파수 빈이 크게 증가하고 호흡 고조파 및 소음의 스펙트럼 전력 억제 가능  
  
- result는 설계된 mmRH가 호흡 고조파, 소음 및 클러터 간섭을 효과적으로 억제할 수 있으며 기존 방법에 비해 RR/HR 감지 정확도가 크게 향상됨  


# Related Works  


# Preliminaries  



# System Implementation  
## A. Vital Sign Signal Extraction Module  
- signal y(n,m) can be expressed for the nth ADC sample and the mth chirp as  
  &ensp; - $y(n,m) = \frac {A_{T} A_{R}}{2} \sum _{i=1} ^{\Omega} [j( 2\pi \frac {2Bd_{i}{nT_{f} }}{cT_d}nT_f + 4\pi \frac {d_i{nT_f + mT_s}}{\lambda}] $  
    
  &ensp; &ensp; + $T_f, T_s$는 time interval corresponding to the fast time and slow time, respectively.  
  &ensp; &ensp; + $d_i(t)$, range between object in the $i-th$ range bin and the radar는 $d_i (t) = \hat d_i + \hatd_i(t)   
  &ensp; &ensp; + $d_i$ is the constant distance between the subject in the ith range bin and the radar and d~i(t) is the time-varying displacement of the subject.  
- Based on (8) and (9), the frequency of the $m-th$ chirp is expressed as  
  &ensp; - $f_b = \frac{2B(\hat d_i + \hat d_i(nT_f))}{cT_s} = \frac{2B \hat d_i}{cT_d}$ &emsp; &emsp; --- (10)   
  &ensp; - fast time displacement $d_i(nT_f)$는 chirp duration가 짧고, frequency에서 큰 변화를 가져올 수 없기때문에 무시할 수 있음.  
  &ensp; - 반사체의 range bin finding은 각각의 chirp에 대해 fast time에 걸쳐 FFT를 수행(range FFT라고 불린다)  
  &ensp; &ensp; + $z(i, m) = \displaystyle\sum_{n=0}^{N-1} y(n,m)exp(-j2\pi \frac{in}{N}) $&emsp; &emsp; --- (11)
  &ensp; &ensp; &ensp; ⨠ i, range bin index
  &ensp; - reflecting object의 range bin은 반사체가 없는 것(range bin) 보다 많은 에너지를 가지므로 range FFT는 empty bin을 필터링할 수 있다.
  &ensp; &ensp; &ensp; ⨠ empty bin : correspond to wall, desk, or metal objects 등
  &ensp; - 4GHz BW를 가지는 FMCW radar의 경우, range redolution이 3.75cm 이므로 반사물체의 multirange bin 검출 가증
  &ensp; &ensp; &ensp; ⨠ multirange bin으로는 팔, 다리 등
  &ensp; - 결과적으로, range FFT로 얻어진 range bin의 위상 변화를 관찰함으로써 range bin에 vital signs 신호가 존재하는지 결정한다.
  &ensp; &ensp; + 
  
## B. Differential Enhancement Module


## C. Signal Decomposition Module


## D. Vital Sign Rate Reconstruction Module



--- 


[^13]: G. Ramachandran and M. Singh, "Three-dimensional reconstruction of cardiac displacement patterns on the chest wall during the P QRS and T-segments of the ECG by laser speckle inteferometry", Med. Biol. Eng. Comput., vol. 27, no. 5, pp. 525-530, Sep. 1989.
[^19]: M. Alizadeh, G. Shaker, J. C. M. De Almeida, P. P. Morita and S. Safavi-Naeini, "Remote monitoring of human vital signs using mm-Wave FMCW radar", IEEE Access, vol. 7, pp. 54958-54968, 2019.  
[^20]: L. Liu, S. Zhang and W. Xiao, "Noncontact vital signs detection using joint wavelet analysis and autocorrelation computation", Chin. J. Eng., vol. 43, no. 9, pp. 1206-1214, 2021.  
[^21]: K.-K. Shyu, L.-J. Chiu, P.-L. Lee, T.-H. Tung and S.-H. Yang, "Detection of breathing and heart rates in UWB radar sensor data using FVPIEF-based two-layer EEMD", IEEE Sensors J., vol. 19, no. 2, pp. 774-784, Jan. 2019.  
[^22]:  H. Shen et al., "Respiration and heartbeat rates measurement based on autocorrelation using IR-UWB radar", IEEE Trans. Circuits Syst. II Exp. Briefs, vol. 65, no. 10, pp. 1470-1474, Oct. 2018.  
[^23]: M. He, Y. Nian and Y. Gong, "Novel signal processing method for vital sign monitoring using FMCW radar", Biomed. Signal Process. Control, vol. 33, pp. 335-345, Mar. 2017.  





