# Simple and scalable response prediction for display advertising 



## 1. INTRODUCTION
  - 본 논문은 광고모델에 관하여 click과 conversion 에 관한 상관관계를 분석하기 위해 머신러닝을 활용한 사례이다.
  - Maximum Entropy model(로지스터 회귀) 와  two-phase feature selection 알고리즘을 통해 관련현상에 관한 도메인의 전문지식도 낮추고 자동화를 쉽게 하였다.
  - 2장에서 선행 연구에 대한 탐구, 3장에서는 click과 conversion 현상에 대한 feature 분석, 4장에서는 Maximum Entropy model 과 hashing trick의 특징
    5장에서는 모델링 기법, 6장에서는 feature 그룹 선택과정, 7장에서는 본연구에서 사용했던 알고리즘, 8장에서는 효과적인 map-reduce 모델을 도출하고
    9장에서 그 결과를 정리하는 구성으로 되어 있다.



## 2. RELATED WORK
  - 로지스터 회귀 방식은 large scale의 문제를 병렬적으로 처리하는데 유리하여 선형모델을 평행화하여 처리할 시 처리속도를 20배 단축시킬수 있다.
  - 이전 연구들에서는 문제를 단순화하기 위해서(?)  advertiser 와 publisher에서 도출되는 feature를 계층적으로 구조로 만들어 이를 계산하는 factore를  log-linear function 로 추정하였다.
  - 하지만 본연구에서는 additional conjunction features를 통해 직접적으로 계층적 요소를 인코딩하였고, Tikhonov regularization with logistic regression 를 통해서 the effect of hierarchical smoothing 를 이끌어 냈다.
  - 또 이 데이터를 hasing을 통해 모델사이즈를 다루기 쉽게 하여 더 적은 전문지식에 대한 이해와 더 나은 스케일요소를 뽑아낼수 있었다.
  
  

## 3. DATA AND FEATURES

## 4. MODELING

## 5. MODELING RESULTS

## 6. FEATURE SELECTION

## 7. ON-STATIONARITY

## 8. LARGE SCALE LEARNING

## 9. CONCLUSION
