---
date: 2025-01-02 17:05:17
layout: post
---





## Fourier Series  
- 반복되는 신호의 주기는  

  $$a_n - ib_n = \frac{1}{p} \displaystyle \int _{-\frac{P}{2}} ^{\frac{P}{2}} x(t) \cdot \Large {
      e^{ -i 2 \pi \frac{n}{P} t } 
      } \cdot dt $$  
  + 신호를 구성하는 사인파의 주파수는 모두 신호의 주기 P의 정수 배수 n  
  + $n = −∞…, −3, −2, −1, 0, +1, +2, +3, …, +∞$  
  + 적분의 한계는 신호 주기의 -1/2에서 +1/2까지  

## Fourier Transform
- 반복되지 않는 신호의 주기는 무한하다
- 반복되지 않는 신호를 구성하는 코사인파와 사인파의 계수를 계산하려면 적분의 한계를 −∞에서 +∞로 확장  

  $$X(f) = \int_{−∞} ^{∞} x(t) \cdot e^{-i 2\pi f t} \cdot dt$$

## Fourier Series와 Fourier Transform 비교  
- 푸리에 급수의 이산 주파수 항, n/P는 푸리에 변환에서 연속 항, f로 대체 : 신호의 주기와 무관함을 의미  
- 신호의 주기가 무한하기 때문에 적분의 한계가 시간 전체를 포함하도록 확장  
  ※ 푸리에 변환은 소리와 같은 랜덤 신호에는 구현할 수 없다(모든 무한을 제거하는 더 이산적인 방법 필요)  
  + DFT는 푸리에 변환의 이산 버전  
    : 이산의 뜻 : DFT 입력 신호와 생성되는 주파수 스펙트럼이 특정 이산 지점에서만 정의되고 다른 모든 지점에서는 정의되지 않는다.  
    : DFT가 모든 단일 주파수에 대해 계산하지 않으며 유한한 주파수 분해능을 갖는다(무한히 가까운 주파수를 처리할 수 없다)    

- DFT, FFT 구현에서는 푸리에 변환에 존재하는 무한대를 제거해야 한다.  
  ※ 빙법: 모서리를 잘라낸다.  

## Spectral Leakage  
- 주파수가 1개만 존재하므로 주파수 스펙트럼은 아래에 표시된 것처럼 3Hz에서 단일 선  

  ![시간 영역의 3Hz 코사인파](https://media.licdn.com/dms/image/v2/D4D12AQETAE8y2A0qJA/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715021888895?e=2147483647&v=beta&t=gwx0trNAAbhzxXTY5hzRYPqUEOzcJRnKZDmf9UVm_Tg)  

  ![](https://media.licdn.com/dms/image/v2/D4D12AQE7K94SU8eU8A/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715021937733?e=2147483647&v=beta&t=xJ_CNzpooz3NaSoo5mLJc8HzNJ_94JpKqOFDitMvqqk)  

- 주파수를 3.05Hz로 높이게 되면 
  + FFT windwow 내에서 전체 cycle이 완료되지 않는다(주파수 스펙트럼의 불연속성 발생). 이로 인해 에너지가 주 주파수에서 모든 측면 주파수로 누출  

  ![](https://media.licdn.com/dms/image/v2/D4D12AQH5YuI2ZGSVdA/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715022009176?e=2147483647&v=beta&t=fVXlHCw_ymBB-RZ1VhuTpFCwpFlrRZ4pRJSPzyGfauw)  

  ![](https://media.licdn.com/dms/image/v2/D4D12AQHw53Sx2vb_aw/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1715022057176?e=2147483647&v=beta&t=D3V9frmwu3ofYHJ1n9g65fS0TsYTtVEfK9MDtQzvIsg)  

- Spectral Leakage 억제를 위한 방법으로 window function 적용  


## [윈도잉 함수](https://github.com/Yunjong-Lee/Radar/blob/master/Algorithms/230102_Window%20Function.md)  



















