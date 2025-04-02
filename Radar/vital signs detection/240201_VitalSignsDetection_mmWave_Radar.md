---
date: 2024-02-01 09:44:54
layout: post
---

# [Paper: Vital Sign Detection Using Millimeter Wave Radars](https://trace.tennessee.edu/cgi/viewcontent.cgi?article=7143&context=utk_gradthes)
- vital sign detection with Radar 동향 논문, University of Tennessee, 5-2020

## Introduction  

- Vital signs State of Art

|    | Type | Freq (GHz) |Dist  | BR Err| HR Err| Method  |Duration|
|--- |---   |---         |---   |---    |---    |---      |---     |
| 16 | UWB  | 1.5{4.5)| 0.8m | x     | 1.7%  | SSM-AD/CSD | 18s    |
| 15 | SFCW | 2-4     | 1m   | x     | 1.6%  | SSM        | 18s    |
| 16 | CW   | 5.8     | x    | x     | 3.4%  | TVW-CSD    | 2-5s   |
| 13 | CW   | 14      | 5m   | x     | 2.2%  | AD         | 20-30s |
| 16 | UWB  | 24      | x    | x     | *1%   | FBTS       | 20-55s |  


- Vital Signs Mmwave Results  

|    | Type | Freq (GHz) |Dist  | BR Err| HR Err| Method  |Duration|
|--- |---   |---         |---   |---    |---    |---      |---     |
| 15 | FMCW | 75-85   | 1m   | 6.89% | 8.09% | FFT        | 100s   |
| 19 | FMCW | 77-81   | 1.7m | 6%    | 20%   | AD-FFT     | 40min  |
| 16 | CW   | 60      | 1m   | 2%    | 3.3%  | FFT        | 10min  |
| 19 | UWB  | 60.5    | x    | x     | x     | MRC        | 150s   |
| 12 | CW   | 60      | x    | x     | x     | FFT        | 20s    |  


- 주제
  + performance 관점에서,
    - 빠르고 정확한 추정 (long term use may not be practical, FCC Part 15.255)  
    &ensp; : AD (Arc-tangent Detection) with FFT, DC Compensation (Linear Least Square Estimator, LLSE), [^Ref_5]  
    - MIMO & MRC 기능 활용을 통한 추정결과 개선, [^Ref_3]  
    ※ 추정 및 개선관련하여, feature extraction methods에서 가능성을 보임
   
  + frequency bands 관련 EIRP[^EIRP] 규정 (for Tx, as of 2013 in FCC 78 FR 59844 (09/30/2013))  
    - 57~65GHz에서,  
      * average power  : ~ 40dBm  
      * peak power : ~ 43dBm  
    - 77GHz에서  (vehicular radar의 경우, 76 ~ 81GHz band에서 적용, part 95)
      * average power : ~ 50dBm  
      * peak power : ~ 56dBm
          
  + PoC
    - holding breath [^holding_breath]
    - estimates on short time scales [^short_time_scale_1] [^short_time_scale_2]

  + SSM[^SSM]  
    - 측정된 심박수의 SNR 향상, 현재 MIMO에서도 SNR 개선   
    - UWB, SFCW 방식에 적용  
    - AD과 complex signal demodulation (CSD) 후에 적용  

## ---  
- 범위 정보는 샘플링 주파수($f_s$) 및 처프 스위프 기울기에 의존
- range resolution은 sweap bandwidth($B_w$)에 의존
- The number of chirps per second:
  + duty cycle 증가
  + 자세한 object의 range & azimuth 제공  
- sampling point는 sampling frequency bin과 같음  
- sampling rates가 높을수록 sample points per chirp 제공 ... 더 많은 range bins 처리  

---

## 4. Vital Sign Signal Processing  

range profile은 하나의 chirp의 FFT 결과로 얻어진다. 하나의 column이고 각각의 row(행)는 대상 거리에 해당하는 beat freq.

### 4.1. Phase based Methods
- CSD (Complex Signal Demodulation) & AD (Arctangent Demodulation)
- CSD : slow-time 축에서 target의 range profile 추출 → 추출된 range bin에 대해 FFT → HR/BR signal 추출  
- AD : range profile에 대해 IQ signal의 phase 획득 → specified bin에서 FFT

### 4.2. State Space Method  
- 

### 4.3. Time Varying Window
- 심박수의 빠른 획득을 위한 측정은 2~5초 내에 이루어 짐.  
&emsp; . 스펙트럼 분해능 관련 문제 발생 : slow-time 축 $f_s$ 및 FFT의 포인트 수 $N$에 따라 달라지기 때문...(더 많은 사이클 필요), 획득 시간 증가  
- sampling rate 감소는 스펙트럼 해상도 인터벌 감소  
- but FMCW나 SFCW radar의 경우 slow-time 축 sampling은 적용하지 않음  
  &ensp; ($N$은 시스템에서 계산된 range bin에 따라 달라지며 1주기 동안 $N$은 $f_s$보다 크지 않기때문)  
- 표준 FFT를 사용하여 acquisition 주기를 늘리는 것만으로도 주파수 해상도는 증가할 수 있다.

### 4.4. Real-time Capabilities

#### 4.4.1. Processing Chain


#### 4.4.2. Extriacting A Commerical Algorithm for Offline Testing

### 4.5. Programming the AWR1642 for MIMO Output


### 4.6. MIMO Processomg


---

[^SSM]: state space method   
[^EIRP]: Equivalent Isotropically Radiated Power (등가 등방성 전력)   
[^Ref_3]: T. Sakamoto. Noncontact measurement of human vital signs during sleep using low-power millimeter-wave ultrawideband mimo array radar. In 2019 IEEE MTT-S International Microwave Biomedical Conference (IMBioC), volume 1, pages 1–4, May 2019. 2, 5, 51, 52, 95   
[^Ref_5]: T. Sakamoto, R. Imasaka, H. Taki, T. Sato, M. Yoshioka, K. Inoue, T. Fukuda, and H. Sakai. Feature-based correlation and topological similarity for interbeat interval 
estimation using ultrawideband radar. IEEE Transactions on Biomedical Engineering, 63(4):747–757, April 2016. 2, 3, 5  
[^holding_breath]: Huey-Ru Chuang, Hao-Chung Kuo, Fu-Ling Lin, Tzuen-Hsi Huang, Chi-Shin Kuo, and Ya-Wen Ou. 60-ghz millimeter-wave life detection system (mlds) for noncontact human vital-signal monitoring. Sensors Journal, IEEE, 12:602 – 609, 04 2012. 4, 5  
[^short_time_scale_1]: M. Alizadeh, G. Shaker, J. C. M. D. Almeida, P. P. Morita, and S. Safavi-Naeini. Remote monitoring of human vital signs using mm-wave fmcw radar. IEEE Access, 7:54958–54968, 2019. 4, 5, 31  
[^short_time_scale_2]: Zhicheng Yang, Parth Pathak, Yunze Zeng, Xixi Liran, and Prasant Mohapatra. Monitoring vital signs using millimeter wave. pages 211–220, 07 2016. 4, 5  
