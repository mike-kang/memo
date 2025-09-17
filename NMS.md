## 목적
중복제거

## 방법
각 class별로 동작
  score가 threshold 보다 작은 것을 제거한다.
  
  가장 스코어가 높은 박스를 찾아, IOU가 threshold보다 큰 것은 제거한다.
  남은 박스 중에서 이 과정을 반복한다.


