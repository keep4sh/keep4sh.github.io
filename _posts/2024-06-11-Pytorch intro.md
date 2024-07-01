---
title: Pytorch Intro
date: 2024-06-11 14:09:00 +09:00
categories: [AI, Deep Learning, Pytorch]
tags: [AI, ML, Deep Learning, Deeplearning, DeepLearnging, Study, Yeardream, Pytorch]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

# 1. Pytorch 소개

Pytorch는 메타에서 개발한 인공지능을 위한 오픈소스 프레임 워크이다.   
쉽게 생각해 GPU를 사용가능한 Numpy라고 생각하면 편하게 접근할 수 있을 것이다.   
또한 직관적인 코드를 구조를 사용한다. 디버깅 측면에서도 아주 용이하다.   
이러한 장점으로 인해 세계적으로도 많은 인구가 Tensor Flow에서 점점 Pytorch로 넘어오고 있다.   
사용자가 많아 지면서 커뮤니티가 크다는 것 또한 큰 장점으로 볼 수 있다.  

### 참고 커뮤니티 및 Docs
[Stack Overflow](https://stackoverflow.com/)   
[PyTorch Documentation](https://pytorch.org/docs/stable/index.html)이다.

# 2. Tensor 생성 방법
torch.rand(*size)