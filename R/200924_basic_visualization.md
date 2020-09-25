# 기본 시각화

## 1. 시각화 함수의 종류

- 고수준 함수 : plot(), boxplot(), hist(), pie(), barplot()
- 저수준 함수 : title(), lines(), axis(), legend(), points(), text()
- 칼라팔레트 함수 : rainbow(), cm.colors(), topo.colors(), terrian.colors(), heat.colors()



## 2. 산포도 - plot()

```R
# 기본 문법
plot(x축 데이터, y축 데이터, 옵션)

# 축에 대한 옵션 설정 axis()
# side = 1 : 하단 축부분, side = 2 : 좌측 축부분
# side = 3 : 상단 축부분, side = 4 우측 축부분
# at : 축의 표시 단위
# labels : 축에 표시될 값
# pos : 축의 위치 
axis(side=, at = NULL, labels = TRUE, tick = TRUE, pos = NA, outer = FALSE, ...)

# 점을 그리는 함수 points()
# 이미 생성된 plot에 점을 추가로 그려줌
points(x, y, 옵션)

# 출력된 그래프 위에 선을 추가하는 함수
# 꺾은 선 추가 lines()
lines(x, y, 옵션)
# 직선 추가 abline()
abline(v = 3, lty = 2)  # vertical
abline(h = 0, lty = 3)  # horizontal
abline(a = -1, b = 1, col = "red")  # y = -1 + x
# 곡선 추가 curve()
curve(x, y, 옵션)

# 제목 설정 title()
title(main="성적그래프", col.main="red", font.main=4) #메인 제목
title(xlab="학번", col.lab=rgb(1,0,0)) # x축 제목
title(ylab="점수", col.lab=rgb(0,0,1)) # y축 제목

# 문자열 표시 text()
# adj는 텍스트의 위치를 지정하는 옵션
# adj : (0,0) 우측 상단, (0, 1) 우측 하단, (1, 0) 좌측 상단, (1, 1) 좌측 하단
text(x좌표, y좌표, labels = "표시할 문자", adj = NULL)

# 그래프의 배치 조정(mfrow)
# nr : 행의 갯수, nc : 열의 갯수
par ( mfrow = c(nr,nc) ) 

# 범례 추가 legend()
legend(x축 위치, y축 위치, 내용, cex=글자크기, col=색상, pch=크기, lty=선모양)
```

| **옵   션**                  | **설    명**                                  |
| ---------------------------- | --------------------------------------------- |
| main = "메인 제목"           | 제목 설정                                     |
| sub = "서브 제목"            | 서브 제목                                     |
| xlab = "문자", ylab = "문자" | x, y 축에 사용할 문자열을 지정함              |
| xlim = 범위, ylim = 범위     | x, y 축 값의 범위                             |
| xaxt="n", yaxt="n"           | x, y 축의 값을 나타내지 않음                  |
| ann = F                      | x, y 축 제목을 지정하지 않음                  |
| tmag = 2                     | 제목 등에 사용되는 문자의 확대율 지정         |
| axes = F                     | x, y 축을 표시하지 않습니다.                  |
| **그래프 유형 : type()**     |                                               |
| type = "p"                   | 점 모양 그래프 (기본값)                       |
| type = "l"                   | 선 모양 그래프 (꺾은선 그래프)                |
| type = "b"                   | 점과 선 모양 그래프                           |
| type = "c"                   | "b"에서 점을 생략한 모양                      |
| type = "o"                   | 점과 선을 중첩해서 그린 그래프                |
| type = "h"                   | 각 점에서 x축 까지의 수직선 그래프            |
| type = "s"                   | 왼쪽값을 기초로 계단모양으로 연결한 그래프    |
| type = "S"                   | 오른쪽 값을 기초로 계단모양으로 연결한 그래프 |
| type = "n"                   | 축 만 그리고 그래프는 그리지 않음             |

| 선의 모양 선택        |                                                              |
| --------------------- | ------------------------------------------------------------ |
| lty=0, lty="blank"    | 투명선 (그리지 않음)                                         |
| lty=1, lty="solid"    | 실선 (default)                                               |
| lty=2, lty="dashed"   | 대시                                                         |
| lty=3, lty="dotted"   | 점선                                                         |
| lty=4, lty="dotdash"  | 점선과 대시                                                  |
| lty=5, lty="longdash" | 긴 대시                                                      |
| lty=6, lty="twodash"  | 2개의 대시                                                   |
| **색, 기호 등**       |                                                              |
| col = 1, col = "blue" | 기호의 색 지정, 1-검, 2-빨, 3-초, 4-파, 5-연파랑, 6-보, 7-노, 8-회색 |
| pch = 0, pch = "문자" | 점 모양 지정 : example(points) 실행하면 pch값의 기호 확인 가능 |
| bg = "blue"           | 그래프의 배경색 지정                                         |
| lwd = "숫자"          | 선을 그릴 때 선의 굵기를 지정                                |
| cex = "숫자"          | 점이나 문자를 그릴 때 점이나 문자의 크기를 지정              |



## 3. 막대그래프 - barplot()

```R
# plot 함수의 기본 옵션과 동일함
barplot(x, y, 옵션)
```

| 인  수              | 기  능                                                 |
| ------------------- | ------------------------------------------------------ |
| angle, density, col | 막대를 칠하는 선분의 각도, 선분의 수, 선분의 색을 지정 |
| legend              | 오른쪽 상단에 범례를 그림                              |
| names               | 각 막대의 라벨을 정하는 문자열 벡터를 지정             |
| width               | 각 막대의 상대적인 폭을 벡터로 지정                    |
| space               | 각 막대 사이의 간격을 지정                             |
| beside              | TRUE를 지정하면 각각의 값마다 막대를 그림              |
| horiz               | TRUE를 지정하면 막대를 옆으로 눕혀서 그림              |



## 4. 히스토그램 - hist()

```R
# plot 함수의 기본 옵션과 동일함
# breaks 지정하지 않으면 자동으로 나눠줌
hist(data, breaks=범위)
```



## 5. 박스플롯 - boxplot()

```R
# plot 함수의 기본 옵션과 동일함
boxplot(data, 옵션)
```

| **옵  션** | **의  미**                                                   |
| ---------- | ------------------------------------------------------------ |
| col        | 박스 내부의 색깔을 지정                                      |
| names      | 각 막대의 라벨을 지정할 문자벡터를 지정                      |
| width      | 박스의 폭을 지정                                             |
| range      | 박스의 끝에서 수염까지의 길이를 지정. 기본은 1.5             |
| notch      | true로 지정할 경우 상자의 허리 부분을 가늘게 표시            |
| horizontal | true로 지정하면 상자를 수평으로 그림. 아래부터 차례로 나열됨 |



## 6. 파이그래프 - pie()

```R
pie(data, radius=크기, 옵션)
```

| **인  수**          | **기  능**                                                   |
| ------------------- | ------------------------------------------------------------ |
| angle, density, col | pie 부분을 구성하는 각도(angle), 수(density), 색상(col)을 지정 |
| labels              | 각 pie 부분의 이름을 지정하는 문자벡터를 지정                |
| radius              | 원형의 크기를 지정                                           |
| clockwise           | 시계방향(T)으로 회전할 지 반 시계방향(F:기본)으로 회전할지 지정 |
| init.angle          | 시작되는 지점의 각도지정                                     |



## 7. 파일로 그래프 저장

```R
# 화면에 나타내지 않고 바로 파일로 저장
png(filename, height=, width=, bg=)
{그래프 그리는 명령어}
dev.off()

# 화면에 나타난 그래프를 파일로 저장
dev.copy(png, filename="") or dev.copy(pdf, filename="")
dev.off()
```

