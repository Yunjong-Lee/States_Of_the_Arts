---
date: 2024-05-10 09:56:11
layout: post
---

# [Noncontact Vital Sign Detection With an FMCW mm-Wave Radar](https://ieeexplore.ieee.org/abstract/document/10058900)  
- IEEE Sensors Journal, Volume: 23, Issue: 8, 15 April 2023  

---

# Index  

- I. Introduction  
- II. Related Works  
- III. Preliminaries  
- IV. System Implementation  
- V. Performance Evaluation

---

# Abstract  
- devices를 이용하여 Wi-Fi (2.4/5 GHz) 신호 추출이 가능함  
  &ensp; - 추출된 신로를 이용하여 Wi-Fi 기반 비접촉 센싱 응용(호흡감지, 위치추정, 동작 인식 등)에 활용 가능함  
  &ensp; - But, Wi-Fi는 다음과 같은 이유로 성능 제한이 있음  
  &ensp; &ensp; + narrow bandwidth, small(갯수) Ant., large wavelength.  
  &ensp; &ensp; + Wi-Fi의 wavelength가 심장의 움직임에 의해 만들어지는 흉벽 움직임 보다 크기 때문에 heartbeat에 의한 tiny pulse 변화를 capture하기 어렵다.  

  |       | wave length     |
  | ---   | ---             |
  | Wi-Fi | 60–120 mm       | 
  | 심장  | 0.2–0.5 mm [^13]|
   

- CW doppler radar는 전력 소모는 적으나, range 정보는 제공할 수 없음  
  
- UWB pulse radar and FMCW radar는 wideband를 이용하므로 object와 device간의 거리 측정 가능  
  &ensp; - UWB는 hardware cost와 system complexity가 높다  
  &ensp; - mmwave FMCW는 wide bandwidth와 narrow beamwidth를 가지므로 서로 다른 물체로부터의 반사를 구분하는데 유리, 소형화 가능.
  
- 기존 신호 처리 기술  
  &ensp; - 주파수 영역 변환 기법 (Fast Fourier Transform [^18] , Short-Time Fourier Transform [^19] , CW Transform [^20] 등) 활용
  
  &ensp; - RR 및 HR 추정  
  &ensp; &ensp; + 시간 영역 신호 처리 기술(앙상블 경험적 모드 분해(EEMD) [^21] , 자기상관 [^22] 및 적응 필터 [^23] 등) 사용  
  &ensp; &ensp; &ensp; → RR 감지의 경우, 간단하고 제어된 시나리오에서 작동 OK.  
  &ensp; &ensp; &ensp; → 그러나, 간섭(호흡 고조파, 잡음, 클러터 등)으로 인해 HR 감지 정확도가 낮다  
  &ensp; &ensp; &ensp; : 다양한 물체(예: 벽, 문, 책상, 가구)에 의해 반사된 신호가 심장 박동 신호를 압도할 수 있다  
  &ensp; &ensp; &ensp; : 호흡으로 인한 흉벽 변위가 심장 박동으로 인한 흉벽 변위 보다 클 수 있다(호흡 고조파는 심장 박동 신호에 가깝거나 압도하여 피크 선택이 잘못될 수 있다)  

- 이 문제를 해결(tackle)하기 위해 본 논문에서 제안하는 솔루션 : 4개의 function module을 구성  
  &ensp; - VS extraction module : VS신호를 추출하기 위해 clutter를 제거하고 VS 신호가 강한 body에 해당하는 range bin 결정. 그 다음에 느린 시간에 따라 생체신호를 추출 ~~하여 클러터 간섭 제거~~   
  &ensp; &ensp; Q. clutter를 제거를 위해 사용한 방법은?
  
  &ensp; - differential enhancement module : ~~HR 추정에 대한 호흡 고조파 및 잡음의 영향을 줄여 1차 시간차에 의해 heartbeat component를 향상시키는 역할~~  1차 시간차를 사용하여 타동 강화 모듈의 심장 박동 구성 요소를 강화하고 호흡 고조파 및 소음의 간섭 완화
  
  &ensp; - 신호 분해 모듈(signal decomposition module) : wavelet packet decomposition (WPD)를 통해 호흡 신호와 심박 신호를 분리하여 심박 신호의 호흡 고조파 및 고주파 노이즈 억제
  
  &ensp; - VS 비율 재구성 모듈(vital sign rate reconstruction module) : VS 비율의 희소 스펙트럼 재구성(sparse spectrum reconstruction, SSR)은 적응형 필터에 mapping되고, 제로 유인 부호 지수 망각 최소 평균 제곱 (zero attracting sign exponentially forgetting least mean square, ZA-SEFLMS) algorithm은 고해상도 희소 스펙트럼을 이용하여 VS 비율 재구성
  
  &ensp; &ensp; + 주파수 빈이 크게 증가하고 호흡 고조파 및 소음의 스펙트럼 전력 억제 가능  
  
- result는 설계된 mmRH가 호흡 고조파, 소음 및 클러터 간섭 억제 가능 및 기존 방법에 비해 RR/HR 감지 정확도 향상됨  


# Related Works  


# Preliminaries  


# System Implementation  

<img src="https://ieeexplore.ieee.org/mediastore/IEEE/content/media/7361/10102602/10058900/xiao2-3250500-small.gif">

## A. Vital Sign Signal Extraction Module  

- n번째 ADC 샘플과 m번째 처프에 대해, signal $y(n,m)$ can be expressed as  

  &emsp; - [Eq. 8] &emsp; $y(n,m) = \large{
                            \frac{A_T A_R}{2} \displaystyle\sum _{i=1} ^{\omega} exp [ j(2\pi \frac{2Bd_i×(nT_f)}{cT_d} nT_f + 4\pi \frac{d_i (nT_f + nT_s)}{\lambda} ) ]
                                            }$  

  &emsp; &emsp; + $T_f, T_s$는 time interval corresponding to the fast time and slow time, respectively.  
  &emsp; &emsp; + $d_i(t)$는  $i-th$ range bin에 있는 object와 radar 사이의 range  
  &emsp; &emsp; &emsp; [Eq. 9] &emsp; $d_i (t) = \hat{d}_i + \hat{d}_i(t)$  
  &emsp; &emsp; + $d_i$는 레이더와 반사체(i-번째 range bin) 사이의 거리이고, $d_i(t)$는 반사체의 시간에 따른 변위  
  
- Eq. (8)과 (9) 기반으로, m_th chirp $f_b$의 frequency는    
  &emsp; - [Eq. 10] &emsp; $f_b = \LARGE{ 
                                        \frac{2B(\hat d_i + \hat d_i(nT_f))}{cT_s} = \frac{2B \hat d_i}{cT_d} 
                                        }$   
  &emsp; - fast time displacement ( $d_i(nT_f)$ )는 chirp duration가 짧고, frequency 변화가 작기때문에 무시 가능.  
  &emsp; - 반사체의 range bin finding은 각각의 chirp에 대해 fast time 영역을 FFT (range FFT라고도 힌디)  
  &emsp; &emsp; + [Eq. 11] &emsp; $z(i, m) = \large{
                                              \displaystyle\sum _{n=0} ^{N-1} y(n,m)exp(-j2\pi \frac{in}{N})
                                              }$  
  &emsp; &emsp; &emsp; -->> 여기서, i는 range bin index  

  &emsp; - reflecting object의 range bin은 반사체가 없는 것의 range bin (empty bin)보다 많은 에너지를 가지므로 range FFT로 empty bin 필터링 가능.  
  &emsp; &emsp; &emsp; -->> empty bin의 예로는 correspond to wall, desk, or metal objects 등  
  &emsp; - 4 GHz의 BW를 가지는 FMCW radar 경우, range redolution이 3.75cm 이므로 반사체의 multirange bin 검출 가증  
  &emsp; &emsp; &emsp; : multirange bin으로는 팔, 다리 등
  
- 결과적으로, range FFT로 얻어진 range bin의 위상 변화를 관찰하여 선택된 range bin에서 vital signs 신호가 존재하는지 결정한다.  
  &emsp; -->> Q. range bin의 위상 변화를 관찰하는 방법 확인이 필요함
  
- Based on (8) and (9), the phase 는  
  &emsp; - $\phi = \large{
  \frac{ 4 \pi (\hat{d}_i + \hat{d}_i(nT_f + mT_s) ) }{\lambda} ≅ \frac{ 4 \pi (\hat{d}_i + \hat{d}_i(nT_f + mT_s) )) }{\lambda}
  }$
  
  &emsp; &emsp; 여기서, quasi-stationary human subject ( $\hat{d}_i$ )는 slow time에서 일정하게 유지되는 반사체와 레이더 사이의 거리이고,  
  &emsp; &emsp; chest wall displacement, $\hat{d}_i (t)$ 는 호흡과 심장박동으로 생겨나는 chest의 displacement이고,  
  &emsp; &emsp; fast time에서 흉벽 변위, $\hat{d}_i (nT_f)$ 는 짧은 chirp 주기로 인해 무시할 수 있고,
  &emsp; &emsp; slow time에서 흉벽 변위, $\hat{d}_i (mT_f)$ 는 pulse change가 발생한다. 그러므로, 강한 vital signs을 가지는 신체 부위에 대응하는 range bin에 대해서는 위상 변이가 크다(위상 변위가 특정 임계값 보다 높다).  

- range bin이 결정된 뒤에 phase signal(respiration signal, heartbeat signal, noise 등이 포함된)은 slow time을 따라 추춮된다.  

  &ensp; - $\phi = [\phi_1, &ensp; \phi_2, &ensp; ... , \phi_m]$

## B. Differential Enhancement Module  
Fig. 3(a) shows the phase signal $\large{ϕ}$ and its corresponding spectrum.  
~~The waveform with large amplitude is caused by respiration and varies significantly, while the tiny vibration at the top of the waveform is caused by heartbeat, which is weak and not visible.~~
- amplitude가 큰 waveform은 호흡에 의해 발생 (변동이 심함), 파형 상단의 작은 진동은 심장 박동에 의해 발생 (눈에 잘 띄지 않는다)  
~~It is apparent that the chest wall displacement is mainly modulated by respiration.~~  
  &ensp; - 호흡으로 인한 흉벽의 변위는 heartbeat으로 인한 것 보다 클 수 있다. ~~The chest wall displacement caused by respiration can be an order of magnitude higher than that caused by heartbeat.~~ 
- chest wall displacement(caused by respiration)는 순수한 사인파가 아니고, Fig 3(a) phase spectrum처럼 위상스펙트럼에 고조파를 포함. 
- respiration frequency $f_r$과 비교하면, heartbeat frequency의 power는 weak하고 2차 호흡 고조파 $2f_r$의 power와 쉽게 합쳐진다. 4차 호흡 고조파, $4f_r$와 noise, HR 추정이 부정확해 진다. 

<img src="https://ieeexplore.ieee.org/mediastore/IEEE/content/media/7361/10102602/10058900/xiao3abcd-3250500-small.gif">  

- HR 추정시 호흡 고조파와 Noise의 영향을 완화하기 위해 VS 신호 추출 후 1'st temporal difference가 수행된다.  
  &ensp; : 1'st order temporal difference가 수행되면, phase 신호의 heartbeat component가 강화됨.  
  &ensp; - 위상 신호 ($\large {ϕ}$)의 1'st order temporal difference  
  &ensp; &ensp; [Eq. 13] &ensp; $\phi = [\phi_2 - \phi_1, \phi_3 - \phi_2, ... , \phi_m - \phi_{m-1} ]^T$  
  &ensp; - 위상신호의 샘플 수 ($M$) 와 일관성을 유지하기 위해, 위상 차 신호 $\phi^\prime$는 식 (14)로 근사된다. ( Fig. 3b 참조 (phase difference signal and its corresponding spectrum) )  

  &ensp; &ensp; [Eq. 14] &emsp; $\phi^\prime = [0, \phi^{\prime T}]^T$  
  &ensp; &ensp; &ensp; :1'st order temporal difference는 heartbeat component가 강화되므로, $f_h$는 $2f_r$과 $4f_r$과 noise와 스펙트럼 내에서 비교시 명확해진다 (fig.3b 참조).  
  &ensp; &ensp; &ensp; ※ but, 완벽히 제거되지 않음. $f_h$의 power가 differential enhancement module 후에 강화되었지만, 호흡 고조파와 노이즈의 power보다는 낮음(fig 3 and 4).  
  &ensp; &ensp; &ensp; ※ 4치 고조파의 피크에 해당하는 주파수가 심박 주파수로 선택되어 큰 HR estimation 오류가 야기될 수 있다.  

## C. Signal Decomposition Module : WPD  
- 호흡으로 인한 chest wall movement의 범위는 1 to 12 mm (frequency로는 0.1–0.5 Hz)이고 heartbeat로 인한 chest wall movement는 0.2 to 0.5 mm (frequency로는 0.8–2.0 Hz)이다. [^5], [^14].
  |          |  range       | frequency    |
  |---       | ---          | ---          |
  |호흡      | 1 - 12 mm    | 0.1 - 0.5 Hz |
  |heartbeat | 0.2 - 0.5 mm | 0.8 - 2.0 Hz |
  
- 차동 강화 모듈 이후에 위상차 신호($ϕ′$)를 분해하고 호흡 신호($θ$)와 심박 신호($h$)를 재구성하기 위해 WPD를 적용한다.  
  + heartbeat와 respiration signals를 분리하면 호흡 하모닉의 간섭과 고주파 노이즈(Eq. 15)를 더욱 완화할 수 있다.   
  &emsp; [Eq.15] &emsp; $\large{    ϕ ^\prime = s_{g,0} + s_{g,1} + s_{g,2} +⋯+s_{g,2^g−2} + s_{g,2^g−1}    }$    
  &emsp; &emsp; -. $s$는 $g-th$ 계층의 WPD 이후의 subband signal  
  &emsp; &emsp; -. $q-th$ subband signal의 주파수 범위는  
  &emsp; &emsp; &emsp; $\large{    \frac{f_{slow}} {2^{g+1}} × q    }$ ⁓ $\large{    \frac{f_{slow}}{2^{g+1}} × (q+1)    } $, &emsp; $q = 0, 1, 2 ...$

- wavelet bias로 Morlet wavelet 선택  
  &emsp; - 선정 사유: 호흡과 심박 파형과 유사  
  &emsp; - WPD의 6번째 level에서 64 subband 신호를 얻을 수 있음  
  &emsp; &emsp; -. $θ = s_{6,0} + s_{6,1} + s_{6,2}$   
  &emsp; &emsp; -. $h = s_{6,5} + s_{6,6} + s_{6,7} + s_{6,8} + s_{6,9} + s_{6,10} + s_{6,11}$      
  &emsp; &emsp; -. 첫번째에서 세번째 서브밴드 신호는 호흡 재구성에 사용되며, 6번째부터 12번째 서브밴드 신호는 심박 신호 재구성에 사용됨.  
  &emsp; &emsp; -. WPD 이후, $Δ$초 간격으로 $δ$초 slide(이동)   
※ sliding time window를 가지는 호흡과 심박 신호에 따라 (signal with sliding time window), vital sign rate reconstruction module은 high-resolution sparse spectrum (정확한 RR과 HR 추정을 위해)을 얻기 위해 제안됨  

## D. Vital Sign Rate Reconstruction Module
### 1) SSR for Vital Sign Rate Reconstruction:
- SSR의 목적 : high-resolution sparse spectrum 획득  
  + high-resolution sparse spectrum 획득 방법: 식 20을 활용한 signal sparsity를 증가시키는 방벙 적용  
  + spectrum reconstruction은 underdetermined linear equation을 기반으로 얻어진다.  
  &emsp; &emsp; $h = \Psi e + \eta, \tag{18}$  
  &emsp; &emsp; $θ = \Psi w + \sigma, \tag{19}$   
  &emsp; &emsp; 여기서, $e = [e_1, e_2, … , e_L]^T, w = [w_1, w_2, …, w_L]^T$ are $L×1$ column vectors,  
  &emsp; &emsp; $h = [h_1, h_2, … , h_M]^T, \, θ = [θ_1, θ_2, … , θ_M]^T$ are $M×1$ column vectors $(M≪L)$,  
  &emsp; &emsp; $η$ and $σ$는 noise (from the environment and body),  
  &emsp; &emsp; $\Psi$는 $M x L$ basis matrix  
  &emsp; $\psi_{m, l} = e^{j \frac{2\pi}{L} ml}$, $m = 1, 2, ... , M$; $l = 1, 2, ... , L$ &emsp; &emsp; &emsp; &emsp; {20}  
  + Compared with FFT, the frequency bins of the reconstructed spectrum by SSR are significantly increased. The spectral power of the respiration harmonics and noise is further suppressed with the introduction of sparse constraint, and the peaks related to RR and HR become dominant.
  + SSR에 의해 reconstructed spectrum의 freq. bin은 FFT와 비교하여 상당히 증가되었다. 희소 제약 조건을 적용하면, 호흡의 하모닉과 노이즈의 스펙트럼 파워는 supress되고 RR과 HR과 관련된 peak가 지배적이 된다.  

### 2) ZA-SEFLMS Algorithm for SSR Based on Adaptive Filter
- adaptive filter는 구조가 simple하고 간섭 관련 성능이 우수하여 널리 이용되고 있음
- 적응 필터의 추정 오류 $\epsilon (k)$는  

  &emsp; [Eq. 21] &emsp; $\epsilon (k) = \rho(k) - v^T (k) \omega(k)$  
  &emsp; &emsp; + $\rho(k)$는 원하는 신호,  
  &emsp; &emsp; + $k$는 시간 요소(또는 객체 요소, instance),  
  &emsp; &emsp; + $\omega(k) = [\omega_0(k), \omega_1(k), ... , \omega_{ ι -1}(k)]^T$,   
  &emsp; &emsp; + $v(k) = [v(k), v(k-1), ... , v(k- ι +1)]^T$는 adaptive filter coefficient vector와 input vector,  
  &emsp; &emsp; + $ ι $는 filter length
  
- $ψ_m=[ψ_{m1},ψ_{m2}, … , ψ_{ML}], m ∈ ${1, 2, … , M}은 적응 필터의 input 벡터($v^T(k)$)에 해당하는 $Ψ$의 row vector이다  
- $h$의 요소 $h_m, m ∈ $ {1, 2, ..., M}은 $ψ_m$은 원하는 신호 $\rho(k)$에 해당한다  
- The vector $e=[e_1, e_2, … ,e_L]^T$은 adaptive filter coefficient vector $ω(k)$에 해당한다   
  + Recursive least square (RLS)는 연속 제곱 오류 시퀀스의 가중 합으로 정의되는 cost function (최근 관심 증가)  

  &emsp; [Eq. 22] &emsp; $ξ_{RLS} (k) = \displaystyle\sum_{u=1} ^k β^{k−u}|η(u)|^2$  
  &emsp; &emsp; + $0 ≤ β < 1$은 forgetting factor(무시할 수 있는 factor),  
  &emsp; &emsp; + $η(u) = h_m − ψ_m e(k)$는 recursion error of SSR,  
  &emsp; &emsp; + $m = mod(u,M) + 1$는 나머지 함수
  
- standard RLS algorithm은 sparse solution을 직접 generate할 수 없다. $\espilon (k)의 $L_1$ 표준 $||esplion(k)||을 사용하여 달성할 수 있는 희소 패널티 함수가 필요하다  
- 최종 cost function은  

  &emsp; [Ep. 23] &emsp; $ξ_{ZA−EFLMS}(k) = \displaystyle\sum_{u = 1} ^k β^{k−u}|η(u)|^2 + γ∥e(k)∥_1$
  &emsp; &emsp; + $γ$ :regularization parameter that aims to counterbalance the gradient correction and sparse constraint.  

- gradient descent recursion of the heartbeat signal spectrum vector는  

  &emsp; [Eq. 24] &emsp; $∇e(k+1) = \large{ \frac{ ∂ξ_{ZA−EFLMS}(k) } { ∂e(k) } } $  
  &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; $= -2 \displaystyle\sum_{u = 1} ^{k} \beta^{k-u} \psi_m (h_m - \psi_m e(k)) + γ sgn(e(k))$  
  &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; $= -2 \displaystyle\sum_{u = 1} ^{k} \beta^{k-u} \psi_m η(u) + γ sgn(e(k))$  

  &emsp; [Eq. 25] &emsp; $e(k + 1) = e(k) + \frac{1}{2} \mu(-∇)$  
  &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; $= e(k) + \mu Θ Λ η(k) - ς sgn(e(k))$  

  &emsp; &emsp; + $Θ : [α_1, α_2, … , α_k]$  
  &emsp; &emsp; + $α_u : [ψ_{m1}, ψ_{m2}, … , ψ_{mL}], u ∈ {1, 2, … , k}$  
  &emsp; &emsp; + $Λ : diag{β^{k−1}, β^{k−2}, …, 1}$  
  &emsp; &emsp; + $η(k) : [η(1), η(2), …, η(k)]^T$  
  &emsp; &emsp; + $μ$ : step size, $ς=γμ$ : zero attraction factor, $sgn(⋅)$ : componentwise sign function  
  &emsp; &emsp; &emsp; -. $sgn(⋅) : A_{m,n} = \frac{k}{|k|}$, if k ≠ 0, or 0, otherwise  

- some noise는 VS 신호감지 성능이 감소되는 불안정한 gradient descent(경사하강법)으로 인해 pulse 감쇠를 일으킬 수 있다. 갑작스런 pulse 간섭을 억제하기 위해 recursion error(재귀오류) $η(k)$를 제한하는 $sgn(⋅)$ 함수 적용
- As a result, the novel recursion updating equation is

  &emsp; [Eq. 30] &emsp; $e(k+1) = e(k) + 12μ(−∇)$  
  &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; $= e(k) + μΘΛsgn(η(k))−ςsgn(e(k))$  

- reconstructed heartbeat spectrum $|e(k)|^2$은 iterative calculation based on (30).
- Similarly, the respiration spectrum $|w(k)|^2$도 얻을 수 있다.

--- 

[^5]: A. Singh, S. U. Rehman, S. Yongchareon and P. H. J. Chong, "Multi-resident non-contact vital sign monitoring using radar: A review", IEEE Sensors J., vol. 21, no. 4, pp. 4061-4084, Nov. 2021.  

[^13]: G. Ramachandran and M. Singh, "Three-dimensional reconstruction of cardiac displacement patterns on the chest wall during the P QRS and T-segments of the ECG by laser speckle inteferometry", Med. Biol. Eng. Comput., vol. 27, no. 5, pp. 525-530, Sep. 1989.

[^14]: T. Zheng, Z. Chen, S. Ding and J. Luo, "Enhancing RF sensing with deep learning: A layered approach", IEEE Commun. Mag., vol. 59, no. 2, pp. 70-76, Feb. 2021. 

[^18]: J. Tu and J. Lin, "Fast acquisition of heart rate in noncontact vital sign Radar measurement using time-window-variation technique", IEEE Trans. Instrum. Meas., vol. 65, no. 1, pp. 112-122, Jan. 2016.

[^19]: M. Alizadeh, G. Shaker, J. C. M. De Almeida, P. P. Morita and S. Safavi-Naeini, "Remote monitoring of human vital signs using mm-Wave FMCW radar", IEEE Access, vol. 7, pp. 54958-54968, 2019.  

[^20]: L. Liu, S. Zhang and W. Xiao, "Noncontact vital signs detection using joint wavelet analysis and autocorrelation computation", Chin. J. Eng., vol. 43, no. 9, pp. 1206-1214, 2021.  

[^21]: K.-K. Shyu, L.-J. Chiu, P.-L. Lee, T.-H. Tung and S.-H. Yang, "Detection of breathing and heart rates in UWB radar sensor data using FVPIEF-based two-layer EEMD", IEEE Sensors J., vol. 19, no. 2, pp. 774-784, Jan. 2019.  

[^22]:  H. Shen et al., "Respiration and heartbeat rates measurement based on autocorrelation using IR-UWB radar", IEEE Trans. Circuits Syst. II Exp. Briefs, vol. 65, no. 10, pp. 1470-1474, Oct. 2018.  

[^23]: M. He, Y. Nian and Y. Gong, "Novel signal processing method for vital sign monitoring using FMCW radar", Biomed. Signal Process. Control, vol. 33, pp. 335-345, Mar. 2017.  

 





