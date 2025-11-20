---
date: 2024-12-03 14:04:23
layout: post
---

# Logistic Regression  

## 개요  
- 알번적인 데이터 분석 기법으로 선형회귀 분석과 딥 러닝이 있다.
  + 선형회귀 분석  
    : 선형 조합을 사용하여 종속 변수와 독립 변수 간의 관계를 모델링  
    $y= β_0 X_0 + β_1 X_1 + β_2 X_2 + … β_n X_n + ε \tag{1}$  
    ※ $β, ε$는 회귀 계수  

    | 선형 회귀             | 로지스틱 회귀            |
    | --------------------- | ------------------------ |
    | 주어진 일련의 독립 변수를 사용하여 </br> 연속된 종속 변수의 실제 값 예측 | 분류 알고리즘 (연속 데이터의 실제 값을 예측할 수 없음) |
    |연속 변수는 가격 또는 나이와 같은 값의 범위를 </br> 값으로 가질 수 있다 | |
    | “10년 후 쌀 가격은 어떻게 될까요?”와 같은 질문에 </br> 답 가능 | “10년 안에 쌀 가격이 50% 상승할까요?”와 같은 질문에 답 가능 |

  + 딥러닝
    : 신경망 또는 소프트웨어 구성 요소를 사용하여 정보를 분석하는 기법

    | 딥러닝                 | 로지스틱 회귀             |
    | --------------------- | ------------------------ |
    | 오류에 대한 조사나 수정이 거의 안된다 | 계산이 투명하고 </br> 문제 해결이 쉽다 </br> 계산이 복잡하지 않음 |  

## 정의
- Logistic Regression은 두 데이터 요인 간의 관계를 찾는 데이터 분석 기법으로, 예측 변수에 기반한 이진 반응 변수를 모델링하는데 사용된다  
※ 2개 클래스 또는 이진 반응 문제를 위해 고안되었지만, 다중 클래스 문제로 일반화 가능  

  + 두 개의 값을 갖는 범주형 종속변수를 분류하고 예측하는 것으로 두 개의 클래스에 대한 확률 값이기 때문에 이항 분포[^1]를 따른다. (독립 변수 $X$가 어떤 확률 값을 갖는냐를 찾는 것임.)   
  + 확률 = $P(y=1|X) = p$  
     : 이 확률 값을 구하기 위한 회귀식이 Eq. 1 이다.  
  + 종속 변수의 범위를 $-∞ ~ ∞$까지 변환이 필요하며, 이를 위해서 활용되는 개념이 odds와 logit function 이다.  
    - odds: 성공확률/실패확률을 의미  
    - logit: 오즈에 log함수를 취하는 변환함수  </br>  
    . $0 ≤ P(y=1|X) = p(성공확률) ≤ 1 $  </br>  
    . $0 ≤ Odds = \large { \frac{성공확률}{실패확률} } = \frac{p}{1-p} ≤ ∞ $  </br>  
    . $-∞ ≤ log(Odds) = log(\frac{p}{1-p}) ≤ ∞ $  </br>  

    ※ Odds는 확률 p가 1에 가까워질수록 분모가 0에 가까워지니 무한대로 갈 것이고 여기에 log를 취하면 범위가 [-∞,∞]로 변환된다 ← 종속변수 범위 변환.  </br>  
    . $log(Odds) = log(\frac{p}{1-p}) = β_0 + β_1 x_1 + β_2 x_2 + … β_n x_n$  </br>  
    . 확률 $P(y=1|X) = p = \LARGE{
        \frac   {e^{β_0 + β_1 x_1 + β_2 x_2 + … β_n x_n}}
                {1+e^{β_0 + β_1 x_1 + β_2 x_2 + … β_n x_n}} }$  </br>  

    . 회귀식을 log(odds)를 통해 확률값으로 변환하는 과정을 거쳐 최종적으로 알고싶은 확률값이 구해지게 된다.  

  + 로지스틱 회귀 분석은 수학에서 로지스틱 함수 또는 로짓 함수를 x와 y 사이의 방정식으로 사용하는 통계 모델이다.  
  + 로짓 함수는 sigmoid 함수로 매핑된다.  
    (sigmoid 함수는 독립변수의 값에 관계없이 종속변수의 값으로 0과 1 사이의 값만 리턴한다)

    . $f(x) = \LARGE{   \frac{e^{-x}}{1+e^{-x}}   }$  

    ![ Sigmoid Function Graph ](https://d1.awsstatic.com/S-curve.36de3c694cafe97ef4e391ed26a5cb0b357f6316.png)  

    로지스틱 회귀분석도 종속 변수의 값 추정이 가능하도록 여러 독립 변수와 단일 종속 변수 간의 방정식으로 모델링하게된다.  

  + 여러 독립 변수를 사용한 로지스틱 회귀 분석을 위한 로짓 모델  
    - sigmoid function으로부터 여러 독립 변수를 사용한 로지스틱 회귀 분석을 위한 모델을 아래와 같이 정의할 수 있다  
      : $y = f(β_0 + β_1 x_1 + β_2 x_2 + … β_n x_n)$  
      ※ 종속 변수와 독립 변수의 알려진 값이 있는 충분히 큰 실험 데이터 세트를 로짓 모델에 적용(학습)하면 회귀계수의 값을 구할 수 있다  

    - 로짓 모델로부터 실패 대비 성공비율 또는 로그확률도 구할 수 있음  
      : Logit Function $ = log(\frac{p}{1-p})$  

- ~~관심 있는 통계적 분포에서 관찰된 데이터가 샘플링될 가능성을 최대화하는 통계적 매개변수를 찾으려는 "최대 우도 추정" 문제로 생각할 수 있음 (supervised machine learning algoriithms에서 보던 일반적인 cost/loss function approch와 밀접한 관련이 있다)~~
- ~~$y_i ∼ β_0 + β_1 x_i$과 같은 단순 선형회귀 모델은 0과 1 경계 외부의 값을 쉽게 생성할 수 있기때문에 좋지않은 선택이 될 것이다. 필요한 것은 lower bound를 0으로 upper bound를 1로 예측하는 것임.~~  
- ~~이 random variable은 Bernoulli distribution을 따르기 때문에 이진변수를 예측하는 대신, 문제를 공식화할 수 있다~~  
  + $P_i ∼ β_0 + β_1 x_i$  

- 경계 요구(lower bound=0, upper bound=1로 예측)를 만족하는 모델(Logistic Equation)  
  + $P_i = \LARGE{ \frac{e^{(β_0 + β_1 x_i)}}{1+e^{β_0 + β_1 x_i}} } $  
  + $logit(p_t) = ln(\frac{p_i}{1-P_i}) = β_0 + β_1 x_i $  
    : 모델은 로그 스케일로 값을 생성하고 위의 로지스틱 방정식을 사용하여 0 ~ 1 사이의 값으로 변환  

- ~~train_set에서 최상의 매개변수 추정치는 최대 우도 프레임워크 내에서 통계적 모델이 실제로 관찰된 데이터를 생성할 가능성을 최대화~~  
  + ~~적합을 관찰된 데이터 세트에 대한 확률 분포로 생각할 수 있음~~   
    ~~: 확률 분포의 매개변수는 관찰된 데이터가 해당 분포에서 나왔을 가능성을 최대화해야 한다.~~  
    ~~: 가우시안 분포를 사용하는 경우 관찰된 데이터가 해당 특정 가우시안 분포에서 추출될 가능성이 더 높아질 때까지 평균 및 분산 매개변수를 변경해야한다.~~  
    ~~: 로지스틱 회귀에서 응답 변수는 이항 분포 또는 특수한 베르누이 분포로 모델링된다.~~  
    ~~: 각 응답 변수의 값 $y_i$는 0 또는 1이고~~  

## [Regression Coefficient Estimation](https://m.blog.naver.com/winddori2002/221706766540)  
- 로지스틱 회귀 계수를 추정하기 위해서는 최대우도법(MLE:Maximun Likelihood Estimation)나 Gradient Descent Method 등을 활용할 수 있다    

### Maximun Likelihood Estimation  
- 우도[^2]를 최대로 만드는 것
- 어떤 모수가 주어졌을 때, 원하는 값들이 나올 가능도를 최대로 만드는 모수를 선택하는 방법 
- 표본 x로부터 우리가 알고자 하는 모수(파라미터)를 추정. 즉, $X$가 변수가 아니라 상수로 고정, 파라미터를 변수로 하여 파라미터의 가능성(=우도)을 다음 식으로 나타낼 수 었다.  

  + $L(\theta) = f_x(x|\theta)$  // $\theta$의 parameter를 가지는 분포  
    - $\theta$가 parameter로 $\mu, \sigma$를 가지고 있는 ( $\theta =(\mu, \sigma)$ ) 정규분포라 할때, 한 개의 데이터가 이 정규분포를 따를 확률은  
      . $p(x_n | \theta) = \LARGE{
        \frac{1}{ \sqrt{2\pi \sigma} }exp{-\frac{(x_n - \mu )^2}{2 \sigma^2}}
    } $ // data $x_n$이 $\theta =(\mu, \sigma)$의 파라미터를 가지는 정규분포를 따를 확률
    - 모든 데이터들이 독립적(Indipendent)이라고 가정하면,  
       $$L(\theta) = p(X|\theta) = \displaystyle \prod_{n=1}^{N}p(x_n | \theta) \tag{Eq. 2} $$  
    - Eq. 2가 likelihood 계산식 이다. data $X$가 $\theta$의 parameter를 가지는 분포를 따르려면, 이 likelihood가 최대가 되는 분포를 찾아야 한다.  
      ※ 최대값을 구할때 주로 미분을 사용하지만(곱셈으로 연결된 식의 구조상 미분을 적용하기 쉽지 않음) log와 -를 취해서 최소가 되는 값을 구함으로써 maximum likelihood를 결정한다.  
       $$E(\theta) = -ln L(\theta) = -\displaystyle \sum_{n=1} ^{N}ln p(x_n|\theta) \tag{Eq. 3} $$
    - Eq. 3이 log likelihood 계산식 임.  

- Maximum Likelihood 계산  
  : likelihood를 최대화하는 (log likelihood를 최소화하는) θ 값을 구함(likelihood 식 미분 → 이 식이 0이 되는 값(극소값)을 찾는다)  

  $$\frac{\partial}{\partial \theta} E(\theta) = - \frac{\partial}{\partial \theta} \displaystyle \sum_{n=1} ^{N}ln p(x_n|\theta) = \sum_{n=1} ^{N} \frac{ \frac{\partial}{\partial \theta}p(x_n|\theta) }{ p(x_n|\theta) } \simeq 0 \tag{Eq. 4} $$

  + explain
    - 분포가 $\theta = (\mu, \sigma)$인 정규 분포라면, $p$는  
      $$p(x_n|\mu, \sigma) = \frac{1}{\sqrt{2 \pi \sigma}} e^{- \frac{{||x_n - \mu||^2}}{2 \sigma^2} } \tag {Eq. 5} $$  
      └─ 여기서, $\mu$는 평균, $\sigma$는 분산을 나타낸다.
      
    $$\frac{\partial}{\partial \mu} E(\mu, \sigma) = - \displaystyle \sum_{n=1} ^{N} \frac{ \frac{\partial}{\partial \mu}p(x_n|\mu, \sigma) }{ p(x_n|\mu, \sigma) } = - \displaystyle \sum_{n=1} ^{N} -\frac{2(x_n - \mu)}{2 \sigma^2} $$
    $$ = \frac{1}{\sigma^2} \displaystyle \sum_{N}^{n=1}(x_n - \mu) = \frac{1}{\sigma^2} (\displaystyle \sum_{N}^{n=1} x_n -N_{\mu}) \tag{Eq. 6} $$
      Eq. 6을 0으로 만드는 parameter $\theta = (\mu, \sigma)$를 찾아야 한다.  
        ├─ $\sigma$는 분모이므로 이 값으로 식을 0으로 만들 수 없디.    
        ├─ 그러므로, $\mu$를 Eq. 7과 같이 정의하여 Eq. 6을 0으로 만든다.  
        └─ 또 $\mu$로부터 $\sigma$ (Eq. 8) 를 얻어낼 수 있음  
    $$\hat{\mu} = \frac{1}{N} \displaystyle \sum_{n=1}^{N} x_n \tag {Eq. 7}$$

    $$\hat{\sigma}^2 = \frac{1}{N} \displaystyle \sum_{n=1}^{N} (x_n -\hat{\mu})^2 \tag {Eq. 8} $$  

    ∴ 결과적으로 likelihood를 최대로하는 파라미터 값(평균과 분산 값)을 MLE라고 한다.
      → 하지만, ML은 분산을 실제보다 작게 추정하여 표본에 대하여 overfitting이 발생할 수 있다.

### Gradient Descent Method  
- 비용함수의 비용 값을 최소화하는 파라미터 $\theta$를 찾는 방법.  

  repeat until convergence {  
    $\theta_j := \theta_j -\alpha \frac{\partial}{\partial \theta_j} J(\theta_0, \theta_1)$  
    (for j = 1 and j = 0)    
  }  

  +. $:=$ : 대입 연산자  
  +. $\frac{\partial}{\partial \theta_j}J$: cost 함수 $J$의 미분 값  
  +. $\alpha$ : learning rate  
    &emsp; -. 갱신되는 $\theta$값의 속도를 결정

![Gradient Descent Algorithm](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJLsIr%2FbtqDQtpPGZt%2Fwxt7CbUZXUZ1FZpHpbbR6K%2Fimg.png)  

#### 1) Derivative Term  
- $\theta(= w)$가 반복적으로 갱신되면서 최솟값에 도달. 
  + $\theta$ 갱신 조건: 기울기 하강과 기울기 상승의 2가지 경우가 있음.
    - 기울기 하강  
      : 포물선의 대칭축을 기준으로 오른쪽 영역에서 한 지점을 초기값으로 설정한 경우, 우측 영역의 기울기(미분값)는 양수이므로, 갱신시 $\theta$는 감소하여 최소값 지점으로 이동  
      ![기울기 하강](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcnTybb%2FbtqDPMKoFro%2FiKK454EqCOlkhjoBC3YDB1%2Fimg.png)  
    - 기울기 상승  
       : 포물선의 대칭축을 기준으로 왼쪽 영역에서 한 지점을 초기값으로 설정한 경우, 좌측 영역의 기울기(미분값)은 음수이므로, 갱신시 $\theta$는 증가하여 최소값 지점으로 이동  
      ![기울기 상승](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbupXVw%2FbtqDQUHupTQ%2FJlLvPbOR2OYkPxUthK2qJ0%2Fimg.png)  

#### 2) Learning Rate(학습 속도)  
- learning rate의 의미
  + learning rate가 작을 경우
    : 최소값 도달을 위해 많은 연산 필요
  + learning rate가 클 경우
    : 
  + 만약 Learning Rate없이 미분값으로만 갱신을 진행하게 되면 최솟값으로 도달하지 않고, 제자리에서 진동(learninf rate를 곱하여 갱신값에 변화를 주며 최소값에 도달)

  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDtIZs%2FbtqDPMQ9vGX%2FRdyVDU4jg4MZttZtQFPzik%2Fimg.png)  

#### 3) θ의 수렴 조건
: 


## Review of logistic regression
- Softmax (Logistic) regression 은 각 클래스 별 대표벡터를 학습합니다. 그림은 5 개의 클래스의 데이터이다. 그리고 star marker는 각 클래스의 대표벡터이다. 학습된 classifier는 새로운 $x$ 가 입력되었을 때 대표벡터들과의 내적 기준으로 가장 가까운 클래스로 $x$의 레이블을 판별한다.

$\LARGE P(y=1 | x) \brack P(y=n | x) $ = $\LARGE exp(θ ^T _1 x) \brack ∑ _k exp(θ ^T _1 x) \LARGE$  

## Logistic regression with L2 regularization
### Regularization 
- 학습되는 대표벡터의 크기와 모양을 조절
  + L2 norm은 벡터의 Euclidean 크기를 나타낸다. 예) (3,4)의 2차원 벡터는 $\sqrt (3^{2} + 4^{2}) = 5$
  + cost 는 학습된 모델의 비용, ML 알고리즘은 이 비용을 줄이는 방향으로 모델~~coefficient~~을 학습
  + Logistic regression 의 입장에서는 대표벡터가 학습할 모델
  + cost는 주어진 $x$로 $y$를 얼마나 잘 예측하는지에 대한 error와 학습된 모델의 norm의 합
    - $\lambda ||\theta||_2 $는 logistic regression 이 학습하는 coefficient vector 의 L2 norm  
      (대표벡터들의 L2 norm 의 합)
    - L2 regularization 을 이용하는 logistic regression 은 이 대표벡터의 크기를 줄이는 방향으로 학습을 유도 (Ridge regression이라고도 함)




# [Regularized Logistic Regression
- [Ref_01](https://brunch.co.kr/@linecard/487), [Ref_02](https://lovit.github.io/nlp/machine%20learning/2018/03/24/lasso_keyword/)  

- Logistic regression 은 feature X와 클래스 Y간의 관계인 클래스의 대표벡터를 coefficients에 학습한다. 대표벡터 (coefficient)를 구성하는 값 $α_{kj}$들은 $j$ 번째 feature, $X_j$와 클래스 $k$와의 상관성이다. 때로는 coefficients vector가 sparse vector가 되도록 유도함으로써 classification에 중요한 몇 개의 features 만을 이용하도록 강제할 수 있다. 이를 L1 regularization 혹은 LASSO model이라 부른다. LASSO는 feature selection의 역할을 하며, 이를 응용하여 keyword extraction 할 수 있다.  

- 로지스틱 회귀에서 최적화 알고리듬으로 경사하강 기법(cost function을 최적화하는 알고리듬)과 고급최적화기법(cost function을 계산하는 방법과 미분항을 계산하는 방법을 제공해야하는 알고리듬)이다.




## Overfitting
- ~~모델이 훈련데이터에만 특수한 성질을 과하게 학습해 일반화를 못해 결국 테스트 데이터에서 오차가 커지는 현상~~
- 모델의 파라미터들을 학습 데이터에 너무 가깝게 맞췄을 때 발생하는 현상으로, 학습 데이터에 너무(과) 적합하여(적합) 다른 데이터에 대해 정확한 예측을 하지 못하는 현상  
  + 학습 데이터에 대해 과학게 학습된 상황

- 원인
  + Model Capacity (모델이 더 복잡한 셩상을 나타낼 수 있는 정도)를 늘린 경우
    - layer를 deep하게 쌓거나 layer당 hidden unit을 늘린 경우  

  + 모델이 샘플 데이터를 너무 오래 학습하는 경우
  + 모델이 너무 복잡한 경우
  + 학습 데이터의 샘플 개수가 충분하지 않은 경우  

- 방지 방법
  + 학습 데이터에 적합한 Model Capacity를 가지도록 모델 설계
    - train에 사용하지 않는 test set을 두고, test set에 대한 모델 동작 평가 → Train sample의 loss는 계속 감소하는데 Test sample의 loss만 계속 증가한다면 overfitting 발생으로 판단 가능  
  + 학습 데이터 세트의 일부를 테스트 세트로 따로 설정하여 과적합 여부 확인
  + 관련성이 낮은 입력을 제거하여 모델의 복잡성을 감소시킨다.

  + [Model Capacity 낮추기: 모델이 학습 데이터에 비해 과하게 복잡하지 않도록, hidden layer 크기를 줄이거나 layer 개수를 줄이는 등 모델 단순화](https://22-22.tistory.com/35)  
  + Dropout: 학습을 할 때 일부 뉴런을 끄고 학습  
  + L1/L2 정규화(L1/L2 regularization)  
  + 학습 데이터 늘리기(data augmentation)    
    - Test Set Accuracy가 증가하다가 감소하면 학습 데이터가 부족한 경우  
    - Training Set Accuracy가 100%에 가깝지만 Test Set Accuracy가 낮은 경우, 학습 데이터 편향(특수한 경우의 데이터를 가지고 일반적인 문제에 적용하려는 경우에 해당)  


## Underfitting
- train set도 학습을 하지 못한 상태  
- 일반화 성질도 학습하지 못해 훈련/테스트 데이터 모두에서 오차가 크게 나오는 경우

- 원인  
  +

- 방지 방법  
  + 


## 검증 : K​-Fold Cross-Validation


※ Bias : 모델의 예측값과 실제 값 차이를 측정 한 값. 모델이 지나치게 단순화되면 예측 값이 실제 값과 멀어져서 더 큰 bias가 발생

※ Variance : 다양한 데이터셋의 예측값들이 얼마나 일관성 있는지 없는지를 측정한 값. 모델의 성능이 서로 다른 데이터셋에서 테스트 된다고 가정할 때, 예측값이 실제와 유사할 수록 variance(분산)이 작아진다. 즉, 분산이 높을 수록 모델이 일반화되지 못하였고 overfitting되었다고 말할 수 있다.

※ Capacity : 모델의 형상을 나타낸 정도이다. 즉 capacity를 늘린다는 것은 layer를 더 deep하게 쌓거나 layer당 hidden unit 개수를 늘리는 등 학습 파라미터 수를 늘리는 것

※ over/under fitting은 오차의 편향과 분선 개념과 관련이 있다.
- 분산이 높을 경우: 모델이 학습 데이터의 노이즈에 민감하게 적합하여 테스트 데이터에서 일반화를 잘 못하는 경우(과적합)
- 편향이 높은 경우: 모델이 학습 데이터에서 특성과 타겟 변수의 관계를 잘 파악하지 못한 경우(과소적합)

![](https://velog.velcdn.com/images%2Fjoo4438%2Fpost%2Fc759a5f6-d3c5-4c33-ade9-78c4cfec4b85%2Fimage.png)  

![](https://velog.velcdn.com/images%2Fjoo4438%2Fpost%2F733d73c5-8804-41b4-aa78-0e45c0baa2b4%2Fimage.png)


--- 

[^1]: 연속된 n번의 독립적 시행에서 각 시행이 확률 p를 가질 때의 이산 확률 분포이다. 이러한 시행은 베르누이 시행이라고 불리기도 한다. 사실, n=1일 때 이항 분포는 베르누이 분포이다.

[^2]: 확뷸분포에서 x가 발생했을 때, x가 나오게하는 파라미터의 가능성.
      Likelihood란, 데이터가 특정 분포로부터 만들어졌을(generate) 확률을 말함. 예를 들어 
      $X = (1,1,1,1,1)라는 데이터가 존재할 때, 데이터 X는 아래 두 분포 중에서 왼쪽 분포를 따를 확률이 더 높다. 그러므로, 왼쪽 분포의 데이터 X에 대한 likelihood가 더 높다고 표현할 수 있다.
      ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJEPr4%2Fbtqz7pMPeHW%2FHkDNuGNsUZ6tb9tVCfw6M0%2Fimg.png)






