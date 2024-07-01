---
title: Softmax Classifier and Logistic Regression
date: 2024-06-11 11:29:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Softmax, Logistic]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

# 1. MSE와 Sigmoid를 통한 Classifier의 문제점

# 2. Softmax Layer 와 Softmax Loss 계산
Data를 Weight를 통과하면서 나온 Output은 각각 하나의 숫자 값을 지니지만 유의마한 값들은 아니다.   
이러한 출력 벡터를 합이 **1**인 형태의 확률 분포로 변환한 것을 Softmax Layer라고 부른다.   

Logit Vector (이전 Layer의 출력 값, Softmax Layer의 입력값)을 지수함수를 적용.   
- 지수함수를 사용하는 것은 지수 함수가 단조 증가 함수 이기 때문임.   
해당 값들의 합에 대한 각 값의 상대적 크기 = 확률   

# 3. Softmax Loss와 Cross Entropy, 그리고 KL Divergence
Softmax Layer에서 최적으로 나오는 값은 벡터의 원소 중 하나만 1, 나머지는 0으로 나올 때 가장 이상적이다.   
이를 Target이라고 표현할 수 있으며 Softmax Layer의 값들이 최대한 Target과 닮아야 한다.   
즉, Target - Softmax Layer 가 최소가 되는 것이 우리의 Objective Function이 되는 것    
   
그렇다면 이러한 두 확률 분포를 최소화 하기 위한 방법으로는 

# 4. Logistic Regression과 Softmax classifer의 관계
