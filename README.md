# BAF-25-2-marketing_2
비어플 25년 2학기 마케팅 2팀  
생성한 데이터 파일 중 zip파일은 용량 및 정리의 용이성, 보안을 위해 해당 레포지토리에는 업로드 하지 않는다.

# File Tree
```bash
.
├── README.md
└── preprocessing
    ├── analysis
    │   ├── boxoffice_data.csv
    │   ├── movie_info_data.csv
    │   └── 분석용데이터생성.ipynb
    ├── calendar_dataset.csv
    ├── 휴일데이터.ipynb
    ├── 영화리뷰크롤링
    │   ├── cgv리뷰_전처리
    │   │   ├── 1.전처리파일통합.ipynb
    │   │   ├── 2.전처리.ipynb
    │   │   ├── 3.줄거리수집통합.ipynb
    │   │   └── 전처리파일저장
    │   │       ├── cgv_장르_줄거리_통합본.csv
    │   │       ├── cgv_원본_통합파일.csv
    │   │       └── cgv_전처리_통합파일.csv
    │   ├── 크롤링봇
    │   │   ├── cgv_줄거리.ipynb
    │   │   └── cgv_리뷰제외.ipynb
    │   └── 영화리뷰데이터_저장
    │       ├── cgv_장르_줄거리.zip
    │       └── cgv데이터.zip
    └── 영화관람객크롤링
        ├── 원본_박스오피스_데이터.csv
        ├── 최종_박스오피스_데이터.csv
        ├── 영화목록.csv
        ├── 엑셀데이터
        │   └── 박스오피스_원본엑셀데이터.zip
        ├── 일별박스오피스_전처리.ipynb
        ├── 일별박스오피스_영화별정리.ipynb
        ├── 주별박스오피스_엑셀파일추출.ipynb
        ├── 일별박스오피스데이터
        │   └── 박스오피스_일별분할데이터.zip
        └── 영화별박스오피스데이터
            └── 영화별_박스오피스_데이터.zip
```

# I. 초기 영화 박스오피스 데이터 수집과 전처리

### 박스오피스 데이터 추출
1. `preprocessing/영화관람객크롤링/주별박스오피스_엑셀파일추출.ipynb`  
"KOBIS 영화관입장권통합전산망"에서 "일별 박스오피스"를 추출함  
[KOBIS 일별박스오피스](https://www.kobis.or.kr/kobis/business/stat/boxs/findDailyBoxOfficeList.do)  
`동적 웹크롤링`을 이용하여 엑셀 파일 다운로드 from 2003-11-11 to 2025-09-06.  
그 결과물은 `zip`으로 압축하여 `preprocessing/영화관람객크롤링/엑셀데이터/박스오피스_원본엑셀데이터.zip`에 저장한다.  

2. `preprocessing/영화관람객크롤링/일별박스오피스_전처리.ipynb`  
`preprocessing/영화관람객크롤링/엑셀데이터/박스오피스_원본엑셀데이터.zip`의 데이터를 데이터 프레임으로 변환 후 일별로 분리하여 `csv`파일로 저장한다.    
해당 파일들은 `zip`으로 압축하여 `preprocessing/영화관람객크롤링/일별박스오피스데이터/박스오피스_일별분할데이터.zip`에 저장한다.  

3. `preprocessing/영화관람객크롤링/일별박스오피스_영화별정리.ipynb`  
`preprocessing/영화관람객크롤링/일별박스오피스데이터/박스오피스_일별분할데이터.zip`의 모든 파일을 하나의 파일로 통합한다. -> `preprocessing/영화관람객크롤링/원본_박스오피스_데이터.csv`  
이후 영화별로 일별 박스오피스 데이터로 나누어 `preprocessing/영화관람객크롤링/영화별박스오피스데이터/영화별_박스오피스_데이터.zip`에 저장한다.  
또한 여기서 분석에 사용할 영화 제목 리스트를 `preprocessing/영화관람객크롤링/영화목록.csv`에 저장한다.  
이것은 CGV검색 용으로 사용된다.  
마지막으로 최초 개봉, 재개봉 로직을 생성 후 `preprocessing/영화관람객크롤링/최종_박스오피스_데이터.csv`로 저장한다.

### CGV 영화 정보 크롤링
4. `preprocessing/영화리뷰크롤링/크롤링봇/cgv_리뷰제외.ipynb`  
동적 웹크롤링을 이용하여, `영화관람객크롤링/영화목록.csv`의 모든 영화를 CGV를 이용해 검색을 한다.  
영화의 평점과 감독 리스트 등등을 추출한다.  
각각의 영화에 대한 크롤링 결과는 `preprocessing/영화리뷰크롤링/영화리뷰데이터_저장/cgv데이터.zip`으로 저장한다.

5. `preprocessing/영화리뷰크롤링/cgv리뷰_전처리/1.전처리파일통합.ipynb`  
`preprocessing/영화리뷰크롤링/영화리뷰데이터_저장/cgv데이터.zip`의 데이터를 하나의 파일로 통합한다.  
`preprocessing/영화리뷰크롤링/cgv리뷰_전처리/전처리파일저장/cgv_원본_통합파일.csv`로 저장한다.    

6. `preprocessing/영화리뷰크롤링/cgv리뷰_전처리/2.전처리.ipynb`  
`preprocessing/영화리뷰크롤링/cgv리뷰_전처리/전처리파일저장/cgv_원본_통합파일.csv`를 전처리 진행한다.  
여기서 영화 제목, 감독과 배우 리스트만을 추출한다.
전처리 결과는 `preprocessing/영화리뷰크롤링/cgv리뷰_전처리/전처리파일저장/cgv_전처리_통합파일.csv`에 저장한다.    

7. `preprocessing/영화리뷰크롤링/크롤링봇/cgv_줄거리.ipynb`  
`preprocessing/영화리뷰크롤링/cgv리뷰_전처리/전처리파일저장/cgv_전처리_통합파일.csv`의 추출 가능한 영화 목록을 기준으로  
각 영화의 줄거리, 장르를 CGV 웹크롤링으로 추출한다.  
각각의 영화 파일은 `preprocessing/영화리뷰크롤링/영화리뷰데이터_저장/cgv_장르_줄거리.zip`로 저장한다.  

8. `preprocessing/영화리뷰크롤링/cgv리뷰_전처리/3.줄거리수집통합.ipynb`  
`preprocessing/영화리뷰크롤링/영화리뷰데이터_저장/cgv_장르_줄거리.zip`의 모든 영화를 하나의 파일로 통합한다.
그 결과를 `preprocessing/영화리뷰크롤링/cgv리뷰_전처리/전처리파일저장/cgv_장르_줄거리_통합본.csv`로 저장한다.

### 공휴일, 문화의 날 수집
9. `preprocessing/휴일데이터.ipynb`  
대한민국의 토요일, 일요일을 포함한 모든 '공휴일'을 수집한다.  
또한 영화관람표를 할인해주는 '문화의 날'도 수집한다. 
10. `preprocessing/calendar_dataset.csv`
`preprocessing/휴일데이터.ipynb`에서 수집한 데이터를 저장한 것이다.

### 배우 및 감독 필모그래피 수집  
11. `preprocessing/배우추출_api`  
해당 폴더에서는 KOFIC의 API를 이용하여 배우와 감독의 목록을 추출하였다.  
여기엔 각 인물의 출연 및 연출 영화 필모그래피가 포함되어있다.  
여러개의 분할 csv파일로 저장하였다.

# II. 분석용 데이터 전처리 및 EDA
### 분석용 데이터 생성
12.  `analysis/분석용데이터생성.ipynb`  
사용한 데이터 :  
- `preprocessing/영화관람객크롤링/최종_박스오피스_데이터.csv`  
- `preprocessing/영화리뷰크롤링/cgv리뷰_전처리/전처리파일저장/cgv_장르_줄거리_통합본.csv`  
- `preprocessing/영화리뷰크롤링/cgv리뷰_전처리/전처리파일저장/cgv_전처리_통합파일.csv`  
- `preprocessing/calendar_dataset.csv`  
이 데이터들을 전부 통합한다.  
그리고 `analysis/boxoffice_data.csv`와 `analysis/movie_info_data.csv`로 분리하여 저장한다.  

13. `analysis/boxoffice_data.csv`  

| 변수명 | 타입 | 설명 |
|---|---|---|
| Movie_Title | object | 영화 제목 |
| Release_Date | object | 최초 스크린 개봉일 (개봉 전 시사회는 제외) |
| Audience_Count | int64 | 일별 관객수 |
| Show_Count | int64 | 일별 상영횟수 |
| Week | int64 | 주차 구분<br>1주차 : 최초 개봉요일 ~ 그 주 일요일<br>2 ~ n주차 : 월요일 ~ 일요일<br>마지막 주차 : 월요일 ~ 마지막 요일 |
| Date | object | 박스오피스 집계 일자 |
| Holiday | int64 | 공휴일 구분<br>평일 : 0<br>주말, 공휴일 : 1 |
| Moonhwa | int64 | 문화의 날 구분<br>문화의 날이면 1, 아니면 0 |
| Pandemic | int64 | 코로나 팬데믹 구분<br>~ 2020년 1월 : 0<br>2020년 2월 ~ 2023년 5월 : 1<br>2023년 6월 ~ : 2 |
| now_showing | int64 | 데이터를 수집한 2025년 9월 6일 기준 상영영화 구분<br>상영중이면 1, 더이상 상영을 하지 않는다면 0 |
| Year | int64 | 박스오피스 집계 일자의 연도를 추출<br>연도별 티켓값의 상승 및 미묘한 심리 반영 |  

14. `analysis/movie_info_data.csv`  

| 변수명 | 타입 | 설명 |
|---|---|---|
| Movie_Title | object | 영화 제목 |
| Main_Country | object | 대표 영화 제작 국가<br>여러 국가에서 제작되어도 대표로 한 국가만 기입 |
| Grade | object | 영화 상영 등급<br>전체이용가, 12세이상관람가, 15세이상관람가, 청소년관람불가 |
| now_showing | int64 | 데이터를 수집한 2025년 9월 6일 기준 상영영화 구분<br>상영중이면 1, 더이상 상영을 하지 않는다면 0 |
| director1~5 | object | 영화 감독 목록 |
| actor1~6 | object | 배우 목록 |
| movie_summary | object | 영화 줄거리 (원본, 평문) |
| Distributor_1~8 | object | 영화 배급사 목록 |
| genre1~7 | object | 장르 목록<br>KOFIC과 CGV의 장르를 중복 제거 및 병합<br>(예 : 코미디, 드라마, SF, 액션 -> 하나의 영화에 네개의 장르) |  

15. `analysis/줄거리_임베딩.ipynb`  
`analysis/movie_info_data.csv`의 '영화 줄거리'에 임베딩 변환을 적용한다.  
모델은 hugging face에 공개되어있는 jina-embeddings-v3 모델을 사용한다
그 이유는  
-  상위권에 존재
-  Max Tokens값이 많아 줄거리와 같은 긴 글에 적합해보였다
-  10월 2일 기준 Zero-shot이 100%로 높았다
- 마트료시카 임베딩을 적용 -> 중요한 정보일수록 앞쪽 차원에 배치되어 임베딩 차원을 편히 선택할 수 있다.  

생성된 영화 줄거리 임베딩 데이터는 `analysis/movie_summary_embedding.csv`에 저장한다.  

16. `analysis/영화별_장르벡터.ipynb`  
`analysis/movie_info_data.csv`의 '장르'데이터를 이용하여 멀티핫 벡터를 생성한다.  
생성된 데이터는 `analysis/movie_genre_multi_hot.csv`에 저장한다.

### EDA
17. `analysis/EDA`  
해당 폴더 안에는 각 팀원들이 지금까지의 데이터를 가지고 EDA를 진행한 코드가 저장되어 있다.  
특히 `analysis/EDA/지승우.ipynb`에서는 배급사별로 유형을 구분하였다.  
구분은 대형과 소형, 흥행과 비흥행 총 네단계로 구분되어진다.  
해당 배급사 데이터는 `distributor_labels.csv`에 저장하였다.

# III. 모델 학습  
### 모델학습용 데이터 생성
18. `model/모델학습데이터생성.ipynb`  
`analysis`폴더에서 생성한 csv 데이터 전부를 사용한다  
- 이상치 영화 제거  
- 종속변수 -> 영화별 총 관객수, 상영주차, 상영일차
- 1, 2주차 평일, 공휴일 구분
- 영화별 팬데믹, 개봉일자, 개봉월, 개봉년도
- 영화별 배급사 카운트
- 영화별 상영 등급, 대표 국가
- 256차원 임베딩 벡터 -> 256개의 컬럼으로 분리
- 25.09.06기준 상영중인 영화 구분 -> `predict`
- 1만명 미만, 500만명 초과 영화 분리
- `train`. `test` 분리  

그 결과 다섯개의 데이터 생성  
`model/model_train_data.csv` : train dataset
`model/model_test_data.csv` : test dataset
`model/model_predict_data.csv` : predict dataset (25.09.06 기준 상영중인 영화, 최종 분석용)
`model/model_below_10k_data.csv` : 1만명 미만 영화 예측용 데이터셋
`model/model_upper_5M_data.csv` : 500만명 초과 영화 예측용 데이터셋  

각 데이터의 구조는 아래과 같다  
| 변수명 | 타입 | 설명 |
|---|---|---|
|Movie_Title|object|영화 이름|
|Total_Audience_Count|int64|총 관람객 수|
|Total_Show_Days|int64|총 상영일수 횟수|
|Total_Weeks|int64|총 상영 주차|
|wk1_Audience|float64|1주차 관객수|
|wk1_AudiencePerShow|float64|(1주차 관객수) / (1주차 상영횟수)|
|wk2_Audience|int64|2주차 관객수|
|wk2_AudiencePerShow|float64|(2주차 관객수) / (2주차 상영횟수) |
|Show_Change|float64|(2주차 상영횟수) / (1주차 상영횟수)|
|opening_Ho_Retention|float64|(2주차 휴일 일평균 관객수) / (1주차 휴일 일평균 관객수)|
|wk1_Holiday_AudienceMean|float64|1주차 공휴일 평균 관객수|
|wk1_Holiday_ShowMean|float64|1주차 공휴일 평균 상영횟수|
|wk2_Holiday_AudienceMean|float64|2주차 공휴일 평균 관객수|
|wk2_Holiday_ShowMean|float64|2주차 공휴일 평균 상영횟수|
|opening_AudienceStd|float64|초반_관객수표준편차|
|Year|int64|개봉연도|
|Month|int64|개봉월|
|Pandemic|int64|팬데믹 구분|
|dist_big_flop|int64|배급사 대형/비흥행|
|dist_big_hit|int64|배급사 대형/흥행|
|dist_small_flop|int64|배급사 소형/비흥행|
|dist_small_hit|int64|배급사 소형/흥행|
|Grade|object|영화 등급|
|Main_Country|object|영화 대표 국적|
|e1 ~ e256|float64|영화 줄거리 임베딩 256차원|  

19. `model/필모그래피벡터생성.ipynb`  
`analysis/movie_genre_multi_hot.csv`과 `preprocessing/배우추출_api`에서 추출한 모든 배우와 감독의 영화 필모그래피를 결합  
- 우선 각 배우, 감독이 연출한 영화의 모든 장르를 멀티 핫 인코딩 후 카운트 후 벡터화  
- 이것의 전체 합이 1이 되도록 L1정규화 
- 각 영화에 출연한 배우, 감독의 멀티 핫 인코딩 벡터를 합함
- 그리고 L1정규화 진행
- - `model/actor_genre.csv`  배우 필모그래피 장르 벡터
- - `model/director_genre.csv`  감독 필모그래피 장르 벡터

### 이진 분류
20. `model/이진분류/계층적이진분류_10k.ipynb`  
CatBoost와 LightGBM 머신러닝 모델을 사용하여 1만명 미만의 영화를 예측.  
즉 1만명 미만, 1만명 이상 500만명 이하, 500만명 초과의 영화 중에서 1만명 미만의 영화만 예측 후 제거한다.
- `model/이진분류/catboost_model_10k.cbm` : 최종 CatBoost 모델
- `model/이진분류/lightgbm_model_10k.txt` : 최종 LightGBM 모델

21.  `model/이진분류/이진분류_5m_모델사용x.ipynb`  
트리기반 앙상블 모델을 사용하지 않고 500만명 초과의 영화를 예측.  
즉 1만명 이상 500만명 이하, 500만명 초과의 영화 중에서 500만명 초과의 영화만 예측 후 제거한다.  
클러스터링 분석을 이용해 500만명 미만, 500만명 초과 초반 흥행 저조, 500만명 초과 초반 흥행 새 클래스로 구분 후 다중분류 진행  
최종적으로 SVM모델을 사용한다.  
- `model/이진분류/svm_scaler.joblib` : 표준화 스케일러 정보 저장 (`predict`데이터 변환 용도)
- `model/이진분류/pca_1.joblib` : 첫번째 주성분 변환 정보 저장 (`predict`데이터 변환 용도)
- `model/이진분류/pca_2.joblib` : 두번째 주성분 변환 정보 저장 (`predict`데이터 변환 용도)
- `model/이진분류/svm_model_5m.joblib` : svm 모델 저장 (`predict`데이터 변환 용도)

22. `model/이진분류/이진분류진행.ipynb`  
`predict`데이터로 1만명, 500만명 이진/다중 분류를 진행한 최종 예측 결과이다.

# IV. 영화 총 상영주차 예측
### 영화 흥행 유형(패턴)과 총 상영주차 예측을 위한 상관분석
23. `week_predict/영화흥행유형.ipynb`  
- 영화 흥행 유형(패턴)생성  
- FA분석  
- 영화 흥행 유형(패턴) 집단간 FA점수의 분포 차이 분석
- 총 상영주차와 변수 유의성 검정
- - `week_predict/full_data_for_week_predict.csv` : 총 상영주차 예측 모델용 `train`과 `test`데이터를 합친 것 (1만명 ~ 500만명 영화)  
- - `week_predict/fa_data_for_week_predict.csv` : 총 상영주차 예측 모델 생성용 데이터 (1만명 ~ 500만명 영화)  
- - `week_predict/movie_hit_category.csv` : 생성한 영화 흥행 유형(패턴) 저장  
- - `week_predict/standard_scaler_FA.pkl` : FA분석에 사용한 표준화 변환 정보 저장 (`predict`데이터 변환 용도)   
- - `week_predict/FA_model.pkl` : FA변환 정보 저장 (`predict`데이터 변환 용도)  