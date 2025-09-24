# BAF-25-2-marketing_2
비어플 25년 2학기 마케팅 2팀


# Extract Analysis Data
All courses are saved in a `preprocessing` folder.

## I. `영화관람객크롤링` folder
1. `주별박스오피스_엑셀파일추출.ipynb`  
"일별 박스오피스" of "KOBIS 영화관입장권통합전산망".  
https://www.kobis.or.kr/kobis/business/stat/boxs/findDailyBoxOfficeList.do  
Download every Excel data from 2003-11-11 to 2025-09-06.  
By using **Dynamic Web Crawling**  
Save raw files in `엑셀데이터` folder. This is compressed - `박스오피스_원본엑셀데이터.zip`.  
2. `일별박스오피스_전처리.ipynb`  
Decompress every Excel data and save daily files by csv.  
Save daily files in `일별박스오피스데이터` folder. This is compressed - `박스오피스_일별분할데이터.zip`.  
3. `일별박스오피스_영화별정리.ipynb`  
Collect all daily files(`원본_박스오피스_데이터.csv`) and save box office data by movie in   `영화별박스오피스데이터` folder. This is compressed - `영화별_박스오피스_데이터.zip`.  
The reason for doing this is to add the date of each movie.  
And extract the movie list. (`영화목록.csv`) It is used as a criterion for searching for movies on CGV.  

## II. `영화리뷰크롤링` folder
1. `크롤링봇/cgv_리뷰제외.ipynb`  
Extract movie ratings, actor list, etc. through cgv web crawling based on movie list `영화목록`.csv`.  
Save in `영화리뷰데이터_저장/cgv데이터` folder by csv for each movie (Compressed by zip).  
2. `크롤링봇/cgv_줄거리.ipynb`  
Extract movie summary, genres through cgv web crawling based on movie list `영화목록`.  
Save in `영화리뷰데이터_저장/cgv_장르_줄거리` folder by csv for each movie (Compressed by zip).  
3. `cgv리뷰_전처리/1.전처리파일통합.ipynb`  
Collect all movie information data extract from cgv. (`영화리뷰데이터_저장/cgv데이터`)  
Save in `cgv리뷰_전처리/전처리파일저장/cgv_원본_통합파일.csv`.  
4. `cgv리뷰_전처리/2.전처리.ipynb`  
Preprocess `cgv_원본_통합파일.csv`.  
We only use movie title, actor list, director list from this.  
And save in `cgv리뷰_전처리/전처리파일저장/cgv_전처리_통합파일.csv`.  
5. `cgv리뷰_전처리/3.줄거리수집통합.ipynb`  
Collect all movie genre and summary data extract from cgv. (`영화리뷰데이터_저장/cgv_장르_줄거리`)  
And collect for all movies, preprocess, save in one csv file in `cgv리뷰_전처리/전처리파일저장/cgv_장르_줄거리_통합본.csv`.

## III. route folder
1. `휴일데이터.ipynb`  
Collect every S.Korea' Holiday dates, including Sat. and Sun.  
And collect `문화의 날`, the day when movie tickets are discounted.  

## IV. `analysis` folder
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