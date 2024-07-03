---
title: 다양한 Gradient Descent
date: 2024-06-13 17:00:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Gradient Descent, Momentum, AdaGrad, RMSProp, Adam]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---
지난 포스팅에서 Gradient Descent의 기본적인 방식, SGD, Mini-Batch GD를 작성했다.
이번 포스팅에서는 보다 다양한 방식의 GD를 작성한다.

<div align=center>
    주요개념
</div>
> Momentum   
> AdaGrad   
> RMSProp   
> Adam

# 0. 보다 다양한 방식의 Gradient Descent가 나오는 이유.
Gradient Descent, SGD, Mini-Batch 등 기본적인 Gradient Descent를 사용 시 Loss가 특정 방향으로는 빠르게 학습될 수 있으나, 다른 방향으로의 학습이 느리게 될 수 있다. 즉 Gradient Descent의 방향이 흔들리면서 진행된다는 의미다. <br>
이는 결과 적으로 **학습의 효율성이 떨어지는 것이다.**

# 1. Momentum
이러한 학습의 효율성을 끌어올리기 위해서 나온 여러 GD의 방법론이 나왔다.   
Momentum은 Gradient 업데이트 시 이전에 이동해왔던 Gradient들을 반영하여서 업데이트를 하는 방식이다. 이전 Gradient의 방향성을 일정 부분 반영하는 학습을 진행하는 것이다.   
기존 SGD의 수식은 다음과 같다.

$$
\text{SGD} \\
x_{t+1} = x_t - \alpha \nabla f(x_t)
$$

SGD 방식은 Loss가 Local Minima에 도달했을 경우 Local Minima에서 벗어날 수 없다는 단점이 있다. 이를 해결하기 위해 위에서 언급하였듯이 이전 Gradient들을 반영하여 이전 방향성과 값을 반영하는 방식으로 Gradient Descent를 진행하는 것이다.   

$$
\text{SGD + Momentum}\\
v_{t+1} = pv_t - \alpha \nabla f(x_t) \\
x_{t+1} = x_t + v_t+1
$$

$v_{t+1}$은 이전 Gradient의 값들이 지속해서 축적된 값들이 되어 Local Minima에서 벗어나지 못했던 SGD에서 해결된다. $p$는 Momentum에 할당되는 가중치를 뜻한다. 0.9 혹은 0.99가 일반적으로 사용되는 값이다.
이 방식의 Gradient Descent는 기존 SGD보다 먼 거리를 이동할 수 있게되어서 Gradient의 진동을 줄이며 학습의 최적화 과정이 부드럽게 진행된다.

# 2. Naive Momentum과 Nestrov Momenum
**Naive Momentum**이라고 표현하는 위에서 언급한 Momentum은 결과적으로 현재 Gradient + Momentum의 형식으로 학습이 이루어진다. 이 형식에서 착안한 아이디어로 Momentum 만큼을 미리 움직인 이후 해당 위치에서의 Gradient를 측정, 학습하는 방식을 **Nestrov Momentum**이라고 한다.

$$
\text{Nestrov Momentum}\\
v_{t+1} = pv_t + \alpha \nabla f(x_t + pv_t)
x_{t+1} = x_t + v_{t+1}
$$

Nestrov는 이를 통해 학습의 최적화와 수렴이 보다 잘 이루어진다.


>Naive, Nestrov 두 방식 모두 각각의 특징을 가지고 있으며 둘 중 어느 것이 무조건 성능이 좋다고 말하기는 힘들다. 두 방식 모두 데이터의 특징에 따라 다르게 작동할 수 있다.

# 3. AdaGrad

이전 Gradient의 축적인 Momentum이 등장한 이후 이를 활용한 다양한 방식들이 등장했다.
우리가 Gradient를 다양한 방식을 통해서 하강하는 이유는 Gradient Descent 시 하강이 진동하면서 이루어 지기 때문이다.   특정 변수에 대해서는 변화 폭이 크고, 다른 특정 변수에 대해서는 변화폭이 좁다는 문제인 것이다.   
이를 해결하기 위한 아이디어로 큰 값은 보다 큰값으로, 작은 값은 보다 작은 값으로 나눠주어서 두 값들의 차이를 줄여나가는 방식이 **AdaGrad 방식이다.**   

$$
\text{AdaGrad}\\
v_t = v_{t-1} + \nabla f(x_t) \bigodot \nabla f(x_t) = v_t + (\nabla f(x_t) \text{제곱의 누적합})\\
x_{t+1} = x_t - \frac{\nabla f(x_t)}{\sqrt{v_t}}
$$

하지만 $v_t$에 계속해서 양수가 계속 더해지게 되고 이는 한없이 커지게 된다.   
때문에 $x_{t+1}$이 계속해서 0으로 작아진다는 문제점이 발생했다.

# 4.RMSProp
AdaGrad의 해결을 위해서 등장한 방식이 **RMSProp**이다.   
$v_t$를 무한정 키우지 않기 위해서 가중치를 반영한다. 이를 통해 무한정 커지는 것을 방지하는 방식이다.

$$
\text{RMSProp}\\
v_t = \beta v_{t-1} + (1-\beta) \nabla f(x_t) \bigodot \nabla f(x_t)\\
x_{t+1} = x_t - \frac{\nabla f(x_t)}{\sqrt{v_t}}
$$

위 식에서 $v_t$의 가중 평균을 통해서 계산하며, $\beta$는 일반적으로 0.99로 설정한다.   이 평균은 정확한 평균은 아니나 t가 커져감에 따라 오차가 점점 줄어든다.


# 5. Adam
RMSProp + Momentum을 사용한 방식이 Adam이다.  위에서 등장한 방식 중 RMSProp에 이전 Gradient들의 누적 합을 반영하는 것이다.

$$
m_0 = 0 \quad v_0 = 0 \\
m_t = \beta_1 m_{t-1} + (1-\beta_1)\nabla f(x_t) \qquad
v_t = \beta_2 + (1-\beta_2)(\nabla f(x_t) \bigodot \nabla f(x_t))\\
x_{t+1} = x_t - \alpha \frac{m_t}{\sqrt{v_t}}
$$

위 수식에서 $m_t$가 이전 Gradient들의 누적합이 기에 이전 Gradient들도 훨씬 잘 반영하게 된다.   
$\beta_1 = 0.9 \quad \beta_2 = 0.999$가 가장 많이 쓰인다.


이러한 Adam을 사용하기 위해서는 초기 $t$가 작았을 때 값을 보정 해줄 필요가 있다.   
