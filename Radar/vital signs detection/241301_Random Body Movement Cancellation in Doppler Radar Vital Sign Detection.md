


# Random Body Movement Cancellation in Doppler Radar Vital Sign Detection
- [IEEE TRANSACTIONS ON MICROWAVE THEORY AND TECHNIQUES, VOL. 56, NO. 12, DECEMBER 2008](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=4682605)

## 4-1. Abstract  
+ quadrature Doppler Radar에서 Random Body 움직임 제거를 위한 Complex Signal Demodulation과 Arctangent Demodulation 연구  
+ Target Apps : sleep apnea monitor, lie detector, and baby monitor
+ BB signal의 DC offset이 calibration된다면, 두 demodulation tech으로 body movement cancellation 가능  
+ complex signal demodulation은 dc offset에 영향을 덜 받음, arctangent demodulation은 고조파 및 상호 변조 간섭 제거(at high carrier frequency)
+ dc offset을 정확하게 calibration하지 못하면 complex signal demodulation이 유리.
+ ray tracing model을 이용하여 

## 4-2. COMPLEX SIGNAL DEMODULATION AND ARCTANGENT DEMODULATION  
+ movement에 의한 random frequency drift(경향)를 제거하려면, front/back 양쪽에서 detection을 수행해야 한다.
+  no random body movement is present, the normalized detected baseband signal in one of the baseband I/Q channels
