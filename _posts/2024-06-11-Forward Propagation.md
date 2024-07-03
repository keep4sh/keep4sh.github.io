---
title: Forward Propagation와 Back Propagation
date: 2024-06-11 10:37:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Forward Propagation]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---
# 1. Foward Porpagation의 아이디어
Foward Propagation은 MLP의 한계를 극복하기 위해서 등장했다.
MLP에서 최종 Output **$y$** 의 간단한 모습은 다음과 같다.

$$
y = w_2 x_2 \\
y= w_2 x_2 = w_2 (w_1 x_1)\\
y = w_2 \times w_1 \times x_1 = w_n \times x_1$$

MLP의 Layer를 아무리 많이 쌓아도 결국 하나의 $w_n$을 $x_1$과 함께 연산해주는 결과, 따라서 Layer가 많은 것의 의미가 퇴색되어 버린다.

이는 MLP의 선형성 때문에 발생하는 문제로 이를 해결하기 위해 비선형 함수의 형태인 활성 함수 (**Activation Function**)을 Perceptron의 Output에 적용해 주면서 선형성을 해결하고자 했다.

$$
\text{Linear Regression} = w_0 + w_1x_1 + w_2 x_2\\
\text{With Activatino Function} = f(w_0 + w_1x_1 + w_2x_2) \rightarrow Outputs
$$

하나의 Layer로 변환되는 것을 막을 수 있다으며 이는 결국 Layer를 쌓아 가는 것의 의미를 줄 수 있다.

# 2. Forward Propagation (순전파)
Perceptron 하나는 Vector 연산으로 표현이 가능해진다.<br>
이렇게 Input $x$에서 부터 최종 Output인 $y$를 연산하는 과정을 의미한다.

$$
\text{Weights Vector} = \begin{bmatrix}
    w_0 \quad w_1 \quad w_2 \\
    w_3 \quad w_4 \quad w_5
\end{bmatrix} \\
$$

$$
\text{Input Vector} = \begin{bmatrix}
    x_0 \quad x_1 \quad x_2
\end{bmatrix}
$$

$$
\text{Weights_Vector} \times\text{Input_Vector}\\
= 
\begin{bmatrix}
    w_0x_0 + w_1x_1 + w_2x_2\\
    w_3x_0 + w_4x_1 + w_5x_2
\end{bmatrix}
$$

해당 Vector 연산은 Bias와 활성 함수를 고려하지 않은 형태이다.

# 3. Linear Layer의 개념 및 특성

# 5. 참고 링크 및 용어 정리

|:---|---|
| 활성화값 | 특정 활성 함수의 Output을 의미 |
| 가중치 Matrix | Layer와 다음 Layer를 있는 가중치의 행렬 |

[순전파, 역전파, 연산그래프](https://ko.d2l.ai/chapter_deep-learning-basics/backprop.html)