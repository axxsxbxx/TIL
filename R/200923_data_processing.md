# 데이터 전처리

## 1. `apply` 계열 함수

```R
> df
      w   h
1  65.4 170
2  55.0 155
3 380.0  NA
4  72.2 173
5  51.0 161
6    NA 166

# apply(data, 1|2, function, na.rm=T|F)
# 배열 또는 행렬에 주어진 함수를 적용한 뒤 그 결과를 벡터, 배열 또는 리스트로 반환
> apply(df, 1, sum, na.rm=TRUE) # 1이면 행 방향
[1] 235.4 210.0 380.0 245.2 212.0 166.0
> apply(df, 2, sum, na.rm=TRUE) # 2이면 열 방향
    w     h 
623.6 825.0 

# lapply(data, function, na.rm=T|F)
# 벡터, 리스트 또는 표현식에 함수를 적용하여 그 결과를 리스트로 반환
> lapply(df, sum, na.rm=TRUE)
$w
[1] 623.6

$h
[1] 825

# sapply(data, function, na.rm=T|F)
# lapply와 유사하나 결과를 가능한 심플한 데이터 셋으로 반환(주로 벡터 or 리스트)
> sapply(df, sum, na.rm=TRUE)
    w     h 
623.6 825.0 

# tapply()
# 벡터에 있는 데이터를 특정 기준에 따라 그룹으로 묶은 뒤
# 각 그룹마다 주어진 함수를 적용하고 그 결과를 반환
> tapply(1:6, gender, sum, na.rm=TRUE)
 F  M 
13  8 
> tapply(df$w, gender, mean, na.rm=TRUE)
       F        M 
 53.0000 172.5333 

# mapply()
# sapply()의 확장된 버전으로, 여러 개의 벡터 또는 리스트를 인자로 받아
# 함수에 각 데이터의 첫째 요소, 둘째 요소...들을 적용한 결과 등을 반환
> mapply(paste, 1:5, LETTERS[1:5], month.abb[1:5])
[1] "1 A Jan" "2 B Feb" "3 C Mar" "4 D Apr" "5 E May"
```



## 2. `날짜 처리` 함수

```R
# 현재 날짜
Sys.Date()

# 현재 날짜 및 시간
Sys.time()

# 미국식 날짜 및 시간
date()

# timezone
Sys.timezone()

# 년월일 시분초 타입의 문자열을 시간으로 변경
as.Date("년-월-일 시:분:초")
as.Date("년/월/일 시:분:초")

# 특정 포맷을 이용한 날짜형
as.date("날짜 및 시간 문자열", format="포맷")
as.Date('1/15/2018',format='%m/%d/%Y') # format 은 생략 가능

# 문자열을 날짜 + 시간형으로
strptime("날짜 및 시간 문자열", format="포맷")
strptime('2019-08-21 14:10:30', "%Y-%m-%d %H:%M:%S")

# as.POSIXct()

# as.POSIXlt()

# 기타함수
weekdays("날짜 및 시간 문자열")		# 요일
months("날짜 및 시간 문자열")		# 월
quarters("날짜 및 시간 문자열")		# 분기
unclass("날짜 및 시간 문자열")		# 1970-01-01 기준으로 얼마나 지났는지

```

| Symbol | Meaning               | Example |
| ------ | --------------------- | ------- |
| `%d`   | day as a number(1-31) | 01-31   |
| `%a`   | abbreviated weekday   | Mon     |
| `%A`   | unabbreviated weekday | Monday  |
| `%m`   | month(01-12)          | 01-12   |
| `%b`   | abbreviated month     | Jan     |
| `%B`   | unabbreviated month   | January |
| `%y`   | 2-digit year          | 07      |



## 3. `문자열 처리` 함수

```R

```

