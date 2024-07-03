---
title: Perceptron의 이해
date: 2024-06-11 09:46:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Perceptron]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

# 1. Perceptron의 개념과 동작 방식

Perceptron : Neural Network의 한 종류로 일종의 선형 분류기 <br>

$$
y = f(w_0 + w_1x_1 + w_2x_2)\\
\text{Input:} x_1, x_2  \quad\text{Output: }y\\
\text{Weights: }w_0, w_1, w_2
\tag{Linear Regression의 모습}$$

<br>
위 수식의 모습에서 sigmoid 함수와 같은 특정 함수 **(Step Function, Activation Function, Non-linear Function)** 를 적용해서 작동하는 단위를 말한다.

$$
\text{Perceptron} = \sigma(w_0 + w_1x_1 + w_2x_2) \\
\tag{ $\sigma$ 를  적용한 모습}$$

이처럼 만들어진 Perceptron은 Neural Network의 기본 동작 방식이 된다.
# 2. Multi-layer Perceptron과 Neural Network
이처럼 생성된 Perceptron을 모아 놓은 단위는 Multi Layer Perceptron이 된다. <br>
Multi-Layer Perceptron은 각 **Perceptron의 Output을** 모아서 **하나의 Output을 다시 생성하는** Perceptron이 생성되는 것이다.<br>

또한 Multi-layer Perceptron을 여러 층을 쌓아 놓은 것을 Neural Network가 형성된다.<br>Neural Network를 MLP라고도 부르기도 한다.
<br>모든 Node가 전부 연결되어 있다면 이를 **Fully-Connected Layer** 라고한다.

|Multi-layered Preceptron|Perceptron들의 Output을 가지고 새로운 Perceptron으로 만드는 것|
|Neural Network          |MLP를 쌓아서 Layer를 만들어 가는 것|
|Fully-Connected Layer   |Layer 내의 모든 Node 간의 연결이 되어 있는 상태|


# 5. 질문
가중치를 0으로 설정하는 것과 과적합 방지를 위한 drop out 기법을 하는 것은 완전히 다른 개념이다.    
때문에 가중치가 0이면 FC-Layer이나 drop-out을 통해서 길 자체를 끊는 것은 FC-layer로 볼 수 없다.


# 용어 정리 및 참고 사이트
- Fully-Connected Layer : Hidden Layer 끼리 모든 Perceptron과 Perceptron이 모두 연결된 상태
- Drop-out : Overfitting을 방지하기 위해 특정 노드를 학습시키지 않고 삭제하는 것

[Neural Network Play Ground](https://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.95560&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)   
[위키피디아 Perceptron](https://ko.wikipedia.org/wiki/%ED%8D%BC%EC%85%89%ED%8A%B8%EB%A1%A0)   
[위키피디아 베타적 논리합](https://ko.wikipedia.org/wiki/%EB%B0%B0%ED%83%80%EC%A0%81_%EB%85%BC%EB%A6%AC%ED%95%A9)