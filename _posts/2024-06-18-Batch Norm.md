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
