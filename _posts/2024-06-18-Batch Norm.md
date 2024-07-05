---
title: Batch Normalization
date: 2024-06-18 13:00:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Batch Noramalization]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

지난 포스팅에 Normalization의 필요성과 L1, L2 Norm에 대해서 작성해 보았다.   
오늘 Batch Normalization에 대해서 작성한다.

<p align=center> 주요 개념</p>

> Normalization
> Stadardization
> Batch Normalization

# 0. Deep Learning에서 Normalization이 필요한 이유.

우리는 모델의 학습을 위해서 임의로 Weight를 초기화 한다. 하지만 이를 통해서 Activation Function을 통과한 Output이 극으로 향할 수 있다.
이는 Activation Func의 포화된 Output으로 인해서 Parameter, Weight의 업데이트가 진행되지 않는 문제를 발생시킨다.   
이를 해결하기 위해 Normalization을 통해서 Input을 조정해주는 것이다.    
예를 들어 우리의 Activation Function이 Tanh라고 생각해보자.

$$
\tanh(x) = 2 \times sigmoid(x) -1
$$

![Tanh Graph](../assets/img/function/Tanh)

Tanh 그래프에서 x가 -2.5 ~ 2.5가 아닐 경우 Gradient의 업데이트가 제대로 이루어지지 않을 수 있다. 이는 반대로 "**x가 -2.5 ~ 2.5와 같이 특정 범위에 있다면 Gradient의 업데이트는 원활하게 진행될 것이다**"로 생각 해볼 수 있다.    
이를 위해서 우리는 Activation Function을 통과하기 전 Input을 조정해주는 것이다.
   
# 1. Batch Normalization
그럼 정규화면 정규화지 왜 Batch Normalization이 나왔을까?
우리는 지난 Gradient Descent 기초 포스팅에서 Gradient Descent와 SGD를 융합한 방식인 Mini-Batch Gradient Descent에 대해서 보았다.    
 같은 데이터 셋에서 여러 Batch로 분할된 데이터를 학습하는 과정인다. 이를 생각해보았을 때 각 Batch 마다 통계적인 특징이 다르게 나타나는 Batch가 생성될 것이다. 즉, 우리의 모델이 학습하는 Input들이 각각 너무나 다른 특성을 지닌 채 학습된다. 때문에 학습이 원활히 진행되지 않을 수 있다.   결과적으로 각 Batch마다 유사한 통계적 특징을 주기 위해서 우리는 Batch 단위로 Normalization이 필요하다.

# 2. Standardization
Standardization은 표준화이다. 각 데이터를 (0,1) 사이에 위치하도록 조정하는 방식이다.
각 데이터에 데이터 셋의 평균을 빼고, 표준 편차로 나눠주는 것이다.
$$
x_{\text{standardized}} = \frac{x - \mu}{\sigma}
$$

표준화는 이상치가 다른 값들에 비해 너무 클 경우 데이터들이 0에 쏠리게 되는 결과를 낳을 수 있다.

# 3. 중요한 부분.
이 Batch Normalization에서 핵심으로 기억할 부분은 Activation Fucntion에 들어가기 전 Input을 Batch 단위로 통계적 특징이 다를 것이기 때문에 이를 비슷하게 맞춰줄 수 있게 정규화를 시행하는 것이다. 통계적 특징을 Batch 마다 통일해 준다면 반드시 (0,1) 사이에 위치할 필요는 없다는 의미이며 모델에게 Parameter로서 분포를 조정하게 할 수 있다.
위 문장에 대한 이해를 반드시 가지기 바란다.