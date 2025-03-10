# Design of ECG Measurement System based on the Android]

- 심전도 신호로부터 깨끗한 ECG 신호를 얻어내기 위해 filter 구현 필요
  - 3단계 노이즈 제거 필터(전원 노이즈 제거를 위한 Band Rejection Filter, noise 제거를 위한 Low pass filter, DC 성분의 노이즈 필터링을 위하여 High pass Filter) 적용
