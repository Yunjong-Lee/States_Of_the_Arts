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
&emsp; $\psi[n] ≜ \psi_0 + \Delta \psi[n]$  
&emsp; 여기서, $\psi_0$는 DC 오프셋, $\Delta \psi[n]$은 호흡 및 심장 활동에 의해 유발된 신체 움직임과 관련된 시간에 따라 변하는 값  
&emsp; $\Delta \psi[n] = \frac{4 \pi}{\lambda} \Delta R [n]$  
위상 추출은 $N_r$차원 벡터에서 생성하는 첫번째 블럭에서 실행된다.  

&emsp; $\hat{\psi} ≜ [\hat{\psi}[0], \hat{\psi}[1], ...  \hat{\psi}[N_r - 1] ]^T $  
&emsp; $N_r$ : the overall number of measurements  
&emsp; $\hat{\psi}[n]$ : $\psi[n]$(complex sample $[n]$의 위상)의 추정치   
  
&emsp; 주어진 벡터 $\hat{\psi}[n]$에 대해, BR과 HR의 추정은 진폭 스펙트럼에서 지배적인 주파수 성분을 식별하는 periodogram method(주기도방법) [^61]을 이용하여 평가될 수 있다.
  + 스페트럼에서 가장 높은 peak는 정상적인 호흡 조건의 호흡 주파수에서 발견되며, HR은 BR 보다 높다(2배 이상). 

&emsp; BR ($F_b$) 의 추정치 $\hat{f_b}$는  
&emsp; $\hat{f_b} = \hat{b} f_r$  
&emsp; 여기서, $\hat{b}$는  
&emsp; $\hat{b} = arg_{ b = (0, 1, ... , { ^{N_0} / _2} ) } Max |Y_b|$  

&emsp; $Y_b ≜ \frac{1}{N_r} \sum_{n=0}^{N_r - 1} \hat{\psi}[n] exp(-j2\pi n {\hat{b}}/_{N_0})$  

&emsp; $N_0 ≜ MN_r$  (M은 oversamplong factor)  

<img src="https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/5/10061175/10049295/vitet9-3244362-large.gif" alt="Vital Signs Estimation Procedures" width="700px" height="200x">







#### &emsp; 6.1.1. FMCW and SFCW Radars:

#### &emsp; 6.1.2 IR-UWB Radars:

### &ensp; 6.2. Estimation of Vital Signs of Multiple Subjects Through MIMO Radars

### &ensp; 6.3. Numerical Results

### &ensp; 6.4. Detection and Estimation Algorithms Exploiting LB Methods





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




