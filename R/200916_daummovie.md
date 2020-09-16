# 다음 영화 리뷰 크롤링

## 1. 한 페이지 크롤링

```R
# 댓글이 모두 다 존재하는 경우
library(rvest)

text <- NULL; point <- NULL; review <- NULL; page <- NULL
url <- "https://movie.daum.net/moviedb/grade?movieId=131576"
text <- read_html(url, encoding="UTF8")
text

# 고객 평점
nodes <- html_nodes(text, ".raking_grade em")
point <- html_text(nodes)
point

# 고객 리뷰
nodes <- html_nodes(text, ".desc_review")
nodes <- html_text(nodes, trim=TRUE)
nodes
review <- nodes[nchar(nodes) > 0]
review
page <- data.frame(point, review)
View(page)

write.csv(page, "daummovie1.csv")


# 댓글 없는 경우
library(rvest)

text <- NULL; vpoint <- NULL; vreview <- NULL; page <- NULL
url <- "https://movie.daum.net/moviedb/grade?movieId=131576"
text <- read_html(url, encoding="UTF-8")
text
for (i in 1:10){
  # 영화 평점
  node <- html_nodes(text, xpath=paste0('//*[@id="mArticle"]/div[2]/div[2]/div[1]/ul/li[', i, "]/div/div[1]/em"))
  point <- html_text(node)
  vpoint <- c(vpoint, point)
  
  # 영화 리뷰
  node <- html_nodes(text, xpath=paste0('//*[@id="mArticle"]/div[2]/div[2]/div[1]/ul/li[', i, "]/div/p"))
  review <- html_text(node, trim=TRUE)
  vreview <- append(vreview, review)
}
page <- data.frame(vpoint, vreview)
View(page)

write.csv(page, "daummovie1.csv")

```



## 2. 여러 페이지 크롤링

```R
library(rvest)

text <- NULL; point <- NULL; review <- NULL; page <- NULL; movie.review <- NULL

site <- "https://movie.daum.net/moviedb/grade?movieId=131576&type=netizen&page="

for (i in 1:5){
  vpoint <- NULL; vreview <- NULL;
  
  url <- paste0(site, i)
  text <- read_html(url, encoding="UTF-8")
  
  # 영화 평점
  nodes <- html_nodes(text, ".raking_grade em")
  point <- html_text(nodes)
  # 영화 리뷰
  nodes <- html_nodes(text, ".desc_review")
  nodes <- html_text(nodes, trim=TRUE)
  review <- nodes[nchar(nodes) > 0]
  
  if(length(review) == 10) {
    page <- data.frame(point, review)
    movie.review <- rbind(movie.review, page)

  } else {
    for (j in 1:10){
      # 영화 평점
      node <- html_nodes(text, xpath=paste0('//*[@id="mArticle"]/div[2]/div[2]/div[1]/ul/li[', j, "]/div/div[1]/em"))
      point <- html_text(node)
      vpoint <- c(vpoint, point)
      
      # 영화 리뷰
      node <- html_nodes(text, xpath=paste0('//*[@id="mArticle"]/div[2]/div[2]/div[1]/ul/li[', j, "]/div/p"))
      review <- html_text(node, trim=TRUE)
      vreview <- c(vreview, review)
    }
    page <- data.frame(point=vpoint, review=vreview)
    movie.review <- rbind(movie.review, page)
  }
}
View(movie.review)
write.csv(movie.review, "daummovie2.csv")

```



## 3. 전체 페이지 크롤링

```R
library(rvest)

text <- NULL; point <- NULL; review <- NULL; page <- NULL; movie.review <- NULL

site <- "https://movie.daum.net/moviedb/grade?movieId=131576&type=netizen&page="

# 전체 리뷰수 이용해서 페이지 수 구하기
node <- html_nodes(read_html(site, encoding="UTF-8"), ".txt_menu")
total <- html_text(node)
total
total <- as.numeric(gsub("[[:punct:]]", "", total)) # 특수문자 제거한 후 숫자로 변환

len <- ceiling(total/10)   # 올림 처리해줌

for (i in 1:len){
  vpoint <- NULL; vreview <- NULL;
  
  url <- paste0(site, i)
  text <- read_html(url, encoding="UTF-8")
  
  # 영화 평점
  nodes <- html_nodes(text, ".raking_grade em")
  point <- html_text(nodes)
  # 영화 리뷰
  nodes <- html_nodes(text, ".desc_review")
  nodes <- html_text(nodes, trim=TRUE)
  review <- nodes[nchar(nodes) > 0]
  
  if(length(review) == 10) {
    page <- data.frame(point, review)
    movie.review <- rbind(movie.review, page)
    
  } else {
    for (j in 1:10){
      # 영화 평점
      node <- html_nodes(text, xpath=paste0('//*[@id="mArticle"]/div[2]/div[2]/div[1]/ul/li[', j, "]/div/div[1]/em"))
      point <- html_text(node)
      vpoint <- c(vpoint, point)
      
      # 영화 리뷰
      node <- html_nodes(text, xpath=paste0('//*[@id="mArticle"]/div[2]/div[2]/div[1]/ul/li[', j, "]/div/p"))
      review <- html_text(node, trim=TRUE)
      vreview <- c(vreview, review)
    }
    page <- data.frame(point=vpoint, review=vreview)
    movie.review <- rbind(movie.review, page)
  }
}
View(movie.review)
write.csv(movie.review, "daummovie3.csv")
```





