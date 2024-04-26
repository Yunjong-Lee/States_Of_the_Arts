---
date: 2024-02-13 10:07:20
layout: post
---


# UWB radar signal processing in measurement of heartbeat features
- [IEEE Int. Conf. Acoust., Speech Signal Process. (ICASSP), Mar. 2017, pp. 1004-1007](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=7952307)

## 1. Abstract
- 심장 박동 및 호흡 특성을 정밀하게 모니터링할 수 있는 비접촉 센서인 초광대역(UWB) 레이더의 새로운 신호 처리 알고리즘을 소개

- 심장 박동 특징을 나타내는 새로운 자유 간섭 신호 제안(인간 흉벽의 반사 신호와 맞는 고조파 계열 표현 모델 활용 및 새로운 시변 필터 활용)

- HR 및 HRV를 추출하는 새로운 처리 절차 제안

- Doppler Radar의 단점
    > 측정 정확도에 영향을 주는 요소로, 레이더와 대상 사이의 거리, 고정 클러터 및 누화 등이 있음
    
- UWB Radar  
    > 높은 범위 분해능으로 인해 호흡은 흉벽에서 산란된 수신 펄스의 시간 지연으로 감지(심폐 활동이 시간에 따라 변하는 지연으로 나타남)  

- 연구 동향  
    > 호흡 분석 및 오염된 수신 신호의 위상 추정/간섭 완화  

- 시변 지연과 도플러 위상 변조를 모두 고려
    > 기존의 UWB 접근 방식은 시변 지연[5, 7-9] 또는 도플러 위상 변조[2]를 사용하여 활력 징후를 추출

- 활력 징후 추출을 위한 알고리듬 제안 및 제안된 알고리듬과 HAPA 알고리듬 비교


## 2.  SYSTEM MODEL AND PROBLEM STATEMENT
- radar로부터 $R [m]$ 떨어진 object(사람의 흉부)를 향해 $T_p$ interval을 가지는 동작 주파수 $f_c$의 waveform $u(t)$를 송신한다고 가정할 때, 송신신호 $s(t)$ ; 
    + $s(t)= \displaystyle \sum_{n} u \Big (t-nT_p \Big )$
- Generalized Gaussian Pulse (GGP)는 물리적으로 구현할 수 있는 좁은 pulse 파로, GGP의 시간영역 함수 
    + $u(t) = A exp \left (-4 \pi \Big (\frac {t-t_0} {\Delta T} \Big )^2 \right) $, &emsp; $0 \le t \le T_p$ &emsp; &emsp; (2)
        > A : 시간 $t = t_0$에서 waveform의 peak  
        > $\Delta T$ : 펄스 폭  
        > $\Delta T + t_0 << T_p$  

- 신호 $s(t)$가 흉부와 충돌한 후 scatter될 때 채널의 시변 임펄스 응답 $h(t)$ :   
    + $h(t) = a_r \delta \Big ( t - \tau _r (t) \Big ) + \displaystyle \sum _{i=1, i \ne r} ^{P} a_i \delta ( t - \tau_i ) $  
        > - 1번째 항 (흉벽 위치에서의 산란 효과 관련 항)  
            >> 호흡과 심장 박동에 의해 주기적으로 움직이며, 시간에 따라 변하는 지연을 발생시킴(식 4로 모델링)
        > - 2번째 항 : 고정 산란체 관련 항  
            > $\delta( \cdot )$은 direc delta이다.  
            > $\tau_i = \frac{2R} {C} $는 i-번째 산란점으로부터 수신된 신호의 시간 지연  
            > Complex Coefficient $a_i$는 송/수신 안테나의 조합 효과(combination effects)와 i-번째 산란 점의 radar cross section(반사 면적)

- 호흡과 심장 박동에 의한 수신 신호의 시간 지연 $\tau _r(t)$은  
    + $\tau _r(t) = \frac{2R} {C} + \tau _b sin(2 \pi f_b t) + \tau _h sin(2 \pi f_h t)$ &emsp;&emsp; (4)
        > . $f_b, f_h$는 breathing and heartbeat rate ($f_b << f_h$)  

- 시변 위상 변화는 이 지연(Doppler phase modulation이라고 알려져 있음)에 의해 생성된다.
    + $\phi _r (t) = 2 \pi f_c \tau_r (t) $
        > . $\tau _i$에 비해 $\tau _r(t)$의 변화는 매우 느려서 채널 모델에 대해 가정된 시스템은 시간 불변으로 가정된다. 

- 베이스밴드에서 수신된 신호 $r(t)$  
    + $r(t) = a_r e^{ j \phi _r (t) } \displaystyle \sum _{n} u \Big( t - \tau_r (t) - nT_p \Big) +\displaystyle \sum _{i=1, i \ne r} ^{P} \displaystyle \sum_n a_i u ( t - \tau_i  - nT_p) +n(t)$ &emsp;&emsp; (5)  
        > . $n(t)$ : AWGN(thermal noise)  
        > . 심폐기능은 흉부로부터 수신된 신호의 시간 지연 변화와 Doppler 위상 변조 $\Psi_r (t) $)에 숨겨져 있다   
        > . Doppler 위상 변조는 수신된 신호의 스펙트럼에서 에너지 감지를 통해 detect(호흡 rate와 심박 rate의 조합)  
        > . $\tau_b ≫ \tau_h$로, 호흡수는 심박수 정보가 가려지고, 수신 신호의 스펙트럼에는 호흡 운동에 의해 영향을 받는 간섭이 다수 존재  

    + solution_1. 호흡률을 감지하고 도플러 위상 변조에서 호흡 동작을 필터링
        > . r(t)를 장기간 관찰하면 시간 지연에서 호흡수를 나타내는 harmonic(고조파) 변화 감지  
        > . 이 속도는 호흡 동작 감지(RMD)로 알려진 알고리즘에 의한 고조파 변화로부터 감지 가능[8]  
        > . RMD를 사용하여 호흡수를 감지하고 도플러 위상 변조에서 호흡 활동 부분을 필터링함으로써 심박 기간을 증폭시킬 수 있다  

    + solution_2. $f_b ≪ f_h$이므로, r(t)의 유도에 의해 호흡 기간에 대한 심박 기간 비율 증폭
        > . 이 derivation은 간섭 제거 기능을 가지나, 시스템의 광대역 신호 및 잡음으로 인해 derivation시 잡음도 크게 증가  

![Block diagram of signal processing algorithm](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/7943262/7951776/7952307/7952307-fig-1-source-small.gif)

![RMD procedure in detection of breathing rate](https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/7943262/7951776/7952307/7952307-table-1-source-large.gif)


## 3. HEARTBEAT EXTRACTION ALGORITHM
### Finding Breathing rate and Removing clutters  
- $\tau$와 $T_p$는 
- $f_b$와 $f_h$는 작은 값이기 때문에 초 단위의 시간 동안 관찰하면 $\tau_r(t)$의 시간 변화가 감지됨 ($\tau_r(t)$의 시간 인덱스 t는 slow-time variable)
- 수신된 신호는 u(t)와 일치하는 필터에 의해 필터링(시간 폭은 $ΔT$)
- 필터의 출력은 샘플링 속도 $ΔT$의 샘플링된 신호 $\hat{r}(i)$, 각 기간 동안 N개의 샘플 포함(각 샘플은 특별한 범위 간격을 나타내며 범위 셀임)
- 샘플링된 신호의 주기를 평균(AWGN 평활화) 한 뒤 range profile 생성  
    > . 각 $T_{st} = LT_p$ sec 마다 하나의 range profile 생성  
    > . q번째(q = 1, ..., Q) range profile의 모든 N 범위 셀은 fast-slow time Q × N 행렬 R의 q번째 행(fast dimension) 형성

- RMD 알고리즘[8,9] process :

```mermaid
graph LR;
    A(선형 추세 제거: for static clutter removal)-->B(DFT: fast-slow time matrix의 column_느린차원);
    B-->C(slow-time dimension frequency windowing);
    C-->D(cell-averaging);
    D-->E(임계값 설정 및 감지);
```

    > ※ interesting range cell이 감지되면, breathing rate가 detected되고, 클러터로 나타나는 다른 모든 정적 개체의 효과 제거 가능.

### HR Extraction
- tx signal $s(t) = \displaystyle \sum _{k = -K} ^K b_k e^{j \frac{2k \pi}{T_p} t}$ &emsp; &emsp; (6)  
    > - $b_k$ : complex coefficient of Fourier series of $u(t)$  
    > - K : 유효 components의 수
    > - $c_K$의 크기(amplitude)는 DC 성분보다 적어도 $\sqrt 2$배 작도록 결정  
    > . range cell의 static clutter는 Linear Trend Removal process에서 제거된다.  
    > . interesting range cell을 찾아 다른 range cell과 다른 object의 효과를 삭제할 수 있음  

- 식 (5)의 2번째 성분은 다음 과정에서는 고려되지 않음  
 
- 식(5)의 흉벽효과에 초점을 맞추고 식 (6)을 고려하면, 일차 필터 이후 수신된 샘플링 신호 $\hat{r} _s(t) = \displaystyle \sum _{k = -K} ^{K} c _{kr} (i) e ^{ j \frac{2k \pi}{T_p} i} + \hat {n}(i)$ &emsp;&emsp; (7)
    > + $c _{kr} (i) = \alpha _{kr} e ^{j (2 \pi f _c + \frac {2k \pi} {t _p} ) \tau _r(i)} $  
    > + $\alpha_{kr}$ : complex constant  
    > + $\hat {n}(i)$ : noise (after match filter), ultra wide-band  
    > 심폐 기능은 $\hat {r} _s(i)$의 미분에 의해 나타난다.  
    > + $c_{kr} (i)$ : narrow-band signal  
    > ※ narrow-band filter는 $c_{kr} (i)$ 추정에 사용  
    > ※ cardiopulmonary(심폐) features는 추정된 $c_{kr} (i)$의 미분으로부터 추출  
    > $c_{kr} (i)$의 통계적 특징은 $\alpha_{kr}$ 의 통계적 특징과 유사하고, 짧은 시간 관측에서는 움직이지 않지만(stationary) 시변 위상으로 인해 긴 시간 관측에서는 통계적으로 움직이는(non-stationary) signal임.  
    > 협대역 필터링은 긴 시간 관찰이 필요하므로 $c _{kr}(i)$ 추출에는 non-stationary signal에 적합한 시변 필터를 사용(현재 FIR 시변 필터 사용)해야 한다.
    > + 추정된 $c _{kr}(i)$는  
        > $= \displaystyle \sum _{l = 0} ^{M-1} h _{ \dot {k} l} (i) \hat{r} (i-k) = \vec {h} _k (i)^H \vec {r} (i) + n _c(i),$ &emsp;&emsp; (8)  
        > $\vec{r} (i) = [ \hat{r}_s (i), \cdots ,  \hat{r}_s (i-M+1)]^T$  
        > $ \vec{h} _k (i)$ : FIR filter의 $M x 1$ time-varying coefficient vector  
        > $n_c (i)$ : narrow-band noise  
        > superscript * : conjugate  
        > superscript H : hermitian matrix  
        > FIR coefficient 벡터를 결정하면, 필터링 프로세스는 완료된다.  
        > 0-th 이산 창형 타원체 시퀀스(DPSS)로 알려진 유한 샘플 간격에서 최대 에너지 농도를 갖는 최적 정규 직교 시퀀스로 $c _{kr}(i)$를 확장하고 다음을 고려한다.  
        > 최소 평균 제곱을 사용하면  FIR 필터의 최적 계수는  
        > $\vec{h} _{k} ^{opt} (i) = F_k \Phi (i),$  
            > $\Phi (i) = [\phi _1 (i)\phi _1 (i) \cdots \phi_M(i)]^T$  
            > $\vec{F}$는 $M × N$ 행렬  
                - $f_k (m,l) = \phi_l (m) e^{j \frac{1} {T_p} m}$  
        > $0 \le m \le M-1, 1 \le l \le M$는 DPSS orthogonal sequences  
        > $M=L, 2MB, ɺ$는 차수 표현, 여기서 $B < 0.6$이면 $c_{kr} (i)$의 정규화된 bandwidth

---

