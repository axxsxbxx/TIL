# 동적 크롤링

## 1. 동적 크롤링하는 경우

- 사용자의 선택과 같은 이벤트에 의해서 자바스크립트의 수행 결과로 컨텐츠 생성
- 페이지의 랜더링을 끝낸 후에 Ajax 기술을 이용하여 서버로부터 컨텐츠의 일부를 전송받아 동적으로 구성하는 경우



## 2. Selenium 서버 사용

- Selenium 서버를 사용하면 제어되는 브라우저에 페이지를 랜더링 해놓고 랜더링된 결과에서 컨텐츠를 읽어올 수 있음
- 컨텐츠 내에 클릭 이벤트를 발생할 수도 있으며 로그인과 같은 데이터를 입력하는 것도 가능

> ### selenium 서버 기동 과정
> 1) selenium-server-standalone-master.zip, chromedriver.exe 를 복사한다.
>
> 2) 적당한 디렉토리에 selenium-server-standalone-master.zip 파일의 압축을 푼다
>
> 3) bin 디렉토리 앆에 chromedriver.exe 를 복사한다.
>
> 4) Selenium 을 기동시킨다. : `java -Dwebdriver.chrome.driver="chromedriver.exe" -jar selenium-server-standalone-4.0.0-alpha-1.jar -port 4445` 를 cmd 창에 입력시킴 



## 3. 동적 크롤링 주요 API

```R
# Selenium 서버에 접속하고 remoteDrier 객체 리턴
remDr <- remoteDriver(remoteServerAddr="localhost", port=4445, browserName="chrome")

# 크롬 브라우저 오픈
remDr$open()

# 페이지 랜더링
remDr$navigate(url) 

# 태그 찾음
doms <- remDr$findElements(using ="css selector", "컨텐츠를 추출하려는 태그의 선택자")

# 찾아진 태그들의 컨텐츠 추출
sapply(doms,function(x){x$getElementText()})

# 태그 찾음
more <- remDr$findElements(using='css selector','클릭이벤트를 강제 발생시키려는 태그의 선택자')

# 찾아진 태그에 클릭 이벤트 발생시키는 두 가지 방법
sapply(more,function(x){x$clickElement()})
remDr$executeScript("arguments[0].click();", more)

# 페이지를 아래로 내리는(스크롤) 효과
webElem <- remDr$findElement("css", "body")
remDr$executeScript("scrollTo(0, document.body.scrollHeight)", args=list(webElem))
```

