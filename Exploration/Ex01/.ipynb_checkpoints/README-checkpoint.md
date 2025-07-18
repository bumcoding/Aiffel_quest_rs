# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 박범찬
- 리뷰어 : ?


# PRT(Peer Review Template)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
        - 중요! 해당 조건을 만족하는 부분을 캡쳐해 근거로 첨부
    
- [ ]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 해당 코드 블럭을 왜 핵심적이라고 생각하는지 확인
    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
    - 해당 코드의 기능, 존재 이유, 작동 원리 등을 기술했는지 확인
    - 주석을 보고 코드 이해가 잘 되었는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인
    - 프로젝트 평가 기준에 더해 추가적으로 수행한 나만의 시도, 
    실험이 기록되어 있는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        
- [ ]  **4. 회고를 잘 작성했나요?**
    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        
- [x]  **5. 코드가 간결하고 효율적인가요?**
    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화/모듈화했는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부


# 회고(참고 링크 및 코드 개선)

- project1(Diabetes)

목표 : MSE를 3000 이하로 낮추기!
시도
- [x] LearningRate값 조정 (0.001 -> 0.01)
    - MSE가 크게 줄어듦 (5376 -> 4710)
- [x] 특성 스케일링 추가 (train과 test에 동일한 평균, 표준편차 적용 (평균 0, 표준편차 1))
    - MSE를 3000 이하로 낮춤 (4710 -> 2885)

- project2(Bike)

목표 : RMSE를 150 이하로 낮추기!
시도
- [ ] features의 변수 추가 ('atemp'를 추가했음)
    - RMSE가 큰 의미없이 줄어듦 (약 0.01정도)
- [ ] LinearRegression 대신 Ridge 회귀 사용
    - RMSE가 역시 큰 의미없이 변동 X
- [x] RandomForestRegressor(트리 기반 앙상블 회귀) 사용
    - RMSE가 약 1/2정도 큰 폭으로 줄어들고 예측 시각화도 크게 발전 (141 -> 79)

[출처] https://everyday-joyful.tistory.com/entry/앙상블-RandomForestRegressor