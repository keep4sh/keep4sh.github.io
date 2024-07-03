---
title: Forward Propagation
date: 2024-06-11 10:37:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Forward Propagation]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---
# 1. Foward Porpagation의 아이디어
Foward Propagation은 MLP의 한계를 극복하기 위해서 등장했다.
MLP에서 Input x에 대한 선형 변환을 거친 최종 Output **$y$** 의 간단한 모습은 다음과 같다.

$$
y = w_2 x_2 \\
y= w_2 x_2 = w_2 (w_1 x_1)\\
y = w_2 \times w_1 \times x_1 = w_n \times x_1$$

MLP의 Layer를 아무리 많이 쌓아도 결국 하나의 $w_n$을 $x_1$과 함께 연산해주는 결과가 된다, 따라서 Layer가 많은 것의 의미가 퇴색되어 버린다.

이는 MLP의 선형성 때문에 발생하는 문제로 이를 해결하기 위해 비선형 함수의 형태인 활성 함수 (**Activation Function**)을 Perceptron의 Output에 적용해 주면서 선형성을 해결하고자 했다.

$$
\text{Linear Regression} = w_0 + w_1x_1 + w_2 x_2\\
\text{With Activatino Function} = f(w_0 + w_1x_1 + w_2x_2) \rightarrow Outputs
$$

하나의 Layer로 변환되는 것을 막을 수 있다으며 이는 결국 Layer를 쌓아 가는 것의 의미를 줄 수 있다.

# 2. Forward Propagation (순전파)
Perceptron 하나는 Vector 연산으로 표현이 가능해진다.<br>
이렇게 Input $x$에서 부터 최종 Output인 $y$를 연산하는 과정을 의미하며 Model은 이를 Vector 형태로 저장한다.

> $$
> \text{Weights Vector} = \begin{bmatrix}
>     w_0 \quad w_1 \quad w_2 \\
>     w_3 \quad w_4 \quad w_5
> \end{bmatrix} \\
> $$
> 
> $$
> \text{Input Vector} = \begin{bmatrix}
>     x_0 \quad x_1 \quad x_2
> \end{bmatrix}
> $$
> 
> $$
> \text{Weights_Vector} \times\text{Input_Vector}\\
> = 
> \begin{bmatrix}
>     w_0x_0 + w_1x_1 + w_2x_2\\
>     w_3x_0 + w_4x_1 + w_5x_2
> \end{bmatrix}
> $$

해당 Vector 연산은 Bias와 활성 함수를 고려하지 않은 형태이다.<br>
이 과정은 하나의 Layer를 지나면서의 연산이며 이를 여러번 거치면서 최종 아웃풋의 가중치들이 나온다.<br>
모델이 예측한 아웃풋이 원 데이터의 결과값과 얼마나 차이가 있는지를 확인하고 차이가 최소화 되게 모델을 학습 시켜야 한다.


# 3. MSE

$$
\hat{y} = w_1x_1 + bias\\
\text{Loss}= (y-\hat{y})^2\\
$$

위 Loss를 최소화하면서 학습을 진행할수록 모델이 데이터를 잘 학습하게 되는 것이다.<br>
> 위에서 사용한 Loss는 다양한 형태로 정의되며 목적 함수 혹은 손실 함수라고 표현한다.
MSE (Mean Squared Error)는 이러한 함수들의 한 예시이다.
$$
\text{MSE} = \frac{\sum_{k=1}^N (\hat{y_k} - y_k)^2}{N}
$$
위 수식처럼 MSE는 Target의 종류 N만큼 나오는 차의 제곱의 합의 평균을 구하는 목적 함수다. <br>
(뭔가  ~~의 가 많이 붙어 표현이 길어지니 수식으로 기억해보자.)

- 오차의 표현 방식에서 오는 차이
> 제곱으로 차를 표현하는 것은 차이가 음수로 표현될 수 있기 때문이다. <br>
> 이 차이의 값 자체가 우리에게 중요하기에 이를 제곱으로 표현해주는 것이다. <br>
> 이는 절대적인 기준이 아니며 제곱이 아닌 절댓값을도 표현이 가능하다. <br>
> 어떤 방식으로 표현해도 좋으나 두 방식에 차이가 있다.
> 제곱으로 오차를 표현 하였을 때 오차가 클 경우 이를 빠르게 줄여나가면서 학습 할 수 있다는 장점 이있다. 
> 이처럼 절댓값과 제곱은 수치 자체에서도 차이를 보이며, $e_3$를 -3에서 -2로 줄인다면<br>
> $e_3$ 값이 제곱 오차에서는 4로 5만큼 줄고, 절댓값 오차에서는 2로 1만큼 준다.

$$ 
e_1 = (\hat{y_1} - y_1) = -1 \quad e_2 = (\hat{y_2} - y_2) = 2 \quad
e_3 = (\hat{y_3} - y_3) = -3 \\
\text{제곱 오차} e_1^2 + e_2^2 + e_3^2 = 14 \quad \text{절댓값 오차} = |e_1| + |e_2| + |e_3| = 6
$$

- MSE 자체의 문제<br>
MSE는 Loss와 Gradient에서 크기의 상한이 존재하게 된다. <br>
1. 오차를 확률론적으로 표현하게 될 때 오차는 [-1, 1]로 표현되고 오차의 합은 결국 1보다 커질 수 없다.
2. 마찬가지로 확률론적 표현으로 인해 오차는 [-1, 1]의 범위를 갖게되며 손실함수의 경사가 2보다 작을 수 밖에 없다는 문제이다. 이는 학습 속도가 느려진다는 문제가 있다.<br>
아직 해당 문제가 와닿지는 않으나 이후 Back Propagation에서 문제가 발생하게 된다.


# 4. 확률론적 접근을 위한 SoftMax
단순히 linear layer를 거친 연산값 자체는 아무 의미를 가지지 못하는 숫자일 뿐이다.<br>
이 숫자갑들을 확률 Vector로 변환 시키기 위해서는 우선 Hidden Layer의 결과값을 양수로 만들어 주는 다양한 함수들을 사용하며, 함수의 결과값을 확률처럼 변환해주는 것, 즉 유의미한 숫자로 변환해주기 위해 각 결과값을 결과값의 합으로 나눠준다면 이는 유의미한 확률로 변환되는 것이다. <br>

이처럼 확률 Vector로 결과값을 변환하는 Layer가 **Softmax Layer** 이다. <br>
대소관계가 역전되지 않는 함수를 사용하는 것이 중요하며 각 Class 별 Softmax Layer의 결과값의 합으로 나눠눔을 기억하면 된다.

# 5. 확률 벡터로 나온 값을 Output으로 변환하기 위해서 사용하는 방식
Softmax Layer를 통해서 우리는 모델의 Output을 확률의 분포로 표현하였다. 이제 이를 우리가 원하는 결과값으로 변환해주어야 한다.
> 우리의 Softmax Layer 값이 [0.3, 0.2 ,0.5]로 나왔으면 <br>
> 우리는 이를 Target처럼 [0, 0, 1]과 같이 표현되어 나오길 원하는 것이다.

확률변수의 분포를 표현하기 위해 KL Divergence를 사용해보자.

$$
P = [0, 0, 1] \quad Q = [0.3, 0.2 , 0.5] \\
D_\text{KL}(P || Q) = - \sum_{x\in X} P(x)\log Q(x) + \sum_{x \in X} P(x) \log P(x) = H(P,Q) - H(P)
$$

이는 결과적으로 Cross Entropy - Entropy로 정리할 수 있다.<br> 다만, 우리의 Cross Entropy $H(P,Q)$는 계속해서 변화하게 된다. 우리의 Q, 예측값이 변화하기 떄문. <br> 하지만 Entropy $H(P)$는 변하지 않는 Target이기에 상수가 된다. 결국 P,Q의 KL Divergence는 P,Q의 Cross Entropy가 된다.

$$
P(H,Q) = \sum_{x \in X} -P(x) \log Q(x) =  - 0 \times \log 0.3 + - 0 \times \log 0.2 + -1 \times \log 0.5 = - 1 \log 0.5
$$



# 참고 링크 및 용어 정리

|:---|---|
| 활성화값 | 특정 활성 함수의 Output을 의미 |
| 가중치 Matrix | Layer와 다음 Layer를 있는 가중치의 행렬 |
|Logit Vector | linear layer의 Output|


[순전파, 역전파, 연산그래프](https://ko.d2l.ai/chapter_deep-learning-basics/backprop.html)