---
date: 2024-05-10 09:56:11
layout: post
---

# [Noncontact Vital Sign Detection With an FMCW mm-Wave Radar](https://ieeexplore.ieee.org/abstract/document/10058900)
- IEEE Sensors Journal, Volume: 23, Issue: 8, 15 April 2023

# Abstract
- commodity devices로부터 Wi-Fi 신호를 추출할 수 있음(Wi-Fi 기반 비접촉 센싱은 다양한 응용(호흡감지, 위치추정, 동작 인식 등) 가능  
  &ensp; - But, 2.4/5Ghz Wi-Fi는 성능 제한이 있음
  &ensp; &ensp; + narrow bandwidth, small(갯수) Ant., large wavelength.
  &ensp; &ensp; + HR detection case) 2.4-/5-GHz Wi-Fi (60–120 mm) wavelength가 심장의 움직임(0.2–0.5 mm [^13])의 원인으로 발생되는 흉벽 움직임 보다 크기 때문에 heartbeat에 의한 tiny pulse 변화를 capture하기 어렵다.
  &ensp; - CW doppler radar는 전력 소모가 적은 장점과, range 정보는 제공할 수 없는 단점을 가짐
- chest wall displacement caused by heartbeat is much smaller than that caaused by respiration.  
&ensp; - accurate하고 reliable한 HR detection이 어렵다 (harmonics, noise, clutter등으로 인해)  
- 이 과제를 해결(tackle)하기 위해 4개의 function module을 구성  
&ensp; - VS extraction module : VS신호를 추출하기 위해 clutter를 제거하고 VS 신호가 강한 body에 해당하는 range bin이 결정된다.  
&ensp; - differential enhancement module : HR 추정에 대한 호흡 고조파 및 잡음의 영향을 줄여 1차 시간차에 의해 heartbeat component를 향상시키는 역할  
&ensp; - 신호 분해 모듈(signal decomposition module) : wavelet packet decomposition(WPD)를 통해 호흡 신호와 심박 신호를 분리하여 심박 신호의 호흡 고조파 및 고주파 노이즈 억제  
&ensp; - VS 비율 재구성 모듈(vital sign rate reconstruction module) : VS 비율의 희소 스펙트럼 재구성(sparse spectrum reconstruction, SSR)은 적응형 필터에 mapping되고, 제로 유인 부호 지수 망각 최소 평균 제곱 (zero attracting sign exponentially forgetting least mean square, ZA-SEFLMS) algorithm은 고해상도 희소 스펙트럼을 달성  
- result는 설계된 mmRH가 호흡 고조파, 소음 및 클러터 간섭을 효과적으로 억제할 수 있으며 기존 방법에 비해 RR/HR 감지 정확도가 크게 향상됨


# ...


# ...


--- 


[^13]: G. Ramachandran and M. Singh, "Three-dimensional reconstruction of cardiac displacement patterns on the chest wall during the P QRS and T-segments of the ECG by laser speckle inteferometry", Med. Biol. Eng. Comput., vol. 27, no. 5, pp. 525-530, Sep. 1989.
# ...




