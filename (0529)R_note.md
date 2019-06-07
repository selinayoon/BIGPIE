3일차 (05/29) - R실습

### Section02. 모수와 통계량

#### 최대값과 최소값

```R
ranicafe <- read.csv("C:/Users/student/Documents/StatWithR/BIGPIE/(0529)Form_of_data2/data/cafedata.csv", header=T, na.strings="na", stringsAsFactors=FALSE )
ranicafe <- na.omit(ranicafe)
str(ranicafe)

# 커피 판매량만 불러오기
ranicafe$Coffees

# sort함수를 사용해 오름차순으로 정렬
sort(ranicafe$Coffees)

# 최솟값
sort(ranicafe$Coffees)[1]

# 내림차순으로 정렬, 최댓값
sort(ranicafe$Coffees, decreasing=TRUE)
sort(ranicafe$Coffees, decreasing=TRUE)[1]

# min(), max() 함수 사용해서 구하기
min(ranicafe$Coffees)
max(ranicafe$Coffees)
```

```R
> ranicafe <- read.csv("C:/Users/student/Documents/StatWithR/BIGPIE/(0529)Form_of_data2/data/cafedata.csv", header=T, na.strings="na", stringsAsFactors=FALSE )
> ranicafe <- na.omit(ranicafe)
> str(ranicafe)
'data.frame':	47 obs. of  22 variables:
 $ t                        : int  1 2 3 4 5 6 7 8 9 10 ...
 $ Date                     : chr  "2010-01-19" "2010-01-20" "2010-01-21" "2010-01-22" ...
 $ Day.Code                 : int  2 3 4 5 1 2 3 4 5 1 ...
 $ Day.of.Week              : chr  "Tue" "Wed" "Thu" "Fri" ...
 $ Bread.Sand.Sold          : int  5 6 8 4 3 7 6 0 3 2 ...
 $ Bread.Sand.Waste         : int  3 8 2 2 0 1 6 0 4 6 ...
 $ Wraps.Sold               : int  25 7 14 5 10 5 19 7 4 13 ...
 $ Wraps.Waste              : int  5 17 0 7 0 3 3 0 9 3 ...
 $ Muffins.Sold             : int  5 3 4 5 8 1 6 6 0 3 ...
 $ Muffins.Waste            : int  1 5 0 0 0 0 0 1 4 0 ...
 $ Cookies.Sold             : int  5 1 1 3 3 5 10 0 3 6 ...
 $ Cookies.Waste            : int  3 6 0 1 0 0 0 0 2 0 ...
 $ Fruit.Cup.Sold           : int  1 0 0 3 2 2 2 0 1 2 ...
 $ Fruit.Cup.Waste          : int  4 3 3 0 0 0 0 0 1 0 ...
 $ Chips                    : int  12 0 0 20 0 4 2 20 3 16 ...
 $ Juices                   : int  8 0 13 0 5 4 5 6 4 7 ...
 $ Sodas                    : int  20 13 23 13 13 33 15 27 12 19 ...
 $ Coffees                  : int  41 33 34 27 20 23 32 31 30 27 ...
 $ Total.Soda.and.Coffee    : int  61 46 57 40 33 56 47 58 42 46 ...
 $ Sales                    : num  200 196 103 163 102 ...
 $ Max.Daily.Temperature..F.: int  36 34 39 40 36 26 34 33 20 37 ...
 $ Total.Items.Wasted       : int  16 39 5 10 0 4 9 1 20 9 ...
 - attr(*, "na.action")= 'omit' Named int 34
  ..- attr(*, "names")= chr "34"
> ranicafe$coffees
NULL
> ranicafe$Coffees
 [1] 41 33 34 27 20 23 32 31 30 27 30 27 26 24 18 22 21 28 23 31 29 48 25 31 25 35 33 35 16 24 20 11 21  8  8  4  4  3  5
[40]  6  4 13  4 16 14 10 11
> sort(ranicafe$Coffees)
 [1]  3  4  4  4  4  5  6  8  8 10 11 11 13 14 16 16 18 20 20 21 21 22 23 23 24 24 25 25 26 27 27 27 28 29 30 30 31 31 31
[40] 32 33 33 34 35 35 41 48
> sort(ranicafe$Coffees)[1]
[1] 3
> sort(ranicafe$Coffees, decreasing=TRUE)
 [1] 48 41 35 35 34 33 33 32 31 31 31 30 30 29 28 27 27 27 26 25 25 24 24 23 23 22 21 21 20 20 18 16 16 14 13 11 11 10  8
[40]  8  6  5  4  4  4  4  3
> sort(ranicafe$Coffees, decreasing=TRUE)[1]
[1] 48
> min(ranicafe$Coffees)
[1] 3
> max(ranicafe$Coffees)
[1] 48
```



#### 최빈값

가장 많이 관찰된 값

```R
# 줄기와 잎 그림
stem(ranicafe$Coffees)
```

```R
> stem(ranicafe$Coffees)

  The decimal point is 1 digit(s) to the right of the |

  0 | 34444
  0 | 5688
  1 | 01134
  1 | 668
  2 | 001123344
  2 | 55677789
  3 | 001112334
  3 | 55
  4 | 1
  4 | 8
```



#### 평균과 중앙값

```R
> ## 평균
> rc<-ranicafe$Coffees
> 
> # 1/자료의 개수
> weight<-(1/length(rc))
> sum(rc*weight)
[1] 21.51064
> mean(rc)
[1] 21.51064
> # rc벡터 뒤에 새로운 원소 NA 추가
> rc<-c(rc,NA)
> # 맨 뒤 다섯개 원소 출력
> tail(rc, n=5)
[1] 16 14 10 11 NA
> mean(rc)
[1] NA
> mean(rc, na.rm=TRUE)
[1] 21.51064
> # 실제로 21잔이나 22잔이 많이 팔렸는지
> # which()는 논리벡터를 전달받아 참값의 인덱스를 반환해줌
> which(rc==21|rc==22)
[1] 16 17 33

> ## 양 끝 값의 변화에 대한 평균의 변화 
> # 커피판매량의 최대값을 480으로 변경
> rc[rc==max(rc)]<-480
> mean(rc)
[1] 30.70213
```

```R
> ## 중앙값
> # 자료량이 홀수이면 자료의개수+1값을 2로 나눠줌
> (median.idx<-(length(rc)+1)/2)
[1] 24
> (rc.srt<-sort(rc))
 [1]   3   4   4   4   4   5   6   8   8  10  11  11  13  14  16  16  18  20  20  21  21  22  23  23  24  24  25  25  26
[30]  27  27  27  28  29  30  30  31  31  31  32  33  33  34  35  35  41 480
> rc.srt[median.idx]
[1] 23
> median(rc)
[1] 23
> ## 양 끝값의 변화에 대한 중앙값의 변화
> # 최대값의 변화와 중앙값의 변화->둔감함.
> rc[rc==max(rc)]<-480
> (median(rc))
[1] 23
```

#### 

#### 표준편차와 사분위수 범위

```R
> ## 개별 관찰값과 평균과의 차이에 대한 평균
> ## 편차
> height <- c(164,166,168,170,172,174,176)
> # 평균을 height.m에 저장
> (height.m<-mean(height))
[1] 170
> # height의 개별값에서 평균을 뺀 값을 height.dev에 저장
> (height.dev<-height-height.m)
[1] -6 -4 -2  0  2  4  6
> # 편차합
> sum(height.dev)
[1] 0
> 
> ## 편차제곱의 평균
> # 편차 제곱
> (height.dev2<-height.dev^2)
[1] 36 16  4  0  4 16 36
> # 편차 제곱합
> sum(height.dev2)
[1] 112
> # 편차제곱의 평균
> mean(height.dev2)
[1] 16
> # 편차제곱합/(n-1) -> 분산
> sum(height.dev2)/(length(height)-1)
[1] 18.66667
> # 분산에 제곱근 취하기
> sqrt(sum(height.dev2)/(length(height)-1))
[1] 4.320494
> 
> ## 분산과 표준편차 구하기
> var(height)
[1] 18.66667
> sd(height)
[1] 4.320494
```



#### 심화

```R
> # 라니의 카페 커피 판매량에 대한 평균과 표준편차
> rc <- ranicafe$Coffees
> rc.m <- mean(rc)
> rc.sd <- sd(rc)
> # cat() -> 전달인자들을 하나의 문자열로 만들어 출력함
> # round() -> 실수형 자료에서 유효숫자를 지정해 실수를 출력함.
> cat("커피 판매량", round(rc.m,1),"±", round(rc.sd,2), "잔")
커피 판매량 21.5 ± 11.08 잔
```

##### 변동계수

: 평균에 대한 상대적인 변동성의 크기
$$
CV=\frac{s}{\bar x}
$$

```R
> # 변동계수 구하기
> rc<-ranicafe$Coffees
> rj<-ranicafe$Juices
> (rc.m<-mean(rc))
[1] 21.51064
> (rc.sd<-sd(rc))
[1] 11.08048
> (rj.m<-mean(rj))
[1] 4.93617
> (rj.sd<-sd(rj))
[1] 3.703138
> # 커피판매량의 변동계수가 주스판매량의 변동계수보다 작음.
> (rc.cv<-round(rc.sd/rc.m,3))
[1] 0.515
> (rj.cv<-round(rj.sd/rj.m,3))
[1] 0.75
```

##### 사분위수 범위와 상자도표

```R
> # 사분위수 범위와 상자도표
> # quantile() 함수를 이용해 사분위수 구함
> (qs<-quantile(rc))
  0%  25%  50%  75% 100% 
   3   12   23   30   48 
> # IQR
> qs[4]-qs[2]
75% 
 18 
> # 내장함수 IQR() 사용
> IQR(rc)
[1] 18
> # 상자도표
> bp<-boxplot(rc,main="커피 판매량에 대한 상자도표")
```

![1559288359505](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1559288359505.png)

##### 이상치

```R
> # 이상치 판별
> # 제동거리 자료의 사분위수값
> Q<-quantile(cars$dist)
> # 자료가 Q1-1.5*IQR, Q3+1.5*IQR 범위 바깥에 있으면 이상치로 판별
> ll<-Q[2]-1.5*IQR(cars$dist)
> ul<-Q[4]+1.5*IQR(cars$dist)
> 
> # 이상치찾기
> cars$dist[cars$dist<ll]
numeric(0)
> cars$dist[cars$dist>ul]
[1] 120
> 
> boxplot(cars$dist, main="Boxplot of Distance")
```

![1559288579797](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1559288579797.png)