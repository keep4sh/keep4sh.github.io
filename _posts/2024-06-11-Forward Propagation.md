---
title: Forward Propagation와 Back Propagation
date: 2024-06-11 10:37:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Forward Propagation]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

# 1. Forward Propagation의 개념

기존 MLP 과정은 결국 하나의 Input data를 여러 Weight를 곱하는 것임으로 다음과 같다.   

$$
w_1 \times w_2 \times x = w_3 \times x$$ 

즉 Layer를 아무리 여러개 쌓아도 결국 하나의 Layer만 가지고 연산하는 것과 다를 게 없다라는 의미가 된다.   
이를 해결하기 위해 특정 Layer를 활성 함수를 사용해서 변경 시키는 것이다.    

$$
w_2 \times x \rightarrow f(w_2 \times x)$$

$$
\quad w_1 \times f(w_2 \times x) \quad !=  \quad w_3 \times x\quad
$$

이렇게 특정 가중치에 대한 연산을 활성함수를 통해 비선형적으로 변환하면 무엇에 이점이 생기는가?   
하나의 Layer로 변환되는 것을 막을 수 있다으며 이는 결국 Layer를 쌓아 가는 것의 의미를 줄 수 있다.

# 2. Nerual Network에서 Forward Propagation
# 3. Linear Layer의 개념 및 특성
# 4. 예시 : MNIST Dataset
MNIST (Modified National Nstitute of Standards and Technology)   
사람의 손글씨 사진 Data set, Train 55,000개와 Test 10,000개이다.   
한 사진 당 28 x 28의 픽셀로 구성되어 있다. 즉, 784 vertor로 표현된다.   
784개의 Data를 Hidden layer를 전진적으로 통과하면서 Label Output을 만들고   
만든 Output 마다의 가중치를 확인하고 **"가중치가 가장 높은 것으로 예측을 하자"**


# 5. 참고 링크 및 용어 정리

|:---|---|
| 활성화값 | 특정 Layer의 특정 유닛 / 즉 특정 Perceptron의 Output을 의미 |
| 가중치 Matrix | Layer와 다음 Layer를 있는 가중치의 행렬 |

[순전파, 역전파, 연산그래프](https://ko.d2l.ai/chapter_deep-learning-basics/backprop.html)