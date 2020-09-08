# 데이터프레임(Dataframe)

## 1) 정의

> 2차원 구조를 가지고 있기 때문에 행렬과 동일한 형태를 가짐

- 열 단위로 서로 다른 타입의 데이터들로 구성 가능함
- 모든 열의 데이터 개수(행의 개수)는 동일해야함



## 2) 생성 방법

```R
# data.frame(vectors..)
# 각 벡터는 데이터프레임의 열을 구성함
# 데이터프레임의 열의 이름, 즉 변수의 이름은 벡터의 이름이 사용됨
> no <- c(1,2,3,4)
> name <- c('Apple','Banana','Peach','Berry')
> qty <- c(5,2,7,9)
> price <- c(500,200,200,500)
> fruit <- data.frame(no, name, qty, price)
> str(fruit)
'data.frame':	4 obs. of  4 variables:
 $ no   : num  1 2 3 4
 $ name : chr  "Apple" "Banana" "Peach" "Berry"
 $ qty  : num  5 2 7 9
 $ price: num  500 200 200 500
# 벡터 이름을 변수의 이름으로 사용하지 않으려면 직접 변수의 이름을 지정해야 함
product <- data.frame(id=v1, name=v2, price=v3)


# data.frame(row.names=vector,…)
# 데이터 프레임을 생성할 때 벡터를 행의 이름으로 사용할 때
# row.names 인수에 행 이름으로 사용할 벡터를 지정함

# data.frame(vectors…[,stringsAsFactors=TRUE])
# 문자 데이터를 팩터형으로 변환하고 싶을 경우 stringAsFactors=TRUE로 지정

# as.data.frame(vector or metrix..)
```



## 3) 인덱싱

```R
> fruit[1,]
  no  name qty price
1  1 Apple   5   500

> fruit[-1,]
  no   name qty price
2  2 Banana   2   200
3  3  Peach   7   200
4  4  Berry   9   500

> fruit[,2]
[1] "Apple"  "Banana" "Peach"  "Berry" 

> fruit[,3]
[1] 5 2 7 9

> fruit[,3, drop=F]
  qty
1   5
2   2
3   7
4   9

> fruit[, c(3,4)]
  qty price
1   5   500
2   2   200
3   7   200
4   9   500

> fruit[3,2]
[1] "Peach"

> fruit[3,1]
[1] 3

> fruit[,3]
[1] 5 2 7 9

> fruit$qty
[1] 5 2 7 9

> fruit[[3]]	# 열 인덱싱
[1] 5 2 7 9

> fruit[3]	# 데이터프레임 형식 유지
  qty
1   5
2   2
3   7
4   9
```



## 4) 주요 기능 및 함수

```R
head(df)			# 상위 6개 행 추출
head(df, n=2)		# 상위 2개 행 추출 (n의 개수만큼)
tail(df)			# 하위 6개 행 추출
tail(df, n=2)		# 하위 2개 행 추출 (n의 개수만큼)

rbind(df, vector)	# 기존의 데이터프레임에 벡터를 행으로 결합함
cbind(df, vector)	# 기존의 데이터프레임에 벡터를 열로 결합함
df$컬럼이름 <- vector	# 기존 데이터프레임에 새로운 열을 추가함

table(vector)		# 팩터로 변환하지 않아도 레벨별 수를 세어줌

# 원하는 행과 열 추출 : subset(df, select=컬럼명, subset=(조건))
# 커미션을 받는 직원들의 모든 정보 출력
emp[!is.na(emp$comm),]
subset(emp,!is.na(emp$comm)) 

# select ename,sal from emp where sal>=2000
subset(emp, select=c("ename","sal"), subset= emp$sal>= 2000)
subset(emp, emp$sal>= 2000, c("ename","sal"))
emp[emp$sal>=2000,c("ename","sal")]

# select ename,sal from emp where sal between 2000 and 3000
subset(emp, select=c("ename","sal"), subset=(emp$sal>=2000 & emp$sal<=3000))
emp[emp$sal>=2000 & emp$sal <=3000, c("ename","sal")]

# 조건문 사용해서 열 추가
score$grade<-ifelse(score$sum >= 230,"A",
                    ifelse(score$sum >= 215,"B", 
                           ifelse(score$sum >=200,"C","D")))

# 급여가 적은 순으로 모든 직원 정보 출력
emp[order(emp$sal),]
```

