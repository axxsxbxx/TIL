# 정적 스크래핑(크롤링)

## 1. 웹 스크래핑/크롤링

- `웹 스크래핑(Web Scraping)`

  > 웹 사이트 상에서 원하는 부분에 위치한 정보를 컴퓨터로 하여금 자동으로 추출하여 수집하는 기술

- `웹 크롤링(Web Crawling)`

  > 자동화 봇인 웹 크롤러가 정해진 규칙에 따라 복수 개의 웹 페이지를 브라우징 하는 행위

  

## 2. `rvest` 패키지의 주요 함수

```R
# 응답 객체를 HTML로 변환
read_html(url, encoding="UTF-8/CP949")

# HTML 요소를 추출하는 함수
html_node(x, css, xpath)
html_nodes(x, css, xpath)

# 데이터를 추출하는 함수
html_text(x, trim=FALSE)

# HTML 속성과 관련된 함수
html_attrs(x)
html_attr(x, name, default="")
```



## 3. `XML` 패키지의 주요 함수

```R
# 응답 객체 변환
htmlParse(file, encoding="UTF-8/CP949")

# 데이터 추출하는 함수
xpathSApply(doc, path, fun)
# fun : xmlValue, xmlGetAttr, xmlAttrs

```



## 4. `httr` 패키지의 주요 함수

```R
# GET으로 사이트 내용 가져오기
http.standard <- GET(url)
title2 = html_nodes(read_html(http.standard), css)
title2 = html_text(title2)

# POST로 사이트 내용 가져오기
data = POST(url, query = list(code = my_otp),
add_headers(referer = otp_url)) 
```



