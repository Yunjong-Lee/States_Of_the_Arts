---
date: 2024-02-13 10:07:20
layout: post
---

# Range Doppler Detection for automotive FMCW Radars
- [Proceedings of the 37th European Microwave Conference, infineon technology](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=4405477)

##### [ Keyword ] Radar, 상호간섭

- tx와 rx 신호간의 difference는 downconversion 후에 결정  
  하나의 주파수 램프에서 추출된 정보로부터 range와 velocity를 함께 검출하는 것은 불완전하다. 불완전을 제거하기 위해 후속 램프들을 생성해야 한다.  
  
- range와 velocity 추출 method  
  + FFT
  + CFAR  
  
- HW 구성
  + Frequency : 24 GHz, sweep bandwidth B = 1 GHz 
  + Front-End (TSLP-16-Package)  
    + tx : VCO & 2 output buffer(deficated for LO Disrtibution & tx antenna)
    + rx : 2 receive path (for angle detection, in parallel), LNA, Mixer, ADC

- radar equation  
  + The basic idea in FMCW에서 기본 개념은 'linear frequency ramp' 생성  
    - bandwidth B와  [-T/2 ~ T/2] 사이의 주기 T를 가지는 하나의 램프에 대한 전송주파수 $f_t(t)$는  
    $f_t(t) = \frac{B}{T}t$

  + phase $\phi_t (t)$ of tx signal $cos \phi_t (t)$ becomes after intrgration:  
  $\phi_t (t) = 2\pi \int _{\frac{-T}{2}} ^t f_T (t)dt$  
  &emsp; &emsp; $= 2\pi(f_ct + \frac{1}{2} \frac{B}{T}t^2)|_\frac{-T}{2} ^t$  
  &emsp; &emsp; $= 2\pi(f_ct + \frac{1}{2} \frac{B}{T}t^2) - \phi_t0$ 
- phase of the downconverted signal $\Delta \phi(t) = \phi_T(t) -\phi_T(t-T)$ is  
$\Delta \phi(t) = 2\pi(f_c\tau + \frac{B}{T}t_T - \frac{B}{2T}\tau^2)$  
where, $\tau$ is the delay between the tx and rx signal of one target and last term in the equation can be neglected because $\frac{\tau}{T} << 1$.  
For calculation of the delay $2(R + v\cdot t)/c$ a target at distance R with constant velocity $v$ is assumed.  
tihs leads to $\Delta \phi(t) = 2 \pi [\frac{2 f_c R}{c} + ( \frac{2 f_c \cdot v}{c} + \frac{2B \cdot R}{T_c})t + \frac{2B \cdot v}{T \cdot c}t^2]$  

The last term is called Range-Doppler-Coupling and can be neglected again  
$\Delta \phi(t) = 2 \pi [\frac{2 f_c R}{c} + ( \frac{2 f_c \cdot v}{c} + \frac{2B \cdot R}{T_c})t]$    

The generated frequency is therefore 
$F_{IF} = \frac{2f_c \cdot v}{c} + \frac{2B \cdot R}{T_C}$  
  
rx signal $S_{IF} = cos(\Delta \phi(t))$ is sampled with an interval $T_A$, the samples are multiplied with a window function $w(n)$ and a zero padding is performed before FFT with the resulting samples is done.  
스펙트럼은 입력 신호가 실수(real)이기 때문에 대칭이다. 복소 기저대역 (complex baseband) signal는 $S_{IF}(t) + i \cdot H(S_{IF}(t) )$로 얻을 수 있다.  
$H(\cdots)$는 Hilbert transformation을 나타냄  
$S_B(n) = A \cdot w(n)e^{i \cdot 2 \pi [\frac{2f_cR}{c} + ( \frac{2f_c \cdot v}{c} + \frac{2B \cdot R}{T_C} )T_An]}$   
