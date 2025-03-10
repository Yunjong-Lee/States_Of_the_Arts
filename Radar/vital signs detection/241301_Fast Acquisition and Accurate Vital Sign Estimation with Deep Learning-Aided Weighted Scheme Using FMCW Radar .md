


# Fast Acquisition and Accurate Vital Sign Estimation with Deep Learning-Aided Weighted Scheme Using FMCW Radar   

## 3-1. type of Radar:
- IR-UWB : radiates multiple impulses to achieve high detection resolution, but with higher power consumption.
-  CW : employs a single modulated wave to measure phase variations under low-cost HW.
- FMCW : integrates the advantages of IR-UWB radar and CW radar by achieving a balance between power and performance

## 3-2. process of detecting vital sign:
- range estimation followed by phase extraction (범위 추정 및 위상 추출)
  + [8] 스펙트럼의 크기를 분석하여 목표 범위 추정 [^1]  
  + [9] 범위 추정을 위한 위성성분 고려 [^2]  
  + [10] 크기와 위상을 모두 고려하는 알고리즘 [^3]
    * vital sign을 측정하는데 10sec 이상의 time 필요...long response time
    * range와 displacement는 목표의 다중반사 표면에 의해 넓은 범위에서 디스플레이 된다[11] [^4]
    * 스펙트럼의 공간적 특성을 고려한 딥 러닝 기반 접근 방식 제안.


## 3-3.  system model
- radar receives reflected waves and produces an IF signal by mixing. Next each IF signal is digitized into M samples with the sampling perid(T_f), and the m-th sampled signal of the n-th IF signal b_n,m is 

- $b_{n,m}=e^{ j (2\pi \frac{2W(R+x_i)} {cT_c} mT_f + \frac{4} {\lambda} (R+x_n) ) }$
where, W is the signal bandwidth, R is the range from the sensor to the target, and $x_n$ represents the displacement caused
by breathing and the heartbeat. c is the speed of light and $\lambda$ is the signal wavelength

---

# References

[^1]: [8] J.-M. Mu˜noz-Ferreras, J. Wang, Z. Peng, C. Li, and R. G´omez-Garc´ıa, “Fmcw-radar-based vital-sign monitoring of multiple patients,” in 2019 IEEE MTT-S Int. Microw. Biomed. Conf. (IMBioC), vol. 1. IEEE, May 2019, pp. 1–3.  
[^2]: [9] M. Alizadeh, G. Shaker, J. C. M. D. Almeida, P. P. Morita, and S. Safavi-Naeini, “Remote monitoring of human vital signs using mmwave FMCW radar,” IEEE Access, vol. 7, pp. 54 958–54 968, 2019.  
[^3]: [10] H.-I. Choi, H. Song, and H.-C. Shin, “Target range selection of FMCW radar for accurate vital information extraction,” IEEE Access, vol. 9, pp. 1261–1270, 2021.  
[^4]: [11] E. Antide, M. Zarudniev, O. Michel, and M. Pelissier, “Comparative study of radar architectures for human vital signs measurement,” in 2020 IEEE Radar Conf. (RadarConf20), 2020, pp. 1–6.


