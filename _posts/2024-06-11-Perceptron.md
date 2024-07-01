---
title: Perceptron의 이해
date: 2024-06-11 09:46:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Perceptron]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

# 1. Perceptron의 개념

Perceptron : Neural Network의 한 종류로 일종의 선형 분류기    
Input $x_1$, $x_2$를 가지고 가중치 $w_1$, $w_2$, bias $w_0$를 연산하여서 Output $y$를 도출한다.   
이 과정에서 $y$가 특정 수치를 기준으로 비교하여서 특정 값을 반환하는 것.   
ex) $y>0$ 이면 $y$ 반환 / $y<=0$ 이면 0 반환   
때문에 activation-function (= non-linear-function)과 같이 활용된다.

# 2. Perceptron의 구성 요소
Perceptron과 Neural의 모습을 비교해서 구성 요소를 살펴보면 다음과 같다.

| 구조   | Neural                | Perceptron        |
| :----- | --------------------- | ----------------- |
| 수용층 | 외부 자극 수용        | Input Data        |
| 연합층 | 가중을 입력 받아 전달 | Each Weight, Bias |
| 반응층 | 최종 출력             | Output Data       |

# 3. Perceptron의 문제점.

$$
\text{Perceptron} \rightarrow w_0 + w_1 \times x_1 + w_2 \times x_2 $$   

여러 논리 문제를 Perceptron을 통해서 해결할 수 있었으나 이는 선형 분리가 가능한 문제에 국한되었다.   
>이는 Perceptron은 다음과 같은 형태로 구성되고 결과 값을  **Activation Function** 을 통해서    
>**0** 또는 **1**로 출력하기 때문이다.
>때문에 Perceptron은 AND, OR 연산과 같은 선형 분리 문제에서만 사용될 수 있다.

즉, Perceptron은 [XOR](https://ko.wikipedia.org/wiki/%EB%B0%B0%ED%83%80%EC%A0%81_%EB%85%BC%EB%A6%AC%ED%95%A9) 과 같은 분류의 문제는 해결할 수 없다.
이를 해결하기 위해 생긴 것이 MLP, 즉 Multi-Layer Perceptron이다.

# 4. Multi-Layer Perceptron (MLP)

**관련 도표 추가 예정.**   

데이터 $x_1, x_2, x_3$에 대해서 Perceptron을 사용해서 Hidden Layer $z_1, z_2, z_3, z_4$로 연결한다.    
이렇게 연결된 부분 자체가 **Perceptron**이며, 이렇게 **Hidden Layer**와 **Input**을 연결하면서 점점 더 복잡한 연산을 진행하는 과정을
**Multi-Layer Perceptron / Neural Network** 라고 부른다.   

MLP 과정은 결국 하나의 Input data를 여러 Weight를 곱하는 것임으로 다음과 같다.   

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

# 5. 질문
가중치를 0으로 설정하는 것과 과적합 방지를 위한 drop out 기법을 하는 것은 완전히 다른 개념이다.    
때문에 가중치가 0이면 FC-Layer이나 drop-out을 통해서 길 자체를 끊는 것은 FC-layer로 볼 수 없다.


# 용어 정리 및 참고 사이트
- Fully-Connected Layer : Hidden Layer 끼리 모든 Perceptron과 Perceptron이 모두 연결된 상태
- Drop-out : Overfitting을 방지하기 위해 특정 노드를 학습시키지 않고 삭제하는 것

[Neural Network Play Ground](https://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.95560&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)   
[위키피디아 Perceptron](https://ko.wikipedia.org/wiki/%ED%8D%BC%EC%85%89%ED%8A%B8%EB%A1%A0)   
[위키피디아 베타적 논리합](https://ko.wikipedia.org/wiki/%EB%B0%B0%ED%83%80%EC%A0%81_%EB%85%BC%EB%A6%AC%ED%95%A9)