---
title: 배구 승률 예측하기 프로젝트
date: 2024-06-10 16:00:30 +09:00
categories: [AI, Deep Learning]
tags: [AI, ML, Machine Learning, Machinelearning, MachineLearnging, Study]		# TAG는 반드시 소문자로 이루어져야함!
use_math: true
---

# 1. Topic
1. Issue
   1. 경기 승패 예측
      1. 팀 단위가 아닌 선수 단위 예측 => 선수가 경기에 미치는 영향을 기준으로 하여서 예측
      2. 승패를 나누는 기준 자체를 어떻게 봐야할 지 설정 필요
         1. 개별 선수들의 승리 기여도 합산 [공격수 / 수비수 , 각 포지션 별로 보정치를 갖고 / 최근 다섯 경기에 대한 가중치]
   2. 공간 데이터를 구해서 이를 활용하는 방식
   3. DE 쪽 Issue
      1. DB 사용 관련
         1. 어떤 DB 사용이 중요한가
            - 여자 경기 관련 CSV 7MB.
            - 남자 경기 포함 20MB 정도 예상.
   4. DS 쪽 Issue
      1. 승리 기여도 지표 작성 필요
      2. 크롤링 관련 소요가 많이들 예정.
   


2. 과정 관련 
   1. 크롤링 (CSV)
      1. 남 / 여 모두 진행
   2. EDA 확인 (Na값 확인 / Outlier 확인 수준)
   3. 전처리 실시
   4. 문헌 조사 시행 (배구 포함 종목별 선수 평가 / 승패 예측 관련 기준)
      1. 평가 지표 작성
   5.  DB 적재
   6.  Model Test
   7.  Model 자동화