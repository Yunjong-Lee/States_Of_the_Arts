---
date: 2024-02-13 10:07:20
layout: post
---

# 차량용 레이더 간섭신호에 대한 영향성 연구
- [2019 한국자동차공학회 추계학술대회](https://webcache.googleusercontent.com/search?q=cache:8b7MFV-UdF4J:https://ettrends.etri.re.kr/ettrends/79/0905000399/18-1_033_041.pdf+&cd=7&hl=ko&ct=clnk&gl=kr)  

##### [ Keyword ] Radar, 상호간섭

- 상호간섭 신호  
  + 정의 : 다른 차량에 장착된 레이더에서의 송신 신호가 자가 차량의 레이더에 수신되어 실제 표적 검출을 방해하는 신호  
  + 제거 : Constant False Alarm Rate 레벨 조정  
  
- 모델  
  + 간섭 신호 모델링 : 간섭신호의 영향으로 doppler bin과 range bin에서 평균 잡음 레벨보다 큰 신호를 표적으로 검출될 수 있음  
    + 간섭신호의 주파수 대역폭(BW)은 다르고 동일한 시간 주기(PRI)를 가지는 경우
      : 1D FFT의 잡음 레벨이 일정하게 올라가며 2D FFT에서 여러 doppler bin에서 range bin에 대해 검출됨  
    + 간섭신호의 BW은 같고 PRI가 다를 경우
      : 간섭신호는 주파수 대역에서 넓게 퍼지는 현상이 발생(1D FFT의 잡음 레벨을 일정하게 높임)  
      : CFAR 알고리즘의 문턱값을 (증가한 잡음 레벨만큼) 올리면 간섭 영향 없이 실제 표적 구분 가능  
 
- 용어
  + 도플러 주파수 : 해당 물체의 움직임을 추정할 때 활용되는 값  
  + doppler bin  
  + range bin  
  + CFAR : 수신신호의 잡음 레벨을 계산하여 잡음, 클러터, 간섭 등의 영향에 대응하여 표적을 감지하는 역할  

---
