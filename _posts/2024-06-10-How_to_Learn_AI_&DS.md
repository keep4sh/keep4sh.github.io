---
title: How to learn AI and DS (1) Fundamentals of Machine Learning and Essential Mathematics
date: 2024-06-10 09:00:42 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

# **조원국 멘토님 AI & DS 강의**   
  
---
# 0. Intro with Glossary
## What is Artificial Intelligence?    

### AI, in its broadst sense, is intelligence exhibited by machines, particularly compuuter systems.

1. Rule-based System   
    Data를 Rule에 따라서 Decision을 만드는 System.   
    e.g.) 
2. Learning-based System   
    Large DataSet을 가지고 HardWare에서 Learning을 진행,   
    스스로 Rule을 만들어 Decision을 만드는 것.   
    e.g.)

**AGI(강인공지능)** 이 될 수록 Learning-Based가 강해지지만, 현재 우리의 단계에선 일정 부분 Rule-Based를 사용할 수 밖에 없다.

## So, What is Machine Learning?

### "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

이게 무슨 소리인지 하나씩 용어 정리 해보자.

**T : Task**
- Goal to learning   
- What mode is expected to perform

**E : Experience**
- Process of examining data
- Supervised learning, un/self supervised learning, semi-supervised learning, reinforcement learning, etc ....

**P : Performance Measure**
- Absolute / squared error for regression
- Accuracy for classicition
- Intersection-over-union for segmentation   
   
정리해보자면,    
컴퓨터가 데이터를 보고 계산하면서 특정 행동을 수행하고, 수행을 평가하는 평가지표를 측정할 수 있으며,    
이를 점점 발전시켜 나갈 때 Artificial Intelligence라고 이야기한다.

---
**Machine Learning**   
Model + Learning Rule

> 그럼 Random Foreset를 설명해보자.
> Decision Tree + Ensemble 기반의 모델을 가지고 Bagging 사용??

**Deep Learning**   
Neural Network + Gradient Descent Optimization


# 1. Data
  1. 차원에 대한 설명 (검증 필요)   
        $x\in \mathbb{R}^d \underset{\text{이 수식은 x가 d차원 공간 상에서의 어떤 한 점을 표현하는 것}}{}$   
        만약 $x\in \mathbb{R}^2$라면 $x = \begin{matrix}x_{1} \\ x_{2} \\ \end{matrix}$   

        ML에서의 차원 : Data set의 Feature의 갯수   
        DL에서 차원 : 각각의 Data(?)

  2. Distribution of Data   
        (histogram을 가지고 정규분포를 그림)    
        데이터 __*Input : x*__ 는 확률분포를 갖게 됨  
        


        $x \sim P(x)$
        > 이러한 확률 분포는 $P(x)$이며 특정 $x_1$에 대해서 $\hat{P(x_1)}$ 처럼 표현한다.
        이러한 $\hat{P(x_1)}$ 을 무수히 많이 뽑는다면 $P(x)$와 계속해서 유사해질 것이다.
        

        이미지 데이터는 픽셀의 크기에 따라서 차원이 결정됨    
        e.g.) 28*28 = 784의 픽셀 => $x\in \mathbb{R}^784$   
        프레임 단위로 영상에서 무엇을 검출하고 이를 추적하면 어떠할까?   
        => 사람 얼굴에서의 분포 / 등을 알고 있으면 이미지 생성 모델을 하는 것.
  3. Mathematical Notation of Dataset

<p align="center">
        $
        \mathcal{D}_\tau \rightarrow \mathcal{D}\tau^\text{train} \text{ and } \mathcal{D}\tau^\text{valid}$

      
        $
        x^{(i)} \in \mathbb{R}^m, \; y^{(i)} \in \mathbb{R}^n, \; \forall i$
</p>




# 2. Neural Network
## Matrix Operations
1. Vector의 사칙연산   
<p align = "center">
$
x = \begin{bmatrix}x1&x2 \\\ x3&x4 \end{bmatrix}$   
$y = \begin{bmatrix}y1 & y2 \\\ y3 & y4 \end{bmatrix}$
</p>

1. 벡터의 합  
$x+y \rightarrow \begin{bmatrix}x1+y1 & x2+y2 \\\ x3+y3 & x4+y4\end{bmatrix}$
2. 벡터의 곱   
$x*y \rightarrow\begin{bmatrix}x1y1 + x2y3 & x1y2 + x2y4 \\\ x3y1 + x4y3 & x3y2 + x4y4 \end{bmatrix}$


## Function
<p align="center">

$x \rightarrow f(x)=x^2$
</p>

$f(x)=x^2$ 와 같이 Input : $x$에 대해서 연산 : $f(x)$를 진행하여서 Output : $x^2$를 도출하는 것

모델도 이와 같다.
<p align="center">

$\text{Input data : }x \rightarrow \text{Model : }f_\theta(x) \rightarrow \text{Predict : } \hat{y}$
</p>
이렇게 뽑아 놓은 $\text{Predict : } \hat{y}$ 를 $\text{Label : } y$과 유사하게 만드는 방법을 찾아가는 것!

## Neural Networks는 무엇인가? (아래 내용은 반드시 찾아볼 것.)
신경망처럼 구성된 모습

- Activation Function
- Feed Foward Network

그렇다면 ML과 DL의 차이점, 각자의 장/단점에 대해서 설명해보자.

# 3. Optimization (최적화)
$\text{Loss Function}$ : $\hat{y}$와 $y$가 얼마나 가까워 졌는지 평가하는 함수
MSE (Mean Squared Error)



Input Layer -> Hidden Layer -> Output Layer 처럼 Network가 움직이는 것?