---
date: 2024-05-10 09:56:11
layout: post
---

# [Noncontact Vital Sign Detection With an FMCW mm-Wave Radar](https://ieeexplore.ieee.org/abstract/document/10058900)
- check date : 2024.05.10

# Abstract
- chest wall displacement caused by heartbeat is much smaller than that caaused by respiration.
&emsp; making it difficult to achieve accurate and reliable HR detection. (harmonics, noise, clutter등으로 인해)
- 이 과제를 해결하기 위해(In order to tackle this challenge), 4개의 function module을 구성
&emsp; - VS extraction module : VS신호를 추출하기 위해 clutter를 제거하고 VS 신호가 강한 body에 해당하는 range bin이 결정된다.  
&emsp; - differential enhancement module : HR 추정에 대한 호흡 고조파 및 잡음의 영향을 줄여 1차 시간차에 의해 heartbeat component를 향상시키는 역할  
&emsp; - 신호 분해 모듈(signal decomposition module) : wavelet packet decomposition(WPD)를 통해 호흡 신호와 심박 신호를 분리하여 심박 신호의 호흡 고조파 및 고주파 노이즈 억제  
&emsp; - VS 비율 재구성 모듈(vital sign rate reconstruction module) : VS 비율의 희소 스펙트럼 재구성(sparse spectrum reconstruction, SSR)은 적응형 필터에 mapping되고, 제로 유인 부호 지수 망각 최소 평균 제곱 (zero attracting sign exponentially forgetting least mean square, ZA-SEFLMS) algorithm은 고해상도 희소 스펙트럼을 달성  
- result는 설계된 mmRH가 호흡 고조파, 소음 및 클러터 간섭을 효과적으로 억제할 수 있으며 기존 방법에 비해 RR/HR 감지 정확도가 크게 향상됨


# ...


# ...


# ...




