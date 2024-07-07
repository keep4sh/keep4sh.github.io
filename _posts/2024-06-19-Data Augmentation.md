---
title: Data Augmentation
date: 2024-06-19 13:00:00 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Data Augmentation]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---
지난 포스팅에서 Drop Out에 대해서 포스팅했었다. <br>이번 포스팅에서는 Data Augmentation이다.

<p align=center>주요 개념</p>
> Data augmentation (자료 증식)<br>
> Crop, Translation, Rotation, Stretching, Brightness<br>
> Mixup, Cutout, CutMix   

# 1. Overfitting 문제
우리가 모델을 학습 시킬 떄 생기는 문제 중 하나는우리의 학습 데이터에만 너무 잘 학습을 진행한 경우가 발생한다. 즉 학습의 Loss는 줄어들지만 Validation의 Loss가 줄지 않는 상황이다. 이를 우리는 **Overfitting** 이라고 기억한다. 
Overfitting이 일어나는 근본적인 이유는 모델 크기와 데이터의 크기가 잘 맞지 않아서 생기는 문제이다.

모델의 크기 관련으로 이를 해결하기 위해서는 모델의 크기를 줄이는 것이다. 즉 Layer의 수를 줄여나가는 것. 혹은 우리가 지난 포스팅에서 작성한 Regularization이다. 데이터를 정규화를 통해 학습하는 범위를 줄이는 것이다.

데이터와 관련해서 해결 방안은 Data의 크기를, 수를 올려나가는 것이다. 데이터의 원래 의미를 가지고 있으면서 데이터를 늘린 방식이 필요한 것이다. Mnist Data Set에서 숫자 데이터의 이미지 상에서의 위치를 옮기거나, 언어 Data와 관련해서는 어순을 변경하는 등의 방식을 갔는 것이다.

# 2. Data Augmentation
위 해결 방안 중 Data와 관련된 방안이 Data Augmentation이다. 굉장히 다양한 Augmentaiton 방식이 있으며 오늘은 Computer Vision 주제에서의 Augmentation을 통해서 알아보겠다.

1. Crop
    이미지 데이터에서 일정 부분(유의미한 의미를 갖는 부분, ex: 고양이 사진에서의 고양이 얼굴 부분)만 잘라내서 데이터를 만드는 방식
2. Translation
    이미지 데이터를 이미지 상에서 위치를 조정해주는 방식 (ex : 고양이 얼굴을 사진의 가장자리, 혹은 모서리로 옮기는 방식)
3. Rotation
    이미지를 회전 시키는 방식
4. Stretching
    이미지를 임의로 늘려서 사용하는 방식.
5. Brightness
    이미지의 밝기를 조정하여서 학습 시키는 방식.


위 5가지 방식은 학습을 시행 시킨 후 성능을 최대한 끌어 올리기 위해서 사용하지 현재는 초기에 사용하지는 않는다고 한다.

# 3. Advanced Augmentaion

이미지 데이터에서 보다 발전된 Augmentaion은 다음과 같다.
강아지의 이미지를 예시로 들어본다.

|Method|Explain|Label|
|Origin|원본 데이터|강아지 1.0|
|Mix-Up|두 이미지가 희미하게 겹쳐 보이게 만듬| 강아지 0.5 / 고양이 0.5|
|Cutout|이미지의 일정 부분을 아예 가려서 학습 시키는 방식| 강아지 0.6|
|CutMix|이미지의 일정 부분을 새로운 다른 의미의 이미지로 대체하는 방식| 강아지 0.6 / 고양이 0.4|


# 4. 음성 데이터
위 예시로서는 이미지 데이터에 대해서 Data Augmentation을 알아 보았다. 언어 데이터 관련해서도 어순 혹은 비슷한 의미의 다른 단어 등 다양하게 활용 방식이 직관적으로 머리에 떠오른다. 그렇다면 Audio Data 와 관련해서는 어떻게 사용될까??

http://arxiv.org/pdf/1904.08779
