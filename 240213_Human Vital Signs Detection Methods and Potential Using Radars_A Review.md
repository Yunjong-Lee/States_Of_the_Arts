---
date: 2024-02-13 10:07:20
layout: post
---

# Human Vital Signs Detection Methods and Potential Using Radars: A Review  
- [M. Kebe, R. Gadhafi, B. Mohammad, M. Sanduleanu, H. Saleh and M. Al-Qutayri, "Human vital signs detection methods and potential using radars: A review", Sensors, vol. 20, no. 5, pp. 1454, 2020.](https://www.mdpi.com/1424-8220/20/5/1454)   
- 측정 방식에 따라 광혈류 측정 방식, 공기 기반(화학, 온도, 습도 등) 측정 방식, 흉벽 변위 측정 방식, 마이크 기반(심전도 측정) 방식, Radar 기반 측정 방식 등 으로 분류됨. 

## 1. 광혈류 측정
- 적색(500n) 및 노란색(600n) 파장을 가진 발광 다이오드를 이용하여 빛을 방출하면 광 검출기(PD)는 반사된 빛을 수신하여 그 강도(심장 주기의 수축기-이완기 동안 변화)를 기록)을 이용한 직접 접촉을 통해 부피의 변화 측정
- PD는 반사/투과 모드에 따라 발광체와 같은 쪽 또는 반대쪽에 위치
- 녹색은 HR 획득에 널리 사용(신체 조직의 감쇠는 낮은 광학 파장 영역에서 높기 때문에, 녹색/황색 영역을 사용하는 PPG 시스템은 반사율 모드에 주로 사용되며 전송 모드는 적색/적외선 광학 신호를 선호한다)
- 이 두 가지 방법은 전송 모드에서 더 높은 정확도의 혈중 산소량을 얻을 수 있으나, 심박수 또는 심박수 변동성의 측정 정확도 측면에서 낮은 정확도를 가짐. 맥박 산소 측정은 이 모드에서 정맥 진동이 덜 강조되기 때문에 전송 모드를 사용합니다[42] 따라서 더 높은 신호 대 잡음비(SNR) 신호가 생성된다.
- 호흡은 수신된 신호의 진폭/주파수 변조를 유발하기 때문에 호흡 수는 PPG로부터 추정될 수 있음.
- 호흡 주기에 baseline wander/dc offset 이 발생된다.
- 반사 모드는 호흡 중 쟁맥압에 더 민감하므로 호흡 수 추정에 자주 사용된다.
- PPG monitoring : cellular phone or camera 기반(Video Plethysmography, VPG)이 주류이며, 심박수의 대략적인 값 제공


## 2. 공기 측정
- 화학 센서
    + CO2 수준 측정(들이마신 공기에는 0.04%의 이산화 탄소 포함, 내쉬는 공기에는 약 6%의 이산화 탄소 포함)
    + 가장 일반적으로 사용되는 센서는 적외선 센서와 광섬유 센서임
- 온도 센서 (서미스터, 두 도체사이의 온도 차이로 인한 천압 신호를 생성하는 열전센서)
    + 들숨과 날숨의 온도차(약 15도) 측정

- 습도 센서
    + 들이마신 공기의 관련 습도는 날숨의 습도와 약 20%에서 60% 정도 차이
    + 정전 용량 및 저항 센서는 습도에 대한 노출로 인해 각각 정전 용량과 저항 값 변화  


## 3. 흉벽 변위 감지 및 혈압 감지 방법
- 흉벽 변위
    + 횡격막과 호흡 근육 활동은 가슴의 변위를 초래(최대 7.37cm까지 팽창)
    + 가속도계/자이로스코프/자력계 등을 사용한 변형 감지, 경흉부 임피던스 감지, 또는 임피던스 폐경 및 움직임 감지
    + 광섬유센서(변형 기반 호흡센서로 사용 가능)는 저항성, 용량성 및 유도성 센서에 비해 응답 시간이 더 빠르거 감도가 높다.
- 혈압 감지 (침습/비침습)
    + 비침습적 방법 : 촉진, 청진, 초음파, 안압계 및 오실로메트릭 감지


## 4. 심전도(PCG)
- 판막이 열리고 닫히는 동안 심장은 마이크가 감지할 수 있는 소리(심장 근육의 수축 및 이완, 심장의 압력 상승 및 하강, 판막의 개폐, 혈액 순환 및 정지를 포함한 동작 등) 생성


## 5. Radar 기반 
### 5-1. (un-modulated) CW Radar 
#### 5-1-1. Algorithm
##### A. time-frequency analysis
- respiration and heart signal의 peak 검출
    > FFT 변환을 통해 자기상관 출력  
    > 시간 영역 데이터의 통계 기반 방법 (시변 신호와 정지 물체의 신호 구별)   

- frequency 방법(FFT required)
    > fourier 변환과 chirp-z변환울 이용하여 생체신호 추출   
    > arctan 복조와 complex signal 복조

- arctan 복조
    > 기저대역 신호는 I/Q phase 신호로 나뉘고, 나누어진 결과로 신호의 arctan를 얻는다.
    > FFT 변환을 통해 심장 박동과 호흡 신호의 스펙트럼 추출 (DC offset 제거 위해 FFT 전에 미분기 사용이 일반적)
    > local oscillator 및 믹서의 위상 잡음에 둔감, I/Q 기저대역 신호의 DC offset 및 위상 불균형에 의해 제한된다.

- complex signal 복조(FFT의 대안으로 사용할 수 있음)
    > 기저대역 I/Q 신호를 복소수 형태로 변환(베셀 함수 사용)하고, 변환된 결과를 복소 푸리에 변환  
    > DC offset에 대해 robust and tolerant

- 기저대역 신호의 harmonics and noise에 취약
    > 다양한 수치 분석 방식(mean, least square, HOUGH transformation, particle filter (PF))을 통해 data의 offset component 식별  
        - mean : 위상이 0~2ㅠ 구간에서 offset이 유지된다고 가정하여 신호의 offset 추정  
	    - ls : 데이터는 offset에 해당하는 중심이 있는 원에 맞춰진다.  
	    - HOUGH : 데이터는 그리드 셀로 나뉘고 Hough 변환은 그리드에서 원을 정의하는 데 사용됩니다.  또는 베이지안 필터를 PF로 사용하여 데이터의 offset 추정  
	    - 벡터 차이에 기반한 직접 위상 추정 : vital sign 추정  
	    - EKF[115] : 심폐수 추정  
	    - wavelet 분석 : 저주파 신호에 대한 효과로 인해 HR, BR 결정  

##### B. numerical analysis, 
- classification/training algorithms  
    > 호흡과 신체 움직임에 따라 다양한 수면 단계 분류[118]  
    > 수면/각성 패턴을 결정하기 위한 선형 판별 분류기 사용[119]  

- mathematical/experimental modeling
    > 폐 용적과 흉벽 변위 사이의 선형 관계[120] 기반 조석량을 추정  
    > 폐내압과 흉벽 변위와 관련된 수학적 모델[121],  그런 다음 Doppler 레이더의 base-band 신호를 사용하여 호흡량(/회) 추정  

#### 5-1-2. Issue
- 널 포인트 감지, LO 및 믹서의 위상 노이즈로 인한 신호 손상, 대상의 무작위 신체 움직임(RBM), 호흡 신호에서 심박 신호 분리 등

- 다중 타겟 감지 등 널 포인트 감지 및 위상 잡음
    > CW 트랜시버 아키텍처 (낮은 IF 단일 SSB), 신호 처리(CSD)[111]

- RBM, 정확한 심장 박동 감지 및 다중 피사체 감지
    > 정교한 아키텍처와 신호 처리 (레이더의 복잡성과 전력 소비 증가 ← 생체 신호 레이더 상용화 안된 이유[127])

- RBM 제거 메커니즘(RBM에 의해 셍상된 신호는 필수 신호의 손상 원인)
    > RBM 제거 메커니즘 : 두 개의 동일한 CW 송수신기와 CSD 사용[122].
    > 자체 주입 잠금을 사용한 레이더[128]
    > EMD(Empirical Mode Decomposition) 신호 처리(안테나와 피사체에서 움직임 아티팩트 제거)[129-130], 섹션 3.5 참조  

- 심장 박동 주파수(1Hz ~ 3Hz)는 호흡 주파수(0.1Hz ~ 0.9Hz)에 가깝기 때문에 호흡 신호의 고조파에 의해 손상 가능(심박 신호는 호흡 신호에 비해 진폭이 작다)
- 심장 신호와 호흡 신호를 분리 위한 매개변수화된 복조 방법 사용[131]
- 매우 좁은 빔, 이중 헬리컬 안테나를 갖춘 간단한 직접 변환 레이더(자동차 애플리케이션용)[132]
- 강한 호흡 신호가 있을 때 작은 심장 박동 신호 감지 방법 : 밀리미터파(mm-wave) 주파수 사용
- 표적의 변위로 인한 위상 변화는 반송파 파장에 반비례 ... 심장 박동으로 인한 흉벽의 작은 움직임은 더 높은 레이더 반송파 주파수에서 정밀하게 감지될 수 있다
- 신호 처리없는 BR과 HR 감지 밀리미터파 레이더[133, 134]
- 다수의 생체 신호 동시 감지(단일 톤 CW 신호는 범위 정보를 제공할 수 없음[135])  


### 5-2. FMCW Radar
- 신호는 매 주기 T마다 생성되는 chirp 신호로 구성되며, 시간에 따라 선형적으로 output signal이 변화
- chirp은 VCO에 linear voltage가 인가되거나 frequency synthesis와 PLL을 이용하여 생성  
※ transceiver 구조는 CW와 유사하지만, computation load를 줄이기 위해 direct-conversion system이 주로 사용된다. direct-conversion이란 수신 신호를 변환할 때,  전송된 신호의 복제본을 이용하여 변환하는 방법, de-chirpping이라고 함)
- de-modulated signal을 beat signal이라고 하며, range와 doppler 정보를 포함하고 있다.
- data의 형태는 slow-time/fast-time data를 포함하는 matrix 형태
    > slow-time data: 전송된 램프 수와 관련되며 범위 정보를 포함
    > fast-time data: 램프당 샘플 수를 나타내며 활력징후 정보를 포함

#### 5-2-1.  Algorithm
- basic algorithm은 localization and detection(BR, HR)

![Vital Signs Extraction Algorithm](https://www.mdpi.com/sensors/sensors-20-01454/article_deploy/html/images/sensors-20-01454-g012-550.jpg)
- noise, DC offset, MA 등을 제거하기 위해 다양한 신호처리 기법이 필요

- time-freq. method
    + FFT 기반 [^138]
- 자동 회귀 알고리즘 (Auto-Regression Algorithm, AR)
    + 신호에서 규칙적인 주파수를 찾아 HR & BR 추출[^139]
    + 범위와 위상 정보는 parametric 데이터 추정과 FFT 변환을 통해 획득  
- 환자(lying on bed)의 활력 징후 결정에 FFT 및 DC 보상 기법 사용[140]
- multiple antennas to detect and locate the vital signs of two objects[141]
- DC compensation은 Vital Sign의 검색 전에 phase unwrapping 처리가 중요(정확도: HR_80% & BR_94%)
- user-induced motion artifact 제거 
    + 특정 신호 에너지 임계값을 초과하는 time window signal energy 생략

```mermaid
  graph LR
  A[Acquisition]
  B[Feature_Extraction]
  C[VitalSign_Detection]

  A-->B-->C
```

#### 5-2-2.  Issue
- RBM 효과, 호흡 신호와 심장 신호의 분리, incoherence 등 issue
- incoherence는 위상 데이터에 포함된 마이크로 도플러 신호를 감지할 수 없을 때 발생[137] 
    + radar waveform의 phase control 필요  
- 범위 분해능: 대역폭에 의해 제한[143]
    + 해상도가 높을 수록 대역폭도 높아진다. (예 : 10GHz FMCW 레이더의 범위 분해능은 약 1.5cm)
- VCO 설계시 높은 위상 잡음 수준으로 인해 까다롭고, VCO는 선형 주파수 스위핑을 나타내지 않을 수 있다. 따라서 선형성을 유지하기 위해 고대역폭 FMCW 레이더[143, 144] 작동 시 교정 필요.
- FMCW 레이더가 CW 레이더에 비해 전력 소비가 많다


### 5-3. SF(Stepped Frequency) CW Radars [147-149]  
- N개의 frame (각 프레임의 시간간격은 $\Delta f$)  
- FMCW와 operation 유사, 반사된 신호로부터 beat frequency 추출  
- localization & multi-subject target detection 가능  
- 콘크리트 아래(1m 이상 이격)에 있는 사람의 생체신호 감지(피사체의 자세에 무관)  
- 상대적으로 낮은 전력 소비로 거리 정보와 마이크로 도플러 정보 제공

#### 5-3-1. Algorithm & Signal Processing  
- FFT 기반 peak 감지
- base-band 데이터는 시간-주파수 행렬(J×N, J = 총 주파수 sweep 수, N은 무선 주파수(RF) step 수) 입력[145]
- FFT 변환 (get Range-Doppler profile)

#### 5-3-2. Issue
- motion artifact of subject
- harmonics에 의한 정확도 감소  


### 5-4. IR-UWB Radar  
- 수신기에 수신된 echo(전송된 펄스의 지연된 복제본) 신호로부터 샘플링  

#### 5-4-1. Algorithm
- MHOC(Multiple High Order Cumulant) algorithm : SNR 개선, 높은 고조파 감소
- Hilbert Huang 변환 [HHT] 및 시간-주파수 영역의 FFT[153] : 수신 신호 처리
- arctangent 복조 및 complex signal 복조 : 생체 신호 추출
- 특이값 분해(SVD) : clutter 제거
- 앙상블 경험적 분해(EEMD), 연속 웨이블릿 변환(CWT) : SNR 개선, 호흡/심박 신호 분리

#### 5-4-2.  Issue
- 전력 밀도 제한(안전 및 다른 장치와 간섭 발생, 실내 애플리케이션에 대해 -41.3dBm/Hz로 제한_US)되므로, 단거리 용도에 적합
- 낮은 신호 전력은 높은 SNR을 가짐


### 5-5. Doppler Radar의 Random Body Movement(RBM) Cancellation
- 두 개의 동일한 CW 송수신기와 CSD 사용 [111]
    + 하나는 피험자 앞에 배치되고 다른 하나는 뒤에 위치  
    + 두 트랜시버에서 수신한 신호의 스칼라 곱으로 RBM 효과 제거  
- self-injection locking[128]
    + 2 Ant.를 앞/뒤로 배치
    + 전면 Ant.에서 송신한 신호를 다시 수신한 뒤에 후면 Ant.로 전송 (정면에서의 반사 계수와 후면에서의 반사 계수가 반대이므로 random body movement가 사라짐)

---
