---
date: 2024-12-30 10:13:02
layout: post
---


# 1. Principle of FFT Algorithm
- Cooley-Tukey Fast Fourier Transform, 1965.
- FFT의 efficiency
  + signal을 $2^x$에 해당하는 횟수만큼 sampling하면 계산이 반복됨.  
  + 계산 결과를 기억하면, 동일한 계산을 반복할 필요가 없음
  + sample이 특정 방식(certain way)으로 정렬(order)된다면, 계산 결과가 next의 시작 point를 형성할 수 있다.  

## Repeating Calculations
### &emsp; Understanding DFT Equation
  
  &ensp; $X_k = \displaystyle \sum_{n=0} ^{N-1} x_n[cos(2\pi k \frac{n}{N}) - i \cdot sin(2\pi k \frac{n}{N}) ]$  

  &ensp; 1. each sample (xₙ)을 주파수 k인 cosine wave의 해당 sample과 곱한 뒤에, 모든 결과를 더한다.  
  &ensp; &ensp; → 결과는 주파수 k = 0에서 코사인 wave의 amplitude.  
  &ensp; 2. 각각의 sample (xₙ)을 주파수 k인 역 sine wave의 해당 sample과 곱한 뒤에, 결과를 모두 더한다.  
  &ensp; &ensp; → 결과는 주파수 k = 0에서 사인 성분의 amplitude.  
  &ensp; 3. 신호의 sample 수 ($N-1$) 까지 반복   
  ※ complex number lists를 얻게되는데, 실수 부분은 각 주파수에서 코사인 성분의 진폭을, 허수 부분은 각 주파수에서 사인 성분의 진폭을 나타냄  

  ![Fig 1. signal has been sampled 8 times](https://media.licdn.com/dms/image/v2/D4E12AQEw1vplOrZZNg/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1664705823541?e=2147483647&v=beta&t=9HO137yk1UK_INswl_4jh1mlGJEn4zF9WfDn5IIySkQ)  

  -. 각각의 sample들은 점으로 표현($x_0, ... , x_7$).  
  -. DFT는 각각 8개의 다른 주파수애서 signal과 cosine과 sine wave를 곱한 뒤에, 각각의 주파수에 대해 곱셈의 결과를 모두 더한다.  
  -. cosine wave와 sine wave sample이 2의 거듭제곱의 배수면, wave의 주파수가 증가되도 특정한 sample 조합의 amplitude는 각각의 다른 주파수에 대해 일정하다.  
    ※ 이 지점에서 cosine과 sine wave를 신호와 곱하면 주파수가 변경되어도, 같은 결과가 나온다. 

### &emsp; Repeating amplitudes on a Wave
#### &emsp; &emsp; cosine wave
- 그래프에서, cosine wave가 2Hz씩 증가하지만, 샘플의 amplitude는 변화없다.
- if, $x_0$ 또는 $x_4$ 신호에 코사인 wave의 해당 포인트를 곱하면 결과는 항상 동일할 것이다.

![](https://media.licdn.com/dms/image/v2/D4E12AQESyVg_MGcRCg/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1664706877428?e=2147483647&v=beta&t=6l5ELHuhFf3-_5mGPShFGjwpA_1lPt7FuZxOi6CSqEE)

![](https://media.licdn.com/dms/image/v2/D4E12AQFHsB2uqIO_Nw/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1664706895932?e=2147483647&v=beta&t=B7SG3x2uYMR7zsnfeeMkuegnyCgzFoYzZN_NyLyVKRw)

![](https://media.licdn.com/dms/image/v2/D4E12AQGEcVlVdqJNcA/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1664706906502?e=2147483647&v=beta&t=1Z7Nps9rc4DgHaY9bXuuRjFEBU4fy-5q94qoj0bL-6s)

![Fig 2. 샘플 0과 4를 표시한 cosine wave ($x_0$와 $x_4$로 대응됨)](https://media.licdn.com/dms/image/v2/D4E12AQEun1OfI1twPA/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1664706922302?e=2147483647&v=beta&t=qklBcSbtLQA4JMaLcewkO5m2CqrsLzu1TGGJYPJMp7E)  

#### &emsp; &emsp; sine wave  
- 신호의 이들 포인트에 sine wave를 곱한 결과도 동일하다.  

![](https://media.licdn.com/dms/image/v2/D4E12AQE9JJXFvaAo7Q/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1664707119718?e=2147483647&v=beta&t=jucedNlu9BwbwWbAuVOYHUsgvbe1-KveUdMChtkFWnQ)  
![](https://media.licdn.com/dms/image/v2/D4E12AQFi5_BtZqcJ-w/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1664707129377?e=2147483647&v=beta&t=Tu2mqWmBnH1ff4BLXSLbaYtpCupFzn703DfhU2F8Wk0)  
![](https://media.licdn.com/dms/image/v2/D4E12AQEi82AwuUdwVw/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1664707138253?e=2147483647&v=beta&t=RTTHr8a4VTUJclBFDzGXKTVM6SUU-ExxqVVcflp2pf8)  
![Fig 3. ](https://media.licdn.com/dms/image/v2/D4E12AQGhLGYQsVBOJg/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1664707146565?e=2147483647&v=beta&t=Z5sJ4wNg24wfAbbSrWaKhjIHMuZktI3xE0OEHxj9koQ)  


#### &emsp; &emsp; Different combinations of samples also repeat  
- 진폭의 반복 현상은 다른 샘플조합도 같음(차이점: 동일한 진폭가 반복되는 주파수의 수).

### &emsp; &emsp; Result  
- 한 주파수에서 sample 곱셈 결과를 기억한다면, 다른 주파수에서 다실 발생할 때 동일한 계산을 반복할 필요가 없음
- 곱셈이 반복되는 주파수에 따라 sample sorting

## Divide-and-Conquer  
- FFT가 반복 계산의 이점을 활용하려면, 분할 정복 알고리듬 적용
  + 샘플을 곱셈이 반복되는 빈도에 따라 그룹으로 분할 (샘플 배열을 더 작은 그룹으로 분할하여 각 그룹에 샘플 쌍 생성)
  + 각 샘플 쌍에 간단한 2-point DFT(2개 샘플에 수행된 DFT) 수행
  + 2-point 결과를 재귀적으로 결합하여 문제 해결
  + 각 새 그룹에 2-point DFT 반복 (전체 샘플 배열의 DFT가 계산 완료 시점까지 진행)

### &emsp; &emsp; Divide-and-Conquer Concept  
- 문제를 동일하거나 관련된 유형의 두 개 이상의 하위 문제로 재귀적으로 분해하여 이들이 직접 해결할 수 있을 만큼 간단해질 때까지 분해  
- 하위 문제에 대한 솔루션을 결합하여 원래 문제에 대한 솔루션 제공   

### &emsp; &emsp; Sort Algorithm  
- 예 : 8개의 난수 배열을 오름차순으로 정렬  
  28 6 73 96 63 71 59 62  

  + 병합 정렬 
    - 분할 단계 : 문제를 작은 하위 문제로 세분화
    - 정복 단계 : 정렬 진행(하위 문제가 정렬되면, 결과적으로 점점 더 큰 그룹으로 병합되어 전체 문제 해결 가능)  

### &emsp; &emsp; Divide-and-conquer applied to the FFT  
### &emsp; &emsp; Divide Stage  
- 입력 배열의 요소를 점점 더 작은 배열로 반복적으로 세분화(FFT는 각 단계에서 짝수와 홀수 요소를 그룹화)  

  ![Fig 4. ](https://media.licdn.com/dms/image/v2/D4E12AQFy7B5f5Gygmw/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1665050182466?e=2147483647&v=beta&t=AV42hoET1sjs3fV17hYBwJlYeXG-ntR8-tL10XmYxbE)  

- $x_0, ..., x_7$까지 label이 지정된 8 samples의 amplitude는  
  | x₀   | x₁   | x₂   | x₃    | x₄    | x₅   | x₆   | x₇    |
  | ---  | ---  | ---  | ---   | ---   | ---  |---   | ---   |
  | even | Odd  | even | Odd   | even  | Odd  | even | Odd   |
  | 0.46 | 0.72 | -0.3 | -0.09 | -0.16 | -0.2 | 0.0  | -0.43 |

- 짝수 샘플( x₀ , x₂ , x₄, x₆)과 홀수 샘플(x₁ , x₃ , x₅, x₇)로 분리   
  | x₀   | x₄    | x₂   | x₆  | x₁   | x₅   | x₃    | x₇    |
  | ---  | ---   | ---  | --- | ---  | ---  | ---   | ---   |
  | even |       |      |     | Odd  |      |       |       |
  | 0.46 | -0.16 | -0.3 | 0.0 | 0.72 | -0.2 | -0.09 | -0.43 |

### &emsp; &emsp; Conquer Stage  
- DFT 검증  
    &ensp; $X_k = \displaystyle \sum_{n=0} ^{N-1} x_n[cos(2\pi k \frac{n}{N}) - i \cdot sin(2\pi k \frac{n}{N}) ]$  
    -. $x_n$ : signal, $n$은 sample index
  + 각 샘플은 코사인파와 역 사인파에서 해당 샘플과 곱해져야 한다.  
    (sine wave는 방정식에서 코사인 항과 사인 항 사이의 마이너스 부호때문에 반전된다)  

    ![Fig 5. k = 0(위) 및 k = 1(아래)](https://media.licdn.com/dms/image/v2/D4E12AQEZ2b8gAmh6jA/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1665257121741?e=2147483647&v=beta&t=CGKBxhShHJfTb4VfAb9NjWgYpf1n6U0d3g8ON-CXnDc)  

    -. 각 그룹에는 샘플이 2개만 있으므로 N=2,  
    -. 첫 번째 그룹: sample x₀ & sample x₄ (Fig 5.에서 green point label)  

  + DFT에서 테스트할 주파수 수는 샘플 수와 같으므로, 각각의 그룹의 2개 샘플을 2개 주파수($k = 0, 1$)에서 테스트.  
  + 각 주파수에서 DFT는 신호를 코사인파(Fig 5.의 왼쪽)와 역 사인파(Fig 5.의 오른쪽)로 곱한다  
  + 곱셈연산 완료 후 모든 곱셈의 결과를 더하여 각 주파수에 대한 신호의 DFT를 제공
    * 주파수 k = 0에서 신호의 DFT(X₀)와 k = 1에서 신호의 DFT(X₁) 제공  

### &emsp; &emsp; Calculating the DFT for k=0  
- 첫 번째 주파수 k = 0에 대한 DFT X₀는  
  $X_0 = x_0 \cdot [cos(2 \pi \cdot 0 \cdot \frac{0}{2}) - i \cdot sin(2 \pi \cdot 0 \cdot \frac{0}{2})] + x_4 \cdot [cos(2 \pi \cdot 0 \cdot \frac{1}{2}) - i \cdot sin(2 \pi \cdot 0 \cdot \frac{1}{2})]$  
  -. $k = 0$, index $(n) : 0 ~ 1$  

  $X_0 = x_0 \cdot [cos(0) - i \cdot sin(0)] + x_4 \cdot [cos(0) - i \cdot sin(0)]$

  ![X₀의 경우, sample index n과 무관하게 k = 0에서 cosine의 amplitude = 1 (b), sine의 amplitude = 0 (r)](https://media.licdn.com/dms/image/v2/D4E12AQFp1rasTAPCuw/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1665257234877?e=2147483647&v=beta&t=mZyvp_whhPZy5pdl9V2yalVQt2XZyL7J-qjQGV6AE2E)  

  $X_0 = x_0 + x_4$ ← 이 방정식으로부터 샘플 x₀와 x₄의 진폭을 읽으면 신호에 대한 X₀ 계산 가능.  
  $X_0 = 0.46 + -0.16 = 0.3$  

### &emsp; &emsp; Calculating the DFT for k=1
- 두 번째 주파수 k = 1에 대한 DFT X₁는
  $X_1 = x_0 \cdot [cos(2 \pi \cdot 1 \cdot \frac{0}{2}) - i \cdot sin(2 \pi \cdot 1 \cdot \frac{0}{2})] + x_4 \cdot [cos(2 \pi \cdot 1 \cdot \frac{1}{2}) - i \cdot sin(2 \pi \cdot 1 \cdot \frac{1}{2})]$  
  -. $k = 1$, index $(n) : 0 ~ 1$  

  $X_1 = x_0 \cdot [cos(0) - i \cdot sin(0)] + x_4 \cdot [cos(\pi) - i \cdot sin(\pi)]$  

  ![sample x₀, 코사인파의 진폭: 1(좌), 사인파의 진폭: 0(우)이고 sample x₁, 코사인파의 진폭:-1, 사인파의 진폭: 0](https://media.licdn.com/dms/image/v2/D4E12AQFPs-DWDI8gtQ/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1665257694335?e=2147483647&v=beta&t=qtRo5jf_D2vclIFy-25FwDnrDdXDvw3Agpa216rGhhM)  

  $X_1 = x_0 - x_4$  
  $X_0 = 0.46 - -0.16 = 0.62$  

### &emsp; &emsp; Repeating the process for the other sample groups
- 2-point DFT를 통해 각 단계의 끝에서 각 샘플 그룹에 적용할 수 있음
- 이 과정을 Butterfly Diagram으로 표현할 수 있다

## Linear Butterfly  

### &emsp; &emsp; 




## &emsp; Why do we need Twiddle Factors?  
- 4-포인트 DFT로 4개의 다른 주파수에서 코사인파와 사인파가 신호에 얼마나 기여하는지 계산  
→ 해당 주파수에서 코사인파와 사인파로 신호 테스트 수행.  

  ![Fig 2. 샘플 x₀, x₂, x₄, x₆를 포함하는 첫 번째 그룹의 4-포인트 DFT 신호(Green), </br> 코사인(Blue) 및 사인(Red) 테스트파](https://media.licdn.com/dms/image/v2/D4E12AQGzLuHndtVLxQ/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1666773677725?e=2147483647&v=beta&t=u6smHNlBSUiPu4QqbDtVGqFc_3qmaMdB84ih7lNScIY)

- 주파수 인덱스 k=1에 대한 DFT X는  
  $X_{k=1} = (x_0 - x_4) - (x_2 - x_6) \cdot i$  

  ![Fig 3. 주파수 인덱스 k=1에 대한 DFT에 대한 그래프](https://media.licdn.com/dms/image/v2/D4E12AQFdbnqqusXegA/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1666776361756?e=2147483647&v=beta&t=Tsi3g1Bd3zM-OVFBleDwk-CyulEKGl3ZUllnzp6NSdE)  

  + $(x_0 - x_4)$가 a₄와 같고, $(x_2 - x_6)$가 a₆와 같음(2-point DFT 참조)   

    ![Fig 4. 2-point DFT](https://media.licdn.com/dms/image/v2/D4E12AQFKZhYPu7mAvg/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1666777766036?e=2147483647&v=beta&t=tOogaT0D_tD2XjvUdjKbmOZfubZVumU3_6Zy-jLSxvw)
  
  + 2-point DFT의 결과 $a_4$와 $a_6$를 결합하여 4-point DFT 계산 가능  
    (but, a₄ 와 a₆의 단순 덧셈으로는 4-point DFT를 얻을 수 없음)  

    ![Fig 5. 나비 다이어그램](https://media.licdn.com/dms/image/v2/D4E12AQFWufxaknuwiQ/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1666868023995?e=2147483647&v=beta&t=xEHkjpJFSrgcHrM6p0t-qgOVsk_2JJeTA1SuncRHqTQ)

    - a₄ 와 a₆을 빼고 a₆에 $i$를 곱해야 하지만, a₆를 바로 사용할 수 없다

    ![Fig 6. ](https://media.licdn.com/dms/image/v2/D4E12AQHXLKmv-WyvYQ/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1666869059312?e=2147483647&v=beta&t=4EH5JNI198q3IU-tvyiikieEnS4aCiShkWUC_R10v2E)  

  + $x_2$와 $x_6$의 위치가 2-point DFT의 코사인 샘플 포인트와 align되지 않는다. 이경우 2-point DFT는 어떻게 수행되는가?  

  ![Fig 7. 2-point DFT stage에서 $x_2$와 $x_6$ sample](https://media.licdn.com/dms/image/v2/D4E12AQG_GmTnv7jycg/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1666778426980?e=2147483647&v=beta&t=moK8Rj5RosXF7cEZgdqVQEdE_HLEHELnUl46g1lqDrw)  


  + 2-point DFT의 코사인파에 대한 sample $x_2$와 $x_6$가 sample point와 일치할 때까지 신호가 x축을 따라 이동한 것처럼 동작.  
   
  ![Fig 8. ](https://media.licdn.com/dms/image/v2/D4E12AQGzVAf7rH_Ilg/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1666779536322?e=2147483647&v=beta&t=8PsKRhXrYQFSIPNxAnOjSV5vNSOJoZFlGPPnSHtv5Zo)  
    
  : 단순히 계산을 더 쉽게 하기 위해 신호를 원하는 대로 바꿔가며 돌아다닐 수는 없다. 그러면 나머지 계산에 오류 발생된다. 그러므로, Twiddle Factor가 필요

## &emsp; Twidle Factor란
  : 각각 butterfly는 2개의 output(even output_red와 odd output_blue)을 생산.  
  : 이전 단계의 butterfly의 출력이 현재 stage의 입력  

- 트위들 팩터는 홀수 입력에 곱해지는 복소수 상수
- 짝수 입력에 더하거나 뺀다(이렇게 하면 현재 버터플라이에 대한 새로운 출력 쌍 생성)
  ※ 복소수 연산은 한 번의 곱셈에서 두 가지 연산(진폭 변화 및 위상 변화)의 의미.

- Fig 8.에서, 
  + x₆ : 다이어그램 오른쪽 하단의 2-point butterfly 입력이 되어 Twiddle Factor W₂⁰ 로 곱해진다. 
    - 이 Twiddle Factor는 1과 같으므로 x₆는 변경되지 않는다. 
    - (그 다음 x₂에 더해) a₆를 생성하기 전에 X(-1). 
      * a₆를 생성하기 위해 실제로 진행한 연산은 x₂-x₆ 임  
  + a₆ : 2-point butterfly 홀수 결과아며, 이 값이 4-point butterfly로 입력된다.
    - 4-point butterfly는 두 개의 엇갈린 2-point butterfly 이다.
    - a₆ 에 Twiddle Factor W₄¹을 곱하면, a₆가 스케일 되고 위상이 변경된다. 
      * 위상 변화 : x축을 따라 a₆를 구성하는 샘플을 4점 DFT에 대한 올바른 위치로 이동
      * 스케일링 연산은 a₆ 의 진폭을 스케일링하여 마치 그것을 구성하는 샘플이 사인파의 해당 샘플에 곱해진 것처럼 보이게 했다.  

## &emsp; 2-point butterfly의 홀수 입력에 트위들 계수 W₂⁰을 곱하는 것이 1을 곱하는 것과 같은 이유  

### &emsp; &emsp; 트위들 팩터: W₂⁰
- 아래 첨자 번호는 현재 작업 중인 DFT의 순서로, Fig 9.의 경우, 2-point DFT로 작업하고 있으므로 순서는 2.  
- 위 첨자 번호는 현재 DFT 내의 특정 sample의 index. Twiddle Factor로 곱해지는 것은 홀수 입력뿐이므로, 2-point butterfly에서 index가 0.  

  ![Fig 9. ](https://media.licdn.com/dms/image/v2/D4E12AQGwyMMmR-9pug/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1667222239847?e=2147483647&v=beta&t=Ou7Ibgl21FEGIlB59A9Gl-Ug04Ju8KbFWjol0MhcwhA)  

- 트위들 팩터 계산  
  $W_O ^I = cos(2\pi \cdot \frac{I}{O}) - i \cdot sin(2\pi \cdot \frac{I}{O})$  
  회전 계수 $W_2 ^0$의 경우는  
  $W_2 ^0 = cos(2\pi \cdot \frac{0}{2}) - i \cdot sin(2\pi \cdot \frac{0}{2})$  
  $W_2 ^0 = cos(0) - i \cdot sin(0) = 1 -0i = 1$  

### &emsp; &emsp; 트위들 팩터: W₄¹
- 4-point butterfly의 다이어그램을 살펴보면, a₆에 회전계수 W₄¹을 곱한다
  + 트위들 인자로 곱해지는 것은 홀수(파란색) 입력뿐이므로 4포인트 버터플라이에서 인덱스는 0 ~ 1이며, 이것은 인터리브 버터플라이의 2번째이므로 인덱스는 1.  

  ![Fig 10. ](https://media.licdn.com/dms/image/v2/D4D12AQHJgMoSkkq0Jw/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1666291720408?e=2147483647&v=beta&t=tFllnTVBD_azooMLEUvCTqaZWC-k_XkP1hHOPHvAjiE)  

  $W_4 ^1 = cos(2\pi \cdot \frac{1}{4}) - i \cdot sin(2\pi \cdot \frac{1}{4})$  
  $W_4 ^1 = cos(\frac{\pi}{2}) - i \cdot sin(\frac{\pi}{2}) = -i$

- 따라서, 회전 계수 W₄¹을 곱하면 위상이 이동하고 a₆ 의 진폭이 조정된다.  
  + a₆를 구성하는 샘플 x₂와 x₆는 2-point DFT단계에서 있었던 위치에서 4-point DFT에 필요한 위치인 (x축을 따라) -90°로 이동, a₆의 진폭은 -1로 조정.

  + 수학적 표현  
  $X_{K=1} = a_4 + a_6 X W_4 ^1 = a_4 + a_6 X -i = a_4 -a_6i$  
  &emsp; &emsp; &ensp; $ = (x_0 - x_4) - (x_2 - x_6)i$  
  ※ - i를 곱하는 것은 허수 차원으로 -90°(-𝜋/2 라디안) 회전하는 것(x축을 따라 -90° 위상이 이동하였음을 의미, 이는 a₆에 발생한 일)  
  
  ![Fig 11. ](https://media.licdn.com/dms/image/v2/D4E12AQHsDeGTs01sMQ/article-inline_image-shrink_400_744/article-inline_image-shrink_400_744/0/1666873481742?e=2147483647&v=beta&t=8KGK3Q1buCedlMpKgjbrVstSN6lpePbbclAycD3ZAqA)  

---  
# 2. twidle table
- FFT 알고리즘에서, 데이터에 곱해지는 삼각 상수 계수[^삼각상수계수]
- 이산 퓨리에 변환을 재귀적으로 결합하는데 사용

- FFT Twiddle Factor: $e^{\frac{i2πk}{N}}$  
- IFFT Twiddle Factor: $e^{\frac{−i2πk}{N}}$  

  ![Fig 1. twidle table_나비 다이어그램](https://i.sstatic.net/BkCSR.jpg)

- It contains 256 complex exponentials $e(k)$  
  $e(k) = cos(\frac{2\pi k}{1024})+jsin(\frac{2\pi k}{1024}),$  
  + k=0,...,255  
  + k is the index number of the iteration thus k=0,1...N  

- matlab code  
    table = round(M*exp(1j*2*pi/1024*[0:1*nMax/4-1]'));  
    table = max(min(real(table),2147483647),-2147483647) + 1j* max(min(imag(table),2147483647),-2147483647);  
    여기서, M은, 2147483647.5, Max는 1024이다.

---  
# 3. 결론
- Twidle Factor는 FFT Algorithm이 전체 계산을 2점 DFT의 부하처럼 취급하는 점을 보완한다. 


--- 

[^삼각상수계수]: Cooley–Tukey FFT 알고리즘의 butterfly 연산에서 root-of-unit 복소 곱셈 상수를 말함