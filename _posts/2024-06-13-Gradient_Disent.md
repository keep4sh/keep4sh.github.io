---
title: Gradient Descent 기초
date: 2024-06-11 09:00:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Gradient Descent]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

지난 포스팅까지 우리는 Foward Propagation을 통해서 Loss를 구하고, Loss를 통해서 새로운 Weights를 구하기 위한 Back Propagation을 시행하는 방식을 알아보았다.   
이번 포스팅에서는 Weights를 Update 하기 위한 Gradient Descent를 작성한다.
<div align=center>
    주요개념
</div>
> Gradient Descent   
> Stochastic, Mini-Batch   
> Learning Rate   

# 1. Gradient Descent
Loss를 최소화 하기 위해서 Back Propagation을 통해서 경사를 구하고 이 경사의 반대 방향 (-1을 곱해줌)으로 Weights를 업데이트 해주면서 Loss가 최소화 되는 값을 찾는 과정이다. 이 방식은 정확한 연산이 가능하나 전체 Data Set이, Input의 크기가 커질 수록 연산이 오래걸린다는 단점이 존재하나다.

$$
\text{Gradient Descent}\\
\nabla W\frac{1}{N} \sum_{i=1}^N L(x_i, y_i;W)
$$

# 2. Stochastic Gradient Descent
데이터 하나만을 이용해서 Gradient Descent를 시행하는 방식을 진행한다.
이 방식은 데이터 하나만을 가지고 사용하기에 부정확한 결과가 나올 수 있으나 계산 자체는 빠르게 나올 수 있다.   

$$
\text{Stochastic Gradient Descent}(SGD)\\
\nabla W L(x_i, y_i,; W)
$$

# 3. Mini-Batch Gradient Descent
위 두 방식은 각각 장,단점이 뚜렷하다. 이를 융합하여 사용한 방식이 Mini-Batch Gradient Descent이다.   
특정 하나의 데이터만을 가지고 GD를 실행하지 않고 전체 데이터 셋에서 Sampling을 시행하여 샘플 데이터 셋을 만들고 Loss를 최소화 하도록 GD를 시행하는 방식을 말하다.

$$
\text{Mini-Batch}\\
\nabla W L(W) = \frac{1}{|Batch|} \sum_{i \in Batch} L (x_i, y_i,; W)
$$

Batch의 사이즈도 파라미터의 하나로서 모델에게 줄 수 있으며, 컴퓨터의 구조 상 2의 배수가 유리하다.   
Batch가 커질 수록 Gradient 값의 분산이 적어진다. (전체 데이터 셋과 유사하게 커지기 때문에)

> 전체 데이터 셋 : 100개   
> Batch Size : 20개   
> Batch를 5번 돌 경우 전체 데이터 셋을 한 번 순회 하기에 1 Epoch이라고 표현한다.   
> Batch를 업데이트 할 때 마다 1 Iteration이라고 표현한다.

흔히 논문들에서 SGD를 사용했다고 표현하는 것은 대부분 하나의 데이터를 통해서 GD를 시행했다고 의미하는 것이 아닌 Mini-Batch GD를 의미한다. 혼용해서 사용하는 편.


# 4. Learning Rate
Gradient Descent를 통해서 $w - {\operatorname{d}\!L(w)\over\operatorname{d}\!w}$와 같이 w를 업데이트 한다면 단점이 존재한다. 
1. 학습의 속도가 느리다. Gradient가 0에 가까워 질 수록 업데이트가 느려지기 때문이다.
2. Local Minima에 빠질 수 있다.

이를 해결하기 위해서 우리는 Learning Rate를 주어서 Weights를 업데이트 하게 된다.   

$$w= w-\alpha(\text{learning Rate}) {\operatorname{d}\!L(w)\over\operatorname{d}\!w}$$

|Learning Rate의 크기|특징|
|클 때|Loss가 줄어드는 양이 커진다. / 너무 클 경우 Loss가 커지는 방향으로 업데이트 되기도 한다.|
|작을 때|Loss가 줄어드는 양이 작다. / 너무 작을 경우 Loss가 줄어들지 않을 수도 있다.|

위 특징들로 인해 적절한 Learning Rate를 설정하는 것이 중요하다.

# 5. Learning Rate Scheduler

Learning Rate를 Loss가 줄어듬에 따라서 조정할 수 있게 설정하는 방법이 존재한다.   
Epoch이 커짐에 따라서 Loss가 줄어들게 되고 이에 따라 Learning Rate를 줄이면 된다.   
이 방식을 Learning Rate Scheduler 기법이라고 한다.

1. Step Decay : 정해진 Epoch 마다 Learning Rate를 절반씩 줄여나가는 방식이다.
2. Exponential Decay : Learning Rate를 지수 함수처럼 줄여나가는 방식이다. 얼마나 줄여나갈지를 정할 수 있으며 학습 초기에 빠른 학습을 위해 Learning Rate를 크게 잡고 진행하고 Epoch이 진행됨에 따라 줄여가는 방식이다.

