---
date: 2026-03-07 05:49:52
layout: post
---

# [Selecting Target Range with Accurate Vital Sign Using Spatial Phase Coherency of FMCW Radar](https://www.mdpi.com/2076-3417/11/10/4514)


### 2.2. Vital-Sign measurement  
- ooo  

    ![Figure 1. Vital-Sign measurement with FMCW radar](https://mdpi-res.com/applsci/applsci-11-04514/article_deploy/html/images/applsci-11-04514-g001-550.jpg)

- Figure 2 shows VS signals measured by FMCW radar.  
- $𝑀⁡(𝑡,𝑟)$ and $𝑃⁡(𝑡,𝑟)$ for respiration and heartbeat
  + radar의 range resolution이 높기때문에 신체의 다양한 부분의 변위는 다른 range-bins들에 반영된다.
  + VS 변위가 존재하는 range-bin을 식별하기 위해 $𝑃⁡(𝑡,𝑟)$ 사이의 temporal correlation coefficient를 Figure 2(c), (d)와 같이 계산된다.  
    * 호흡은 흉부나 복부
    * heartbeat은 목과 같은 얇은 스킨
  + $𝑃⁡(𝑡,𝑟)$ 사이의 correlation과 reference resporation 신호는 0.5 ~ 0.6m 사이(복부)에서 높게 나타남.
  + $𝑃⁡(𝑡,𝑟)$ 사이의 correlation과 reference heartbeat 신호는 0.75 ~ 0.85m 사이(목 주변)에서 높게 나타남
  + respiration과 heartbeat 신호는 $𝑀⁡(𝑡,𝑟)$보다 $𝑃⁡(𝑡,𝑟)$의 여러 range-bin에서 더 정확하기 관측된다.
  
- the extracted VSs (respiration and the heartbeat) from various range bins corresponding to high and low correlation with referenced signals:
  + $𝑃⁡(𝑡,𝑟 = 0.525,0.550) m$ (Fig. 2e) is highly correlated with referenced respiration, but 𝑀⁡(𝑡,𝑟 =0.525,0.550) m is not.  
  + $𝑃⁡(𝑡,𝑟 =0.775,0.800) m$ (Fig. 2f) shows a high correlation with a referenced heartbeat; however, 𝑀⁡(𝑡,𝑟 =0.775,0.800) m does not.  
  + At 𝑟 =0.800 m in Figure 2e and 𝑟 =1.050 m in Figure 2f, 𝑀⁡(𝑡,𝑟) nor 𝑃⁡(𝑡,𝑟) are associated with referenced VSs.  

    ![Figure 2. Measured vital-sign signals](https://mdpi-res.com/applsci/applsci-11-04514/article_deploy/html/images/applsci-11-04514-g002-550.jpg)


### 2.3. Spectial Phase Coherency  
- VS의 변위를 포함하고있는 range bin 선택  
  : 다양한 range bin $P(t,r)$에서 VS의 변위가 관찰되므로 range bin $P(t,r)$에서 coherency가 높아야 한다.
- coherency 정량화  
  : $SPC(t,r, 𝑟^′) = \frac{\displaystyle \sum ^{t} _{n=t-t_0} 𝑃⁡(𝑠,𝑟) · 𝑃⁡(𝑠,𝑟′)}{\large {\delta_P(r)} · {\delta_P (𝑟′)} }$, for $𝑟≠𝑟′$  

  여기서, $t$ 동안 $𝑃⁡(𝑠,𝑟)$의 평균은 사전에 소거되고, $𝑃⁡(𝑠,𝑟)$는 $𝑃⁡(𝑠,𝑟)$의 표준편차이다.  
  + 가장 높은 SPC 값을 가지는 range-bin 쌍은 VS target range $r_T(t)$로 선택된다.  
    : $r_T(t) = arg \displaystyle\max_{ (𝑟,𝑟^′) } SPC(t,r,r^′)$

### 3.2 Process
- continuous variation을 재구성하기 위해 $𝑃⁡(𝑠,𝑟)$에 phase unwrapping 적용
- time complexity를 줄이기 위해 human target의 boundary를 $M(t,r)$의 variance를 참조하여 set (=suppresses stationary clutter)
- $P(t,r)$ signal filtering:  
  + respiration : 0.1~0.4 Hz
  + heartbeat : 0.8~1.7 Hz
- 각각의 range-bin 쌍에 대해 SPC 계산하고 $𝑟_𝑇⁡(𝑡)$ 선택한 다음, 선택된 range-bin의 $P(t,r)$의 평균 계산하고 zero-crossing detection을 이용하여 vital rate를 계산

- 기존 방법과의 비교
  + conventional method <sup>[37](#note)</sup> : $𝑟_𝑇⁡(𝑡) = arg \displaystyle \max_r \frac{\displaystyle \sum ^𝑡 _{𝑠=𝑡−𝑡_0} 𝑀⁡(𝑠,𝑟) · 𝑃⁡(𝑠,𝑟)} { \sigma_{𝑀⁡(𝑟)} · \sigma_{𝑃⁡(𝑟)} }$  

    여기서, $\sigma_{𝑀⁡(𝑟)}$은 $𝑀⁡(t,𝑟)$의 standard deviation    


   



--- 

# [Target Range Selection of FMCW Radar for Accurate Vital Information Extraction](https://ieeexplore.ieee.org/document/9285301)




---

# References


<a name="note">[37]</a> [Choi, H.I.; Song, H.; Shin, H.C. Target range selection of FMCW radar for accurate vital information extraction. IEEE Access 2020.](https://ieeexplore.ieee.org/abstract/document/9285301)



