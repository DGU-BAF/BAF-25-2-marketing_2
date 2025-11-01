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
1. `preprocessing/휴일데이터.ipynb`  
대한민국의 토요일, 일요일을 포함한 모든 '공휴일'을 수집한다.  
또한 영화관람표를 할인해주는 '문화의 날'도 수집한다. 
2. `preprocessing/calendar_dataset.csv`
`preprocessing/휴일데이터.ipynb`에서 수집한 데이터를 저장한 것이다.

### 분석용 데이터 전처리
Make final dataset for **analysis**.  
1. `분석용데이터생성.ipynb`  
It use `최종_박스오피스_데이터.csv`, `cgv_장르_줄거리_통합본.csv`, `cgv_전처리_통합파일.csv` and `calendar_dataset.csv`.  
Then split `boxoffice_data.csv` and `movie_info_data.csv`.  

2. `boxoffice_data.csv`  

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

3. `movie_info_data.csv`  

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