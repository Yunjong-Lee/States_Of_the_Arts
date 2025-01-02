---
date: 2025-01-02 17:05:17
layout: post
---





## Fourier Series  
- 반복되는 신호의 주기는  

  $$a_n - ib_n = \frac{1}{p} \displaystyle \int _{-\frac{P}{2}} ^{\frac{P}{2}} x(t) \cdot e^{- i 2 \pi \frac{n}{P} t} \cdot dt $$  
  + 신호를 구성하는 사인파의 주파수는 모두 신호의 주기 P의 정수 배수 n  
  + $n = −∞…, −3, −2, −1, 0, +1, +2, +3, …, +∞$  
  + 적분의 한계는 신호 주기의 -1/2에서 +1/2까지  

## Fourier Transform
- 반복되지 않는 신호의 주기는 무한하다
- 반복되지 않는 신호를 구성하는 코사인파와 사인파의 계수를 계산하려면 적분의 한계를 −∞에서 +∞로 확장  

  $$X(f) = \int_{−∞} ^{∞} x(t) \cdot e^{-i 2\pi f t} \cdot dt$$

## Fourier Series와 Fourier Transform 비교  
- 푸리에 급수의 이산 주파수 항, n/P는 푸리에 변환에서 연속 항, f로 대체 : 신호의 주기와 무관함을 의미  
- 신호의 주기가 이제 무한하기 때문에 적분의 한계가 시간 전체를 포함하도록 확장
- 푸리에 변환은 소리와 같은 랜덤 신호에는 구현할 수 없다. 모든 무한을 제거하는 더 이산적인 방법이 필요
  + DFT는 푸리에 변환의 이산 버전  
    : 이산은 DFT로 들어가는 신호와 생성되는 주파수 스펙트럼이 특정 이산 지점에서만 정의되고 다른 모든 지점에서는 정의되지 않는다.  
    : DFT가 모든 단일 주파수에 대해 계산하지 않는다는 것을 의미하며, 유한한 주파수 분해능을 갖는다.  
      (무한히 가까운 주파수를 처리할 수 없다)    

- DFT, FFT의 실제 구현에서는 푸리에 변환에 존재하는 무한대를 제거(빙법: 모서리를 잘라낸다)해야 한다.  

## Spectral Leakage  
- 주파수가 1개만 존재하므로 주파수 스펙트럼은 아래에 표시된 것처럼 3Hz에서 단일 선  

  ![시간 영역의 3Hz 코사인파](https://media.licdn.com/dms/image/v2/D4D12AQETAE8y2A0qJA/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715021888895?e=2147483647&v=beta&t=gwx0trNAAbhzxXTY5hzRYPqUEOzcJRnKZDmf9UVm_Tg)  

  ![](https://media.licdn.com/dms/image/v2/D4D12AQE7K94SU8eU8A/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715021937733?e=2147483647&v=beta&t=xJ_CNzpooz3NaSoo5mLJc8HzNJ_94JpKqOFDitMvqqk)  

- 주파수를 3.05Hz로 높이게 되면 FFT windwow 내ㅐ에서 전체 cycle이 완료되지 않으며, 이로 인해 주파수 스펙트럼은 불연속성으로 인해 에너지가 주 주파수에서 모든 측면 주파수로 누출  

  ![](https://media.licdn.com/dms/image/v2/D4D12AQH5YuI2ZGSVdA/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715022009176?e=2147483647&v=beta&t=fVXlHCw_ymBB-RZ1VhuTpFCwpFlrRZ4pRJSPzyGfauw)  

  ![](https://media.licdn.com/dms/image/v2/D4D12AQHw53Sx2vb_aw/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715022057176?e=2147483647&v=beta&t=D3V9frmwu3ofYHJ1n9g65fS0TsYTtVEfK9MDtQzvIsg)  

## Spectral Leakage 억제를 위해 window function 적용
### hanning window  
- 윈도우 가장자리 신호를 테이퍼링하여 불연속성을 제거

  ![](https://media.licdn.com/dms/image/v2/D4D12AQHXXH43GLo5zA/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715022120263?e=2147483647&v=beta&t=7n1HQ2QuJBDo8F7S5e5eA56oIQxT0SJehwfCPTgDuiU)  

  ![](https://media.licdn.com/dms/image/v2/D4D12AQGrBCxvBMpbtw/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715022183444?e=2147483647&v=beta&t=QCRpjO4QUr0JLmzluls-1U3f0mBCNiKvp7IHnO1xeVE)  

- 전체 에너지는 여전히 여러 주파수에 분산되어 있음
  + 윈도잉 함수는 신호의 모양을 단일 코사인이 아닌 여러 코사인파의 모음으로 변형시켰다.  

- Hanning 윈도우를 적용하면, 윈도우 가장자리에서 3Hz 코사인파를 취소하기 위해 주 주파수의 양쪽에 2개의 추가 주파수가 튀어나왔고, 주 3Hz 주파수는 에너지의 일부가 손실된다(주파수 스미어링). 주 주파수의 진폭은 1보다 적고, 두 개의 측면 주파수로 스미어링된다.

## 윈도잉 함수 목록  

### 1. 직사각형 윈도우  
- 창의 전체 길이보다 몇 샘플이 짧게 정의(프레임의 가장자리에서 신호가 0이 되어 스펙트럼 누출이 줄어들지만, 누출량은 많지 않다)  

  $$w(n) = 1$$  

  ![3.05Hz 신호에 적용된 단축된 직사각형 창](https://media.licdn.com/dms/image/v2/D4D12AQEzBlG7daLAPg/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715060438982?e=2147483647&v=beta&t=xmYP0lsDziypfMqMkfY21mOtUTOhF6LKEVSuOoVGDcs)  
  ![](https://media.licdn.com/dms/image/v2/D4D12AQFEzKE0Ho6r8A/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715060501386?e=2147483647&v=beta&t=AKYVBTHZEHTw54NO-IUNSd6KNnuIqeOaRAcK3y7gmcw)  

### 2. 바틀릿 윈도우  
- 각형 모양의 창으로, 신호를 0에서 창 중앙의 크레센도까지 선형적으로 페이드 인하고, 동일한 선형 방식으로 신호를 0으로 페이드 아웃
  
  $$w(n) = \frac{2}{N-1} (\frac{N-1}{2} - |n - \frac{N-1}{2}|)$$

  ![](https://media.licdn.com/dms/image/v2/D4D12AQE1aznC8Ul0Iw/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715060795060?e=2147483647&v=beta&t=nzC-QzkJirBm2AvF6ERll8J2H7kfky45CH_gpeNNP2g)  

  ![](https://media.licdn.com/dms/image/v2/D4D12AQEcf35KMrLOrA/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715060845342?e=2147483647&v=beta&t=ysEeVqBWduS01iq4kx2IlOSfALVD6se7M7FDFrfFi6w)  

- 용도
  + 잡음이 많은 환경에서 신호 분석  
  + 무선 주파수(RF) 통신  
  + EEG(뇌파) 또는 ECG(심전도) 추출 : 생물전기 신호 분석 시 원치 않는 간섭 주파수(근육 활동이나 전력선 노이즈로 인한 간섭 주파수)를 수집하여 side lobe 억제  
  + 기계의 진동 분석  
  + 사이드로브 억제에 뛰어나지만, Hanning이나 Hamming 윈도우와 같은 다른 윈도우에 비해 메인로브가 더 넓다("노이즈" 주파수가 원하는 신호와 주파수가 매우 가까운 경우 성능 감소)  
### 3. 해닝 윈도우  
- 누설 감소와 주파수 스미어링 사이의 실용적인 타협안을 제공  

  $$w(n) = 0.5 - 0.5 cos(\frac{2 \pi n}{N-1})$$  

  ![3.05Hz 신호에 적용된 Hanning 창](https://media.licdn.com/dms/image/v2/D4D12AQEGzdgF3MHM4g/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715061197011?e=2147483647&v=beta&t=l5Lq5GkvaPV2QhDIJv5MWtAVFWl2QV7wg_LV4AF0gKI)  
  ![](https://media.licdn.com/dms/image/v2/D4D12AQGdlbhSfH8hTA/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715061217216?e=2147483647&v=beta&t=jYEw1zKASttWI6WQn5Wkzq-FMS7pqPhZnSijyKWH1jo)  

### 4. 해밍 윈도우  
- 해닝 윈도우와 모양과 이름이 비슷하지만 윈도우 가장자리에 약간의 신호를 남겨둔다는 차이점  
  + 약간의 불연속성이 남지만 역 해밍 윈도우를 사용하여 원래 신호를 복구할 수 있다  

  $$w(n) = 0.54 - 0.46 cos(\frac{2 \pi n}{N-1})$$  

  ![3.05Hz 신호에 적용된 해밍 윈도우](https://media.licdn.com/dms/image/v2/D4D12AQHgeaSPFX-XdQ/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715061526912?e=2147483647&v=beta&t=SBDlWJHaNYT9bzGJYoWtajk5ZuVv8BhXuiT2OnZ2GT0)  





















