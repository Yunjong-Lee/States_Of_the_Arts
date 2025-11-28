# [Vital Signs Monitoring of Multiple People using a FMCW Millimeter-Wave Sensor](https://ieeexplore.ieee.org/document/8378778)
- 2018 IEEE Radar Conference (RadarConf18)  

# PPROCESSING STEPS
## D. Signal Processing for Vital Signs Estimation
- 1. Phase extraction and unwrapping  
- 2. Noise removal  
- 3. Separation of breathing and heart-beat  
- 4. Motion corrupted segment removal  
- 5. Windowing and gain control  
- 6. Spectral estimation  
- 7. Inter-peak distance  
  + 심박수와 호흡수는 각각의 시간 영역 파형에서 피크 간 거리를 찾아 추정  
  + 최소 피크 거리(Pmin)와 최대 피크 거리(Pmax)의 두 임계값은 샘플링 속도와 허용 주파수 범위(심박수의 경우 0.8~2.0Hz)에 따라 정의  
  + 파형의 첫 번째 피크를 유효한 피크로 선택한 뒤, 다음 유효한 신호 피크 분리  
  &emsp; - 신호 피크 분리 조건  
  &emsp; &emsp; : 현재 피크와 이전 유효한 피크 사이의 거리가 간격 [PminPmax] 내에 있도록 선택  
  &emsp; &emsp; : 예상되는 생체 신호 진폭에 따라 진폭이 너무 높거나 너무 낮은 경우의 피크 제외  
  + 유효한 신호 피크 분리 후, 모든 유효 신호 피크에 대한 피크 간 거리의 평균을 기준으로 추정  
  + FFT 기반 추정치의 신뢰도 메트릭이 너무 낮은 경우 피크 간 거리가 생체 신호의 대체 추정치로 사용  

- 8. Breathing-Rate estimate
- 9. Heart-Rate estimate


---


# In-Cabin Radar Monitoring System: Detection and Localization of People Inside Vehicle using Vital Sign Sensing Algorithm
- S:\DOWNL
- 5682-Article Text-5932-1-10-20220908.pdf
