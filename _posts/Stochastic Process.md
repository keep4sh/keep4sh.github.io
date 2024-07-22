Stochastic Process
시계열 프로세스의 원천이 되는 이론.
시간 축 마다 정의 되는 Random Variable들의 집합
- 시간은 Float으로 정의되기 때문에 무한성이 들어감.
$X_t$ 가 자체분포를 갖고 선택되어 샘플링 된 것이 데이터. -> 이것들을 다 이어 붙인 것이 시계열

Gausian Process 
 Stochastic Process 안의 Random Variable이 가우시안 분포의 흐름을 따르면 말함.

Stationarity
 샘플 하나에 대해서 말하는 개념 X,
 Stochastic Process의 모든 Random Variable들이 아래 조건을 만족할 때 다음과 같이 말함.
- weak Stationarity
뮤와 시그마가 모두 같을 때
- Strong Stationarity
항상 같은 분포를 가지는 것.

우리가 시계열로 예측을 하는 것은 Stationarity를 어느정도 만족할 때 가능하다.
이 Stationarity, Non-Stationarity는 흑,백의 논리가 아니다.
때문에 Non-Stationarity한 정도를 줄여주기 위해서 래빈이라는 것을 사용.

Autocovariance
 - 실전에서 데이터 EDA 시 많이 사용

decomposition
 - 시계열 데이터는 Trend , Seasonality, Residuality -> 둘 제외 나머지
 - 시계열 방법론 얘기할 때 많이 나옴.
 - 방법론 2가지 존재
    1. 각 요소의 합으로 이루어짐
    2. 각 요소의 곱으로 이루어짐.

    Data Smoothing : moving average / exponential moving average


ARIMA Model
Too hard, Stay strong

Transformer를 이용한 시계열 예측 부분이 중요!
Informer가 핵심. (마스킹) Attention Score를 전체를 재서 유의미한 값을 가지는 것들만 최종 아웃풋을 예측. ProbAttention -> 코드 상에서 Prob Attention을 이해하자.

DLinear : 
NLinear : input의 마지막 값으로 자기 자신을 빼주어서 연산을 진행하는 모습

Patch TST :  

TimesNet / TSLib이라는 라이브러리 아주 중요하다.


 Dilated Causal Convolution


 # 2. 시계열 이상 탐지

 Time Series anomaly detecton
 - 평균값, 주기성, 노이즈 발생 등. / 경향성을 벗어나느 것을 이상치로 하여 탐지
 - method 별로 윈도우 단계로, point 별로 abnomaly를 측정 가능

## Reconstructor 기반

### LSTM Autoencoder
인코딩하고, 디코딩 시 Restruction을 진행 -> Reconstruction error를 기준으로 이상 데이터 구분.

만약 학습에서의 분포와 다른 분포가 들어오면 Reconstruction이 제대로 진행되지 않아서 abnomal로 탐지할 수 있음.

### USAD - 강의 중 구현도 진행
- Adversarial Training

## Reconstructor Error 기반이 아닌 이상탐지

### MAD-GAN
일반 구조 자체는 GAN과 동일함.
Abnormal을 찾고 싶은 window를 GAN Inversen으로 찾아서 generator의 Input으로 넣어줌.
-> Discriminator Loss, Reconstruction error의 합으로 Score 사용


### Anomaly Transformer
Series 내 데이터들 중 abnomal한 포인트는 자신과 가까운 곳들만 높은 연관성을 가진다. (Series 중 abnomal이 적다는 가정이 깔려있었어야 함.)

학습은 일반 Transformer를 사용한다.
- LSTM 때 처럼 Reconstruction Error를 사용할 수도 있다.
- 그렇기에 Attention Vector로 뽑을 수 있고 Abnomal은 Gaussian으로 표현된다. 
- Association에 대한 설명들 정리



시계열 코드들은 거기서 거기임. (TSLib에서 기반)