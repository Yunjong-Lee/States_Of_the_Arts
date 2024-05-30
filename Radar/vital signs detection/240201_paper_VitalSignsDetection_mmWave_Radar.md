---
date: 2024-02-01 09:44:54
layout: post
---

# [Paper: Vital Sign Detection Using Millimeter Wave Radars](https://trace.tennessee.edu/cgi/viewcontent.cgi?article=7143&context=utk_gradthes)
- vital sign detection with Radar 동향 논문, University of Tennessee, 5-2020

## Introduction
- Vital signs State of Art

|    | Type | Frequency  |Dist  | BR Err| HR Err| Method     |Duration|
|--- |---   |---         |---   |---    |---    |---         |---     |
| 16 | UWB  | 1.5{4.5GHz | 0.8m | x     | 1.7%  | SSM-AD/CSD | 18s    |
| 15 | SFCW | 2-4GHz     | 1m   | x     | 1.6%  | SSM        | 18s    |
| 16 | CW   | 5.8GHz     | x    | x     | 3.4%  | TVW-CSD    | 2-5s   |
| 13 | CW   | 14GHz      | 5m   | x     | 2.2%  | AD         | 20-30s |
| 16 | UWB  | 24GHz      | x    | x     | *1%   | FBTS       | 20-55s |  


- Vital Signs Mmwave Results  

|    | Type | Frequency  |Dist  | BR Err| HR Err| Method     |Duration|
|--- |---   |---         |---   |---    |---    |---         |---     |
| 15 | FMCW | 75-85GHz   | 1m   | 6.89% | 8.09% | FFT        | 100s   |
| 19 | FMCW | 77-81GHz   | 1.7m | 6%    | 20%   | AD-FFT     | 40min  |
| 16 | CW   | 60GHz      | 1m   | 2%    | 3.3%  | FFT        | 10min  |
| 19 | UWB  | 60.5GHz    | x    | x     | x     | MRC        | 150s   |
| 12 | CW   | 60GHz      | x    | x     | x     | FFT        | 20s    |  

- 본 논문에서 다룰 내용  
&emsp; +. 빠르고 정확한 추정  
&emsp; +. AD with FFT, DC Compensation (Linear Least Square Estimator, LLSE)  
&emsp; +. MIMO 기능 활용을 통한 추정결과 개선  
  + long term use may not be practical (FCC Part 15.255)
  + frequency bands 관련 EIRP[^EIRP] 규정 (for Tx, as of 2013 in FCC 78 FR 59844 (09/30/2013))
  &emsp; 57~65GHz에서,   
  &emsp; +. average power  : ~ 40dBm   
  &emsp; +. peak power : ~ 43dBm   
  &emsp; 77GHz에서  (vehicular radar의 경우, 76 ~ 81GHz band에서 적용)
  &emsp; +. average power : ~ 50dBm
  &emsp; +. peak power : ~ 56dBm  


- SSM[^SSM]  
&emsp; +. 측정된 심박수의 SNR 향상, 현재 MIMO에서도 SNR 개선   
&emsp; +. UWB, SFCW 방식에 적용  
&emsp; +. arctangent demodulation (AD)과 complex signal demodulation (CSD) 후에 적용  

## ---  
- 범위 정보는 샘플링 주파수($f_s$) 및 처프 스위프 기울기에 의존
- range resolution은 sweap bandwidth($B_w$)에 의존
- The number of chirps per second:  
&emsp; +. duty cycle 증가  
&emsp; +. 자세한 object의 range & azimuth 제공  
- sampling point는 sampling frequency bin과 같음  
- sampling rates가 높을수록 sample points per chirp 제공 ... 더 많은 range bins 처리  


## Vital Sign Signal Processing
### 1. Phase based Methods
- CSD (Complex Signal Demodulation) & AD (Arctangent Demodulation)
- CSD : slow-time 축에서 target의 range profile 추출 → 추출된 range bin에 대해 FFT → HR/BR signal 추출  
- AD : range profile에 대해 IQ signal의 phase 획득 → specified bin에서 FFT

### 2. State Space Method  
- 

### 3. Time Varying Window
- 심박수의 빠른 획득을 위한 측정은 2~5초 내에 이루어 짐.  
&emsp; +. 스펙트럼 분해능 관련 문제 발생 : slow-time 축 $f_s$ 및 FFT의 포인트 수 $N$에 따라 달라지기 때문...(더 많은 사이클 필요), 획득 시간 증가  
- sampling rate 감소는 스펙트럼 해상도 인터벌 감소  
- but FMCW나 SFCW radar의 경우 slow-time 축 sampling은 적용하지 않음  
  &ensp; ($N$은 시스템에서 계산된 range bin에 따라 달라지며 1주기 동안 $N$은 $f_s$보다 크지 않기때문)  
- 표준 FFT를 사용하여 acquisition 주기를 늘리는 것만으로도 주파수 해상도는 증가할 수 있다.

### 4. Real-time Capabilities

#### 4.1. Processing Chain


#### 4.2. Extriacting A Commerical Algorithm for Offline Testing

### 5. Programming the AWR1642 for MIMO Output


### 6. MIMO Processomg


---

[^SSM]: state space method 
[^EIRP]: Equivalent Isotropically Radiated Power (등가 등방성 전력)
