---
title: Back Propagation
date: 2024-06-12 13:37:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Back Propagation]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
publishe: true
---
# 1. 합성 함수의 Chain Rule
$f(x,y) = ax^2 + by + c$<br>
$g(\sigma)= g(f(x,y)+d)$

$f(x,y)$에 대해서 $x$로 편미분하는 식 = ${\operatorname{d}\!f\over\operatorname{d}\!x}= 2ax$<br>
$f(x,y)$에 대해서 $y$로 편미분 하는 식 = ${\operatorname{d}\!f\over\operatorname{d}\!y} b$

이를 합성 함수인 $g(\sigma)$에 대해서 미분을 할 때는 chain Rule이 적용된다.
> Chain Rule : 합성함수인 $g(y)= g(f(x))$를 미분하면 $g\prime(y) \times f\prime(x)$가 된다.

$g(\sigma)$에 대해서 $x$로 편미분 = ${\operatorname{d}\!g\over\operatorname{d}\!\sigma} \times {\operatorname{d}\!f\over\operatorname{d}\!x} = g\prime(\sigma) \times 2ax$ <br>

$g(\sigma)$에 대해서 $y$로 편미분 = ${\operatorname{d}\!g\over\operatorname{d}\!\sigma} \times {\operatorname{d}\!f\over\operatorname{d}\!y} = g\prime(\sigma) \times b$

위 규칙을 기억하고 BackPropagation에 대해서 이야기 한다.

# 2. Backpropagation
우리는 Foward Propagation에서 임의의 weights를 가지고 예측을 진행하고 이를 Target의 Label과 함께 연산하기 위해 확률분포로 변환한 후 Loss를 측정하는 방식을 배웠다.<br>
이제 이 Loss를 최적화 하기 위해서 Gradient Descent를 적용하기 위해 어떻게 각 weights에 gradient를 업데이트 해야하는 지 알아야 한다.<br>

이 때 사용하기 위한 방법이 합성 함수의 Chain Rule이다.<br>
각 Layer는 여러 Input들에 Weights와 Bias를 연산하는 것이다. 이는 Layer를 거듭하고 Activation Function, Softmax Layer 등과 같은 여러 함수들을 통과하게 되고 이에 Weights들은 합성함수의 연산이 되는 것이다. 간단한 예시로 들어보자.

$$
\text{Inputs : }x_1, x_2, x_3\\
\text{Weights : } w_{11}, w_{21}, w_{31}, w_{12}, w_{22},w_{32}\\
\text{Ouputs : } y_1, y_2\\
\text{Bias 제외}
$$
이렇게 진행되는 것을 예시로 들었을 때, 우리는 Input과 Weights를 연산하여 $\hat{y_1}, \hat{y_2}$를 구하고 이를 Target Label인 $y_1, y_2$와의 Loss를 구할 수 있다.<br>

$$
\hat{y_1} = x_1 \times w_{11} + x_2 \times w_{21} + x_3 \times w_{31} = f_1(x_1, x_2, x_3)\\
\hat{y_2} = x_1 \times w_{12} + x_2 \times w_{22} + x_3 \times w_{32} = f_2(x_1, x_2, x_3)
$$

Loss를 최소화 하는 것이 Target Label과의 차이를 줄이는 것이고 Loss를 구하는 함수를 $g(\hat{y_n})$라고 정의 하자.<br>

$$
x_1 \text{에 대한 $\hat{y_1}$ Loss를 미분} = g\prime(\hat{y_1}) = g\prime(f_1(x_1,x_2, x_3)) = {\operatorname{d}\!g\over\operatorname{d}\!\hat{y_1}} \times {\operatorname{d}\!f_1\over\operatorname{d}\!x_1}
$$

$$
x_1 \text{에 대한 $\hat{y_2}$ Loss를 미분} = g\prime(\hat{y_2}) = g\prime(f_2(x_1,x_2, x_3)) = {\operatorname{d}\!g\over\operatorname{d}\!\hat{y_2}} \times {\operatorname{d}\!f_2\over\operatorname{d}\!x_1}
$$

위 수식을 통해서 우리는 $w_{11}$에 대해서 Loss Function에 대한 Gradient Descent를 진행할 수 있게 된다.

## Logistic Regression에서의  Backpropagation
## Linear layer에서의 Backproppagation
## Softmax layer에서의 Backpropagation