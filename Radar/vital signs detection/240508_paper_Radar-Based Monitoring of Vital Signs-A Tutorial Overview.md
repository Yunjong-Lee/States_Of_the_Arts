---
date: 2024-05-08 14:55:53
layout: post
---

---
date: 2024-05-08 14:55:53
layout: post
---

# [Radar-Based Monitoring of Vital Signs: A Tutorial Overview](https://ieeexplore.ieee.org/abstract/document/10049295)
- Published in: Proceedings of the IEEE ( Volume: 111, Issue: 3, March 2023)

## 1. Abstract:
~~In the last years, the use of radar systems in health monitoring has been paid to the availability of both low-cost radar devices and computationally efficient algorithms for processing their measurements. In this article, a tutorial overview of radar-based monitoring of vital signs is provided. More specifically,~~  
- available radar technologies and the signal processing algorithms for VS. 
- some useful guidelines that should be followed in the selection of radar devices for vital sign monitoring and in their use. 
- various specific applications of radar systems to health monitoring and some relevant research trends

## 2. Introduction
- ~~Monitoring human vital signs, such heart and respiration rates, represents a routine practice to detect patient deterioration. Changes in vital signs can reveal the existence of serious medical problems; for this reason, early identification of these changes can improve survival rates in several conditions [1]. Vital signs monitoring is often accomplished by means of wearable health devices [2]; this is due to the fact that these devices enable continuous monitoring during daily activities. However, in various situations, such as in the case of infected patients or of patients suffering from mental illness or affected by severe burns or injuries, the use of wearable sensors is not possible or recommended. In such cases, the use of noncontact monitoring devices, such as radar systems, can help healthcare professionals by providing critical information about patient state [3].~~ 
- The application of radar devices to this field and, in particular, to the estimation of heart and respiration rates has become an active research area in recent years [^4], [^5], [^6], [^7]. 
  + the first experimental results in this field date back to 1975, when the use of short-range radar technology was proposed to noninvasively acquire respiratory information by comparing a microwave signal with its echo reflected from the chest of a patient [8], [9]. ~~In the following years, the possibility of employing radar systems for the wireless detection of the physiological movements due to both heartbeat and respiration has been shown [10], [11], [12], [13]. This has motivated the investigation of the use of this technology in a number of medical applications, including adult and neonatal sleep monitoring [14], [15], [16], disaster medicine (e.g., in the detection of human vital signs under rubbles after earthquakes [17]), and lung cancer radiotherapy [18].~~
  + radar-based monitoring of vital signs have been published [^13], [^19], [^20], [^21], [^22], [^23], [^24]
  + doppler radar, UWB radar with signle tx/rx Ant.: 13, 19, 20, 21
  + array Ant. : 22


## 3. Radar for Vital Signs Monitoring: Basic principles, Objectives, and Challenges
- system consists of a tx and a rx.
- Target range and velocity can be estimated with a single tx/rx Ant..
  - measurement of the distance of any target from a given radar system is based on the estimation of the propagation delay of the received waves.
  - measurement of the velocity of target is based on the estimation of the structral changes in wave (표적이 레이더에 접근하거나 멀어지는 경우 도플러 효과로 인해 수신된 전파의 주파수 변화가 관찰됨)
  - measurement of the angular coordinates of any target requires at least two rx Ant. (Object에 충돌하는 전자기파의 DOA 추정).

- body movement(흉벽의 움직임)가 준주기적 진동을 가지며, 이러한 진동이 파동을 변조한다. 그러므로 반사된 전자파로부터 VS에 대한 HR과 BR을 추출할 수 있음[^27], [^28]

- VS Monitoring
  + BR 신호 추출 및 추정, 추출된 BR에서 HR 추정
  + HRV 식별

## 4. Physiological Fundamentals and Mathematical Modeling

### &ensp; 4.1. Basics of Cardiovascular and Respiration Physiology

### &ensp; 4.2. Modeling of Chest Displacement

## 5. Radar Systems: Technologies and Architectures

### &ensp; 5.1. Radar Technologies and Classification

### &ensp; 5.2. Architecture of SISO Radar Systems

#### &emsp; 5.2.1. CW Radars:

##### 5.2.1.1. CW Doppler Radar

##### 5.2.1.2 FMCW Radar

##### 5.2.1.3 FSCW Radar

#### &emsp; 5.2.2. IR-UWB Radar

### &ensp; 5.3. Architecture of MIMO Radar Systems

## 6. Signal Processing Algorithms for Vital Signs Monitoring

### &ensp; 6.1. Deterministic Detection and Estimation Algorithms for SISO Radars
- 단순화를 위해 SISO CW doppler radar로 focus를 맞추고, phase를 고려하면  
  + 위상 추출 단계:  
&emsp; -. $\psi[n] ≜ \psi_0 + \Delta \psi[n]$  
&emsp; &emsp; +. $\psi_0$는 DC 오프셋, $\Delta \psi[n]$은 호흡 및 심장 활동에 의해 유발된 신체 움직임과 관련된 시간에 따라 변하는 값  
&emsp; &emsp; +. $\Delta \psi[n] = \frac{4 \pi}{\lambda} \Delta R [n]$  
&emsp; &emsp; +. 위상 추출은 $N_r$차원 벡터에서 생성하는 첫번째 블럭에서 실행된다.  
&emsp; &emsp; +. $\hat{\psi} ≜ [\hat{\psi}[0], \hat{\psi}[1], ...  \hat{\psi}[N_r - 1] ]^T $  
&emsp; &emsp; +. $N_r$ : the overall number of measurements  
&emsp; &emsp; +. $\hat{\psi}[n]$ : $\psi[n]$(complex sample $[n]$의 위상)의 추정치   
  
  + 주어진 벡터 $\hat{\psi}[n]$에 대해, BR과 HR의 추정은 진폭 스펙트럼에서 지배적인 주파수 성분을 식별하는 periodogram method(주기도방법) [^61]을 이용하여 평가될 수 있다.  
  &emsp; ※ 스페트럼에서 가장 높은 peak는 정상적인 호흡 조건의 호흡 주파수에서 발견되며, HR은 BR 보다 높다(2배 이상). 
  
  &emsp; &emsp; - BR ($F_b$)의 추정치 $\hat{f_b}$는  
  &emsp; &emsp; &emsp; $\hat{f_b} = \hat{b} f_r$  
  &emsp; &emsp; &emsp; +. $\hat{b} = arg_{ b = (0, 1, ... , { ^{N_0}/_2 } ) } Max |Y_b|$  
  &emsp; &emsp; &emsp; +. $Y_{\tilde{b}} ≜ \LARGE{ \frac{1}{N_r} \sum_{n=0} ^{N_r - 1} \hat{\psi}[n] exp(-j2\pi n {\hat{b}}/_{N_0}) }$  
  &emsp; &emsp; &emsp; +. $ N_0 ≜ MN_r$  (M은 oversamplong factor)  
  &emsp; &emsp; &emsp; +. $f_r ≜ \LARGE{ \frac{1}{N_0 T_s} }$  
  &emsp; &emsp; - $Y_b$는 $\widetilde{\psi}$의 $N_0$ DFT 차수의 $\widetilde{b}$th element를 나타내며, 동일한 차수의 FFT 알고리듬을 이용하여 효과적으로 계산할 수 있다.

<img src="https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/5/10061175/10049295/vitet9-3244362-large.gif" alt="Representation of the signal processing chain characterizing
various deterministic methods for VS Estimation" width="700px" height="200x">

#### &emsp; 6.1.1. FMCW and SFCW Radars:

#### &emsp; 6.1.2 IR-UWB Radars:

### &ensp; 6.2. Estimation of Vital Signs of Multiple Subjects Through MIMO Radars

### &ensp; 6.3. Numerical Results

### &ensp; 6.4. Detection and Estimation Algorithms Exploiting LB Methods


# 7. Some Considerations on radar selection and on its use in experimental campaigns.
- ~~In this section, we illustrate some important lessons that we have learned from our experimental work conducted on healthy adult volunteers in the laboratories of the Department of Engineering “Enzo Ferrari” and of the Cardiology Division, Department of Biomedical, Metabolic and Neural Sciences, University of Modena and Reggio Emilia, Modena, Italy.~~ 
- First, we focus on the essential requirements that radar devices employed for vital signs monitoring should meet.
- Then, we provide some guidelines for developing an experimental setup and illustrate some numerical results about the estimates of vital signs extracted from our experimental measurements. 
- Finally, we comment on how to assess estimation accuracy in vital signs monitoring.
## Fundamental Requirements of Radar Devices  
- 측정 환경 요인
  + maximum distance of the radar from the body of the subject under test.  
  &emsp; -. $R_{max} = N \LARGE{ \frac{c}{4B} }$  
  &emsp; &emsp; +. $N$ : number of samples per chirp   
  &emsp; &emsp; +. $B$ : bandwidth of the radiated signal  
  &emsp; &emsp; ※ $B$가 주어진 경우, $N$을 증가(높은 sampling rate 적용)시키면, $R_{max}$는 증가한다.

  + bandwidth and operating frequency ($f_0$)  
  + resolution  
  &emsp; -. 변위 분해능은 연속적으로 수신된 두 개의 프레임에 대한 최소 측정 가능한 변위로 정의  
  &emsp; &emsp; +. displacement $\Delta R_{k, k+1}$은 $k$번째 frame과 이어지는 frame 사이의 taget point로 표현된다.  
  &emsp; &emsp; &emsp; $\Delta R_{k, k+1} = \LARGE{ \frac{\lambda}{4 \pi} } \Delta \psi_{k, k+1}$   
  &emsp; &emsp; &emsp; ... $\Delta \psi_{k, k+1}$ : 에코에서 관측된 phase 변화  
  &emsp; &emsp; +. $\delta_{b,M}$이 호흡에 의한 chest 변위_최대값이라면, 가슴 움직임을 감지하는데 충분한 해상도는 아래 식을 만족해야 한다.    
  &emsp; &emsp; &emsp; $\LARGE{ \frac{\Delta R_{k, k+1}}{T_0} \ge \frac{2\delta_{b,M}}{T_{B,R}} }$  
  &emsp; &emsp; &emsp; $T_0 \le \LARGE{ \frac{2 \delta_{b,M}}{T_{B,R}} }R_{k, k+1}$ &emsp; or &emsp; $T_0 \le \LARGE{ \frac{T_{B,R}}{2 \delta_{b,M}} \frac{\lambda}{4\pi} } \Delta \hat{\psi}_{k, k+1}$ &emsp; &emsp; &emsp; &emsp; --- (82)  
  &emsp; &emsp; +. $δ_{b,M}$과 $4λ$가 같다(where $λ ≅ 4 mm$)고 가정하면, 위상 모호성(phase ambiguity)을 피하기 위해 부등식 $Δψ_{k,k+1} < 2π$가 만족되어야 한다.  
  &emsp; &emsp; +. from (82)로부터 (83)이 추론된다.  
  &emsp; &emsp; &emsp; $\LARGE{ \frac{1}{T_0} > \frac{16}{T_{BR}} }$ &emsp; &emsp; &emsp; &emsp; --- (83)   
  &emsp; -. 프레임 속도는 호흡 frequency보다 높아야 하며, HR의 변위에 대해서도 $T_{B,R}$을 $T_{H,R}$로 대체한 다음 유사하게 공식화 할 수 있다.  
  &emsp; -. BR 및 HR 추정에서 충분한 정확도를 얻으려면, 프레임 속도 $\frac{1}{T_0}$의 선택이 중요함.
  &emsp; &emsp; +. BR의 frame 속도:  
  &emsp; &emsp; +. HR의 frame 속도: $^{50~100}/_{60 [sec]}, 1 ~ 1.67 Hz$ 
  |  | BR | HR |
  |---|---|---|
  | general | $^{10~25}/_{60 [sec]}, 0.2 ~ 0.4 Hz$ | $^{50 ~ 100}/_{60 [sec]}, 1 ~ 1.67 Hz$ | 
  | stress  | $^{~40}/_{60 [sec]},  ~ 0.67 Hz$ | $^{ ~ 180}/_{60 [sec]}, ~ 3 Hz$ | 

  &emsp; &emsp; &emsp; +. (83)을 기반으로, 프레임 속도는 정지 상태에서 25Hz, 스트레스 상태에서는 45Hz 정도이며, 프레임 속도와 별개로 활력 징후에 대한 정확한 추정치를 생성하려면 충분히 긴 관찰 시간이 필요  
  

  + angular resolution  

## 
## 
# 8. Applications of The Radar Technology to VS Monitoring 


--- 

[^4]: C. Gu, C. Li, J. Lin, J. Long, J. Huangfu and L. Ran, "Instrument-based noncontact Doppler radar vital sign detection system using heterodyne digital quadrature demodulation architecture", IEEE Trans. Instrum. Meas., vol. 59, no. 6, pp. 1580-1588, Jun. 2010.  
[^5]: S. M. M. Islam, F. Fioranelli and V. M. Lubecke, "Can radar remote life sensing technology help combat COVID-19?", Frontiers Commun. Netw., vol. 2, pp. 3, May 2021.  
[^6]: G. Wang, J.-M. Muñoz-Ferreras, C. Gu, C. Li and R. Gómez-García, "Application of linear-frequency-modulated continuous-wave (LFMCW) radars for tracking of vital signs", IEEE Trans. Microw. Theory Techn., vol. 62, no. 6, pp. 1387-1399, Jun. 2014.  
[^7]: G. Wang, C. Gu, T. Inoue and C. Li, "A hybrid FMCW-interferometry radar for indoor precise positioning and versatile life activity monitoring", IEEE Trans. Microw. Theory Techn., vol. 62, no. 11, pp. 2812-2822, Nov. 2014.  
[^13]: E. Staderini, "UWB radar in medicine", IEEE Aerosp. Electron. Syst. Mag., vol. 17, no. 1, pp. 13-18, Feb. 2002.  
[^19]: C. Li, V. M. Lubecke, O. Boric-Lubecke and J. Lin, "A review on recent advances in Doppler radar sensors for noncontact healthcare monitoring", IEEE Trans. Microw. Theory Techn., vol. 61, no. 5, pp. 2046-2060, May 2013.  
[^20]: C. Gu, "Short-range noncontact sensors for healthcare and other emerging applications: A review", Sensors, vol. 16, no. 8, pp. 1169, Aug. 2016.  
[^21]: M. Kebe, R. Gadhafi, B. Mohammad, M. Sanduleanu, H. Saleh and M. Al-Qutayri, "Human vital signs detection methods and potential using radars: A review", Sensors, vol. 20, no. 5, pp. 1454, Mar. 2020.  
[^22]: E. Cardillo and A. Caddemi, "A review on biomedical MIMO radars for vital sign detection and human localization", Electronics, vol. 9, no. 9, pp. 1497, Sep. 2020.  
[^23]: C. Li et al., "A review on recent progress of portable short-range noncontact microwave radar systems", IEEE Trans. Microw. Theory Techn., vol. 65, no. 5, pp. 1692-1706, May 2017.  
[^24]: S. Pisa, E. Pittella and E. Piuzzi, "A survey of radar systems for medical applications", IEEE Aerosp. Electron. Syst. Mag., vol. 31, no. 11, pp. 64-81, Nov. 2016.  
[^27]:   
[^28]:  

[^61]: 




