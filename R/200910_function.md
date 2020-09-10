# 함수

## 1. 정의

> 특정 작업을 독립적으로 수행하는 프로그램 코드 집합
>
> 함수를 사용하여 반복적인 연산을 효과적으로 할 수 있음

#### :heavy_check_mark: 함수의 처리 과정

- **시작(입력)** :매개변수를 통해 아규먼트값을 받아옴

- **실행(연산)** : 연산, 변환 등

- **종료(출력)** :수행결과를 데이터셋으로 반환, 출력 등



## 2. 생성 방법

```R
# 호출시 함수가 정의하고 있는 매개변수 사양에 맞춰서 아규먼트를 전달해야함
# 리턴값이 없는 함수는 NULL이 리턴됨
# return()문이 생략되는 경우에는 마지막으로 출력된 데이터 값이 자동으로 리턴됨
# 가급적 리턴함수를 사용하여 명확히 구현하는 것이 필요함
함수명 <- function([매개변수]){
    함수의 수행코드
    [return(리턴하려는 값)]
}

> func2 <- function(x,y) {
+   xx <- x
+   yy <- y
+   return(sum(xx, yy))
+ }
> 
> func2()
Error in func2() : 기본값이 없는 인수 "x"가 누락되어 있습니다
> func2(5,6)
[1] 11


# 매개변수에 기본값을 선언하는 경우 / 리턴값이 없는 경우
# 기본값이 존재하는 경우 기본값이 없는 매개변수만 전달해도 가능
# 기본값이 존재해도 다른 변수 전달 가능함
> exam5 <- function(n, deco="#"){
+   if(n > 0){
+     for(i in 1:n){
+       cat(deco)
+     }
+     cat("\n")
+   }
+   return()
+ }
> 
> exam5(5)
#####
NULL
> exam5(6, "@")
@@@@@@
NULL
> exam5(10, "*")
**********
NULL
> 
> exam5(-1)
NULL
```



## 3. 가변 길이 인자를 가지는 함수

```R
# 아규먼트의 개수와 타입을 가변적으로 처리 가능함
# 리턴값의 경우에도 선택적으로 처리 가능함
# 아규먼트의 타입을 제한하려는 경우 is.xxxx() 함수를 활용함
> f7<- function(...) {
+   data <- c(...)
+   sum <- 0;
+   for(item in data) {
+     if(is.numeric(item))
+       sum <- sum + item
+     else
+       print(item)
+   }
+   return(sum)
+ }
> f7(10,20,30)
[1] 60
> f7(10,20,'test', 30,40)
[1] "10"
[1] "20"
[1] "test"
[1] "30"
[1] "40"
[1] 0

# 일반 매개변수와 가변 매개 변수 동시에 사용 가능
> f9 <- function(p1, ..., p2="ㅋ") {
+   cat("p1=", p1, "\n")
+   cat("가변형 = ", ..., "\n")
+   cat("p2=", p2, "\n")
+ }
> 
> f9(10)
p1= 10 
가변형 =  
p2= ㅋ 
> f9(10,20)
p1= 10 
가변형 =  20 
p2= ㅋ 
> f9(10,20,30)
p1= 10 
가변형 =  20 30 
p2= ㅋ 
> f9(10,20,30,40)
p1= 10 
가변형 =  20 30 40 
p2= ㅋ 
> f9(10,20,30,40,p2=50)
p1= 10 
가변형 =  20 30 40 
p2= 50 
> f9(10,20,30,40,p1=50, p2=60)
p1= 50 
가변형 =  10 20 30 40 
p2= 60 
```



## 4. 전역변수와 지역변수의 사용

```R
# 함수 안에서 만들어진 변수는 지역변수이며, 지역변수는 함수내에서만 사용 가능함
# 함수 안에서 만들어지지 않은 변수를 사용할 때는 전역변수를 사용하는 결과가 됨
# 전역변수에도 존재하지 않는 변수를 사용하면 오류 발생
# 함수 내에서 전역 변수에 값을 저장하려는 경우 대입연산자로 <<- 을 사용함
> a <- 3
> b <- 7
> c <- 11 
> ft<-function(a){
+   b<-a+10     
+   c<<-a+10   # 전역대입연산 
+   d<-a
+   print(a);print(b);print(c);print(d)
+   return()  # NULL
+ }
> print(ft(100))
[1] 100
[1] 110
[1] 110
[1] 100
NULL
> print(a);print(b);print(c);print(d) 
[1] 3
[1] 7
[1] 110
Error in print(d) : 객체 'd'를 찾을 수 없습니다
```



## 5. invisible() 함수

```R
# return() 함수는 리턴값을 출력해주지만 invisible() 함수는 출력해주지 않음
# 하지만 리턴값은 저장되기 때문에 변수에 할당해서 사용 가능
# 리턴값을 눈으로 확인할 필요가 없는 경우 사용
> ft.1 <- function(x) return()
> ft.2 <- function(x) return(x+10)
> ft.3 <- function(x) invisible(x+10)
> 
> ft.1(100)
NULL
> ft.2(100)
[1] 110
> ft.3(100)
> 
> r1 <- ft.1(1000);r1
NULL
> r2 <- ft.2(1000);r2
[1] 1010
> r3 <- ft.3(1000);r3
[1] 1010
```



## 6. stop() / warning() / try() / trycatch()

```R
# stop()
# 에러를 일으킬 조건을 만족하면 강제로 에러를 일으켜서 함수를 중단시킴
> testError1 <- function(x){
+   if(x<=0)
+     stop("양의 값만 전달 하세요.")
+   return(rep("테스트",x))
+ }
> 
> testError1(5)
[1] "테스트" "테스트" "테스트" "테스트" "테스트"
> testError1(0)
Error in testError1(0) : 양의 값만 전달 하세요.

# warning()
# 조건을 만족하면 경고창을 띄움
# 함수를 중단시키지는 않고 경고 메시지를 띄운 후 끝까지 수행함
> testWarn <- function(x){
+   if(x<=0)
+     stop("양의 값만 전달 하세요.")
+   if(x>5){
+     x<-5
+     warning("5보다 크면 안됩니다. 5로 처리해서 수행합니다.")
+   }
+   return(rep("테스트",x))
+ }
> 
> testWarn(3)
[1] "테스트" "테스트" "테스트"
> testWarn(10)
[1] "테스트" "테스트" "테스트" "테스트" "테스트"
경고메시지(들): 
In testWarn(10) : 5보다 크면 안됩니다. 5로 처리해서 수행합니다.

# try()
# 에러가 발생하더라도 중단시키지 않고 에러 메세지 띄운 후 실행함
> test2 <- function(p){
+   cat("난 수행함\n")
+   try(testError(-1))
+   cat("나 수행할까요? \n")
+ }
> test2()
난 수행함
Error in testError(-1) : 함수 "testError"를 찾을 수 없습니다
나 수행할까요? 

# trycatch()
# 예외처리를 정의할 수 있는 함수
> testAll <-function(p){
+   tryCatch({
+     if(p=="오류테스트"){
+       testError1(-1)
+     }else if (p =="경고테스트"){
+       testWarn(6)
+     }else{
+       cat("정상 수행\n")
+       print(testError1(2))
+       print(testWarn(3))
+     }
+   },warning = function(w){
+     print(w)
+   },error = function(e){
+     print(e)
+   },finally ={
+     cat("오류, 경고 발생 여부에 관계없이 반드시 수행되는 부분\n")
+   })
+ }
> 
> testAll("오류테스트")
<simpleError in testError1(-1): 양의 값만 전달 하세요.>
오류, 경고 발생 여부에 관계없이 반드시 수행되는 부분
> testAll("경고테스트")
<simpleWarning in testWarn(6): 5보다 크면 안됩니다. 5로 처리해서 수행합니다.>
오류, 경고 발생 여부에 관계없이 반드시 수행되는 부분
> testAll("아무거나")
정상 수행
[1] "테스트" "테스트"
[1] "테스트" "테스트" "테스트"
오류, 경고 발생 여부에 관계없이 반드시 수행되는 부분
```



## 기타 함수

```R
# is.xxxx() 함수는 원래 값 하나씩 비교함

# any()
# any(is.xxxx()) 로 수행하면 해당되는 값이 하나라도 있으면 TRUE
> f.case2 <- function(x) {
+   if(any(is.na(x))) 
+     return("NA가 있습니다.")
+   else
+     return("NA가 없습니다.")
+ }
> f.case2(100)
[1] "NA가 없습니다."
> f.case2(NA)
[1] "NA가 있습니다."
> f.case2(1:6)
[1] "NA가 없습니다."
> f.case2(c(10,20,30))
[1] "NA가 없습니다."
> f.case2(c(NA, 20))
[1] "NA가 있습니다."
> f.case2(c(10, NA, 20))
[1] "NA가 있습니다."

# all()
# all(is.xxxx()) 로 수행하면 모두 해당되는 값이면 TRUE
> f.case3 <- function(x) {
+   if(all(is.na(x))) 
+     return("모두 NA임")
+   else
+     return("모두 NA인 것은 아님")
+ }
> f.case3(100)
[1] "모두 NA인 것은 아님"
> f.case3(LETTERS)
[1] "모두 NA인 것은 아님"
> f.case3(NA)
[1] "모두 NA임"
> f.case3(c(NA, NA, NA))
[1] "모두 NA임"
> f.case3(c(NA, NA, 10))
[1] "모두 NA인 것은 아님"

# Sys.sleep()
# 지연할 초 단위를 설정할 수 있는 함수
# 웹 크롤링할 때 유용하게 사용
```