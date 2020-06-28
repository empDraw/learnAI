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
 - Yahoo의 Right Media Exchange 트래픽 로그를 통해 network-of-networks model 의 데이터를 분석하였다.
 - 본 연구의 주요 이벤트는 클릭율(CTR) 과 전환율(CVR)이며, advertiser, publisher, user, time 이 주요 도메인이다.
 ---
 - 클릭이벤트과 전환(머뭄) 현상 (PCC) 에 대한 보다 정확한 이벤트 도출을 위해 전환이벤트에 대한 time delay 을 분석하였고, 
 - 10분 이내가 전체 이벤트의 86.7 %,  한시간 이내는 95.5 % , 2일 이내는 98.5% 를 차지하였다.
 - 너무 적은 데이터 샘플링은 부정확한 결과를 도출할 수 있고, 너무 많은 데이터는 실용성이 떨어 질 수 있기 때문에 적절한 범위 선택이 필요하다.

 

## 4. MODELING
  - 모델링의 데이터셋들은 Category 형이며, 로지스터 회귀(Maximum Entropy model) 를 통해 분석하였다(?)
  - 하지만 데이터셋들이 너무 많은 cardinality 를 가지고 있을 경우 차원이 커져 분류가 어려울수 있기 때문에 Hasing 을 통해 숫자를 줄이는 작업을 진행했다.
  - 같은 bin에서 오는 충돌을 막기 위해 Bloom filter 를 이용한 Collision analysis를 시도하였다 ( 하지만 별 영향도는 없었다? )
  - 또 matrix factorization 를 이용한 low-dimensional representation도 Hasing으로 생길수 있는 문제( 변수가 축소됨에 따라 생기는 충돌) 해결 하는데 도움이 되지만 본연구에서는 다루지 않았다?
  - Multi-task learning 을 통해서 특정 multi-task solver 없이 하나의 모델에서도 작업이 가능(비용도 절감?)했다.
  - Subsampling 과정에서는 negatives samples를 통해 정확도를 높였고(?)  Regularization 과 로지스터 회귀의 결합으로 hierarchical smoothing를 이끌어 낼수 있었다.
  

## 5. MODELING RESULTS
  - 모델링의 결과는 **negative log likelihood (NLL), root mean squared error (RMSE), area under the precision / recall curve(auPRC), area under the ROC curve (auROC)** 로 평가하였다.
  - 중요한 Feature를 도출하기 위해서 hasing을 통해 차원을 축소하여 인코딩하였고, 결과값을 배열이 아닌 Map(dictionary - key-value) 로 저장하였다.
  - 큰 규모의 학습세트를 다루기 위해 subsample 을 활용하였고, 본 연구에서는 1%의 subsample이 정확도와 훈련시간이 적절하게 나오는 절충점이였다.
  - feedback 모델은 잘못된 signal을 전달 할 수 있으나 기존모델을 업데이트 하는 것보다 비용이 비쌀때 유용하다.
  -- (Comparison with a hierarchical model 부분은 해석이 잘 안되어 추후 보충예정 )
  -

## 6. FEATURE SELECTION

## 7. ON-STATIONARITY

## 8. LARGE SCALE LEARNING

## 9. CONCLUSION
