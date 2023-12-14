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


# 외부데이터 결합 


# modeling
1. automl = AutoML(mode="Compete",algorithms = [ 'Random Forest', 'LightGBM', 'Xgboost'], n_jobs = -1,total_time_limit=2400, eval_metric="rmse", ml_task = "regression") 사용

# 느낀점
1. 첫 머신러닝 대회 출전. 처음 모델링 했을때 0.47 나왔는

# 추후 발전을 위해 보완할 점 
