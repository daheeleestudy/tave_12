# 데이콘 대구 교통사고 피해 예측 AI 경진 대회
https://dacon.io/competitions/official/236193/overview/description
1. 팀으로 참여하였지만 본인 기여율 99% 
2. 결과: public score 0.42708 (113등/943등) private score 0.42741 (90등/943등,  대략 상위 10% 안)

# 후기
1. 독립변수와 종속변수 사이 correlation이 매우 작아 중대한 영향을 끼치는 컬럼을 알기 어려웠음
2. train과 test 의 컬럼 불일치성이 많아 서로 일치하는 컬에서 파생변수 생성 및 외부데이터 활용함
3. 대회 종료 후 외부데이터 여러개 merge한거 submission 해봤는데 public에서는 0.42740(최종 제출한 스코어보다 낮음) 나왔으나 private에서 0.4269로 가장 높은 점수 나옴
4. 최종 private score 보다 높게 책정된 분석파일들을 같이 업로드함
 

![image](https://github.com/daheeleestudy/tave_12/assets/139957707/7f9d12a7-15e5-4bf6-bbac-4c232ddd0ba6)

# preprocessing (모든 파일 공통)
1. train data
![image](https://github.com/daheeleestudy/tave_12/assets/139957707/5fb3585a-0ce5-4dd8-8372-cc087450a1ca)
2. 가해운전자 연령 -> numeric 전환, null값과 미분류값 결측값 대체, 98세 이상 -> 98로 대체 
3. 데이터 행 제거 
- 법적인 운전가능 나이만 추출해서 scoring 했지만 낮은 성능 보임, 주석처리함
- 상식적인(?) 피해운전자 연령 2세 이하 제거했으나 낮은 성능 보임
- 가장높은 eclo 수치 (outlier처럼 보이는) 제거하면 성능 안좋아짐
- 결론 : 가해운전자 연령 10세 미만 '만' 제거 
4. train test data 컬럼 일치
5. 시군구 -> 도시/구/동으로 split
6. 도로형태 -> 도로형태1, 도로형태2로 split
7. 사고일시 -> datetime 전환 및 year/month/day/hour로 split
8. train data에만 있는 동 컬럼 -> 최빈값 동으로 대체
9. train data에만 있는 기상상태 컬럼 -> 최빈값 기상상태 대체
10. hour이 5~10은 출근시간, 11~17은 낮시간 17~23은 퇴근시간 나머지는 새벽시간으로 파생변수 생성
11. 빨간날(대체공휴일 포함)+ 주말 -> 공휴일 , 아닌날은 평일로 라벨링
12. 
 


# 외부데이터 결합 


# modeling
1. automl = AutoML(mode="Compete",algorithms = [ 'Random Forest', 'LightGBM', 'Xgboost'], n_jobs = -1,total_time_limit=2400, eval_metric="rmse", ml_task = "regression") 사용

# 느낀점
1. 첫 머신러닝 대회 출전. 처음 모델링 했을때 0.47- 0.48 나옴. 
2. 중간에 피드백 받아서 날씨별 데이터 분할 후, 가장 잘나온 모델 각각 돌려보고 파라미터 설정까지 했을 때 0.442 까지 떨어짐
3. 외부데이터 추가 결합 + autoML 돌리니 0.42대까지 떨어짐. 이게 정답(?) 이었다
4. autoML pycaret 돌려보고 싶었으나 시간문제로 하지 못함

# 추후 발전을 위해 보완할 점 
