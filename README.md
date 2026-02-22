# Cookie Cats A/B Test 이탈률 분석
##### 분석 기간 : 2025.12 / 2026.02(추가분석)
## 프로젝트 개요
모바일 퍼즐 게임 Cookie Cats의 A/B 테스트 데이터를 활용하여  
초기 Gate(관문) 위치 변경이 유저 이탈률에 미치는 영향을 분석하였습니다.  

기존 레벨 30에 위치한 Gate를 레벨 40으로 이동시킨 실험을 기반으로,  
단순 평균 비교가 아닌 **통계적 가설 검정**을 통해  
유저 행동 변화의 유의성을 검증하는 것을 목표로 하였습니다.  

## 활용 데이터
Cookie Cats A/B Test Dataset  
https://www.kaggle.com/datasets/mursideyarkin/mobile-games-ab-testing-cookie-cats

## 데이터 구조
userid : 유저 고유 ID  
version : gate_30 (기존) / gate_40 (변경)  
sum_gamerounds : 설치 후 14일간 플레이 수  
retention_1 : 1일차 재접속 여부  
retention_7 : 7일차 재접속 여부  
총 90,189명의 유저 데이터로 구성  

## 데이터 분석
### 1. Gate 위치에 따른 7일차 유지율 비교
<img width="571" height="433" alt="output" src="https://github.com/user-attachments/assets/b76d7e03-9eaf-4874-ac4f-9e0422344f28" />  

gate_30과 gate_40의 7일차 유지율 차이 존재

단순 평균 비교를 넘어 통계적 검정 수행

##### Z-test 결과
z = 3.16  
p-value = 0.0016  
→ 1% 유의수준에서도 통계적으로 유의한 차이 확인  

즉, Gate 위치 변경이 단순 우연이 아니라  
실제로 유저 잔존에 영향을 미쳤을 가능성이 높음을 의미한다.

### 2. 1일차 유지 여부와 7일차 유지 관계
<img width="249" height="134" alt="스크린샷 2026-02-18 204226" src="https://github.com/user-attachments/assets/9e98730f-cde5-4276-80e9-1db96dd16c9a" />  

1일차 재접속 유저는  
미재접속 유저 대비 7일차 유지 확률이 약 4배 이상 높음  
→ 초기 플레이 경험이 장기 리텐션에 결정적 영향  

### 3. 플레이 성향별 분석 (Light / Mid / Heavy)
<img width="630" height="470" alt="pshml" src="https://github.com/user-attachments/assets/8047434d-b257-42c8-8ed0-820be8e15f2d" />  

Light 유저 → gate_30에서 유지율 높음  
Heavy 유저 → gate_40에서 영향 거의 없음  
Mid 유저 → 큰 차이 없음  

난이도 구조 변경은 모든 유저에게 동일하게 작용하지 않음  
특히 라이트 성향 유저가 초기 허들에 더 민감하게 반응  

## 핵심 결론
Gate 위치 변경은 7일차 유지율에 통계적으로 유의한 영향을 미쳤다.  
초기 재접속(D1)은 장기 유지(D7)의 강력한 선행 지표이다.  
난이도 상승은 헤비 유저보다 라이트 유저에게 더 큰 영향을 준다.  
초반 구간 설계는 단기 경험이 아닌 장기 리텐션 전략의 핵심 요소이다.  

## 신규 유저 관점 시사점

신규 유저는 아직 플레이 패턴이 형성되지 않은 상태이기 때문에  
초기 난이도 상승이나 관문 구조에 더 민감하게 반응할 가능성이 높다.  

따라서 초반 설계는 단순 난이도 조정이 아니라  
“장기 잔존 유저를 만드는 전환 구간” 으로 설계되어야 한다.  

## 한계점
- 14일 데이터만 존재하여 장기 LTV 분석 불가  
- 마케팅 유입 경로 정보 부재  
- 정교한 유저 행동 로그(세션 시간, 이탈 지점 등) 부족  

## 활용 기술
PySpark : 그룹 집계 및 분산 처리 환경 실습  
Python : 데이터 분석 및 가설 검정  
VScode / Jupyter Notebook : 분석 환경  


