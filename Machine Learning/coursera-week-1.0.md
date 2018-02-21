# Supervised Learning (지도 학습)

우리가 알고리즘에게 정확한 답을 알고있는 데이터(data set)를 준다는데서 유래한다.

## Supervised learning problems

* regression problem: f(x) = n. 어떤 연속적인 속성 값을 예측하는 문제
* classification problem: True/False. 이산적(연속적의 반대말)인 결과값을 예측하는 문제

## **Regression** 문제의 예

* 집의 평수에 따라 가격을 예측하고자 하는 문제
* 특정인물의 사진이 주어졌을때, 그의 나이를 예측해야 하는 경우
* 대량의 동일한 제품들을 3 개월 안에 얼마나 팔 수 있을지 예측하려 하는 경우

## **Classification** 문제의 예

* 특정한 가격에 많이 팔리는지 적게팔리는지
* 특정 환자의 종양이 양성인지 악성인지
* 개인 고객들의 계정이 해킹에 의해 유출되었는지 안되었는지 관찰하기위한 소프트웨어를 개발하려하는 경우

### 예

* 스팸/스팸아님 라벨이 붙여진 이메일 데이터가 주어진 상황에서의 스팸필터를 학습
* 당뇨병이 유무를 알 수 있는 환자데이터를 이용하여 새로운 환자가 당뇨병이 있는지 없는지 학습

# Unsupervised Learning (비지도 학습)

어떤 데이터가 주어지지만 어떤 라벨도 붙어있지 않거나 동일한 라벨이 붙어있는 경우이며, 그 데이터가 어떤 의미가 있는지 조차 모르는 상황에서 특정한 구조를 찾는 작업이다.

### 예

* 구글뉴스: 유사한 뉴스를 그룹화하여 분류
* Organize computing clusters
* Social network analysis
* Market segmentation
* Astronomical data analysis
* Clustering
* Non-clustering

## 참고

* [조대협님의 블로그](http://bcho.tistory.com/966)
