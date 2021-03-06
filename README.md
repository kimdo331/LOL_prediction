# LOL_prediction
League of Legends 게임의 12가지 데이터만으로 팀의 승패 여부를 판단하는 프로젝트

##  개요

처음에는 Genetic Algorithm으로 접근하였지만 정확도가 생각보다 낮았고, 나중에 Logistic Classification 기법을 배운 뒤에 그걸로 해봤는데 오류가 생겨서 오류를 수정하니 0.85정도의 accuracy를 보인다.

이 머신러닝 시스템을 실시간 경기에 적용한다면 팀의 우세정도를 실시간 수치로 나타낼 수도 있을 것이라고 본다.

-----------

## Logistic Classification

### 현재 상황

원래는 csv파일의 Y값이 1이었다.(승리한팀이 먼저 나온다는 뜻) 그래서 이를 랜덤하게 섞어 진팀이 먼저 나올수도 있게 하여 Y값이 1 또는 0이 되도록 하였다.

`min_max_scaler`는 `x_data`, `x_test`에만 적용해주었다. y값들은 매칭할 때 `min_max_scaler`를 적용하면 `0.999999`가 되어 `1.`과 다르다고 판별되기 때문.

이후에 입력 데이터를 더 늘리고 (챔피언 정보 등), 모델을 더 정교하게(logistic classification 말고 다른거 등) 한다면 더욱 높은 accuracy를 보일 수 있을 것이다.

### 참고자료

https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-05-2-logistic_regression_diabetes.py

https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-07-3-linear_regression_min_max.py

----------

## Genetic Algorithm

### Genetic Algorithm 이론

- 초기화
- 선택: 상위 일부를 뽑아냄
- 교차: 교배로 다음 세대 생성
- 변이: 돌연변이
- 대치: 새로운 세대로 바꿈
- 반복
- 종료

### step
0. 학습 데이터 크롤링 (예: 100개)
1. 데이터 가져오기 (어떤 방식으로 다룰건지)
2. 각 팀별 점수 생성, 실제 우승팀과 비교하여 살릴 개체 정하기
3. (선택 - 교차 - 변이 - 대치) 실행

### TODO LIST
- myHeader.cpp의 readGameData 함수에서 얼마 이상의 값을 읽으려고 하면 에러가 뜨는 문제 해결하기
- crawling에서 한 warp을 한번씩 값 가져오는게 아니라 모든 warp의 버튼을 클릭한 뒤에 값을 가져오는 방식으로 속도 개선하기
- 학습 모드, 예측 모드 각각 만들기


- 블루, 레드팀의 점수를 각각 생성한다. 모델은 [score = w_1\*x_1+...+w_6\*x_6] 로 하고  score가 큰 팀과 실제로 승리한 팀이 일치한 개체는 생존한다.
- 각 개체는 [w_1, w_2, .., w_6, b]으로 구성된다.


### 처음 생각한 내용
각 개체들은 주어진 값들 x_1 ~ x_6을 받아서 블루, 레드팀의 점수를 계산한다. 그리고 점수가 높은 팀이 승리할 것이라고 예측한다. 결과를 맞춘 횟수가 많은 순서대로 정렬하여 상위 일부만 생존한다.


- kill	  챔피언 처치
- gold  	골드 획득량
- deal  	챔피언에게 가한 피해량
- ward  	와드 설치
- damage	받은 피해량
- CS		  CS

--------------


