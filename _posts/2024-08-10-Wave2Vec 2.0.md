---
title:  Wave2Vec 2.0
date: 2024-08-10 13:00:00 +09:00
categories: [AI, Deep Learning, Speech Recognization]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Model, ASR]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

# 1. Abstract

Speech Recognization 분야에서 대표적인 모델로 사용되는 Wave2vec 2.0에 대한 리뷰이다.  
음성 데이터는 라벨 데이터를 구하는 과정에서 어려움이 있다. 발음과 억양의 다양성, 음성 데이터의 사이즈로 인한 리소스 등 학습 시 어려움이 있다.
Wave2Vec 2.0에서는 Self - Supervised Learning을 통해서 매우 적은 양의 Label Data를 통해서도 높은 수준의 Word Error Rate를 달성했다.   

# 2. Model Architecture

![Model Architecture](../assets/img/Wave2vec%202.0/Architecture.png)


## 2-1. Bunch of CNN
Wave2Vec은 푸리에 변환을 통해 얻은 mel - spectogram을 사용하지 않고 Raw 형태의 Wave form을 사용한다. 이 Waveform에서 여러 CNN 층을 통해서 Encoding을 진행한다. 해당 Layer의 Output을 **$\text{Z}$** 라고 표현한다.

## 2-2. Masked and Transformer Architecture [Context Network]

$\text{Z}$에서 특정 구간에 대해서 Masking을 진행한다. [논문 내에서 Maksing이라고 서술하지만 읽고 난 느낌으로는 사전에 정의된 CodeBook 내에서 대체, Replacement가 더 옳은 표현이지 않나 싶다.] 매 Time Step 마다 동일한 비율의 부분을 Masking을 진행, 이를 Transformer Layer를 통해서 문맥적 표현을 투사한 벡터를 가져오게 된다.
이를 $\text{C}$로 표현한다.

## 2-3. Quantization module

아까 Feature Encoding을 통해서 추출한 벡터 $\text{Z}$를 Quantization한다. 이 부분이 아주 중요하다. 이 모듈을 통해서 Self - Supervised Training이 가능해진다. 주의할 점은 이 모듈에서 진행하는 Quantization은 Vector Quantization이다. Model의 Parameter 자체를 Quantized 하는 것과는 다른 것이다. 이전 Context Network에서 Masking을 말할 때 언급한 Codebook은 사전에 정의된, 유한한 수 만큼의 표현을 의미한다. WaveForm을 **Discrete** 하게 표현해준다.  
이렇게 **Discrete**한 표현으로 만들어 주는 이유는 다음과 같다.
고차원 벡터로 표현되는 Feature Encoder의 Output $\text{Z}$를 보다 효율적으로 표현하게 된다. 주파수의 형태인 Raw waveform을 일정 구간마다 이산적으로 표현하게 해준다. 이 과정에서 Codebook에서 변형시킬 때 Gumble Softmax 방식을 통해서 선택하게 한다. Gumble Softmax는 Gumble Max Trick에서 BackPorp을 취하기 위해서 Softmax를 취한 형태이다. [이미 Pytorch 내에서 구현됨.]
$$
\text{argmax} \rightarrow \text{Softmax}
$$
해당 모듈의 출력값을 $\text{Q}$ 라고 표현한다.

# 3. Training
Wave2vec 2.0에서 Loss는 CTC Loss를 사용한다. Input으로 들어온 Raw Waveform과 Context network의 Output인 $\text{C}$의 길이는 동일하지 않다. 때문에 Loss 계산을 위해서는 기존의 Loss와 다른 CTC Loss를 사용한다. CTC Loss는 다음과 같이정의 된다.

$$
\text{L}_m = - \log \frac{\exp(sim(C_t, Q_t) / K)}{\sum_{\hat{q} \sim Q_t} \exp(sim (C_t, \hat{q})/ K)} 
$$

$\text{C}_t$와 $\text{Q}_t$의 유사도를 비교,이를 $\text{Q}$의 Output들의 집합과 $\text{C}_t$와 비교한다. 이를 Log를 취함으로서 Gradient 측면에서 안정서을 높인 것이다. [마찬가지로 Pytorch 내에서 구현됨.]

# 4. Language Modle and Decoding
이렇게 구해진 연산으로 구해진 Vector를 통해서 Languge Model에게 Waveform을 전달, 이를 Decoding하여서 Text를 얻어낼 수 있다. 보다 다양하게 활용될 수 있음을 시사한다고 생각한다.

# 5. Result
Wave2vec 모델을 읽으면서 Quantization 부분이 어려웠다. Quantized 된 벡터와 연산을 진행한 Vector가 어떻게 유사도 측정을 할 수 있는 것인지 이해가 어려웠다. 좀 더 공부해 보았을 때, 다음과 같은 결론을 얻었다.
Vector Quantization을 통해서 Quantization된 Vector와  $\text{C}$는 모두 동일한 Vector Space 상에 존재한다. Quantization이 차원을 축소하거나 이를 변환하는 것이 아니라 Vector의 끝점, Value를 Discrete하게 변환해주는 것을 말하며 이렇게 표현하는 방식을 보다 많이 활용한다면 데이터 처리 분야에서 보다 효율적으로 처리 될 것이다.

