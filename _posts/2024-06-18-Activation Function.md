---
title: Activation Function (Non-linear Function)
date: 2024-06-18 09:00:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Activation Function]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

지난 포스팅까지 Gradient Descent를 시행하는 다양한 방식에 대해서 작성했다.   
이번 포스팅은 Activation Function, 활성 함수에 대해서 포스팅을 작성하겠다.

<div align=center>
    주요 개념
</div>
> sigmoid   
> Tanh   
> ReLU, Dead ReLU   
> Leaky ReLU   
> GeLU

# 0. Activation Function들이 등장한 배경
기존 Posting에서 Activation 관련해서 언급을 한번 했었다. Hidden Layer를 많이 쌓았을 때 Layer가 쌓이는 것이 의미를 갖지 못하고 하나의 Layer로 합쳐진다. 때문에 이를 활성 함수인 Sigmoid를 통해서 0보다 컷을 경우 활성화 해주고 0보다 작을 경우 비활성화 해주는 것이다. 

# 1. Sigmoid
가장 기본적인 Activation Function이다. ( $-\infin, \infin$ ) 사이의 실수를 (0,1)로 변환하는 일종의 확률 값을 제시하는 형태이다.

$$
\sigma(x) = \frac{e^x}{e^x + 1} = \frac{1}{1+e^-x}
$$

# 2. Tahn

# 3. ReLU

# 4. Dead ReLU

# 5. Leaky ReLU

# 6. GeLU