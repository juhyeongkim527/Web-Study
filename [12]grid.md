# 미디어 쿼리

- **뷰포트** 는 실제 화면이 표시되는 영역을 말함, `<head>` 태그의 `<meta>` 태그 내에 아래와 같이 사용 가능\
`<meta name = "viewport" content = "width = device-width, initial-scale = 1">`

- 단말기 브라우저 창의 너비와 높이는 `device-width`, `device-height` 로 나타낼 수 있고, 실제 브라우저의 너비와 다를 수 있기 때문에 이를 주의해야함

- `<line rel = "stylesheet" media = "미디어 쿼리 조건" href = "css 파일 경로">` 를 통해 미디어 쿼리가 작성된 외부 css 파일을 각 조건에 따라서 가져올 수 있음

- css 파일 내부에서는 `<style>` 태그 내부에서 `@media <미디어 조건 (and)로 연결 가능> { <스타일 규칙> }` 으로 작성 가능

# 플렉스 박스 레이아웃 

- columns 개수 지정 불가 : 알아서 웹페이지 크기에 따라서 `flex-wrap : wrap;`을 해주면 columns과 rows의 개수가 지정됨

- 따라서, 플렉스 항목의 정렬 방법을 사용하는 `align-self` 속성 이외에는 대부분 플렉스 컨테이너에 적용할 클래스나 아이디에 속성을 작성

# CSS 그리드 레이아웃

- columns, rows 개수 지정 가능 : `autofit`이나 `autofill`과, `minmax()`를 사용하여 자동으로 지정도 가능

- 그리드 항목에 번호로 레이아웃을 지정하는 방식이나, 컨테이너에 템플릿 영역을 지정하는 방식 두가지로 사용 가능
    - 여기서, 각 class를 ㄱ자나 ㄴ자같이 한줄로 쓰지 않는다면 다른 클래스와 div를 정의해서 사용해줘야함

- 예를 들어, 아래처럼하면 `box1`을 ㄱ자로 쓰니까 안되고,

```
<!DOCTYPE html>
<html lang="ko">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>CSS Grid Layout</title>
  <style>
    #wrapper {
      width: 700px;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-template-rows: repeat(3, 100px);
      grid-template-areas:
        "box1 box1 box1"
        "box2 box3 box3"
        "box2 . box4"
    }

    .box {
      padding: 15px;
      color: #fff;
      font-weight: bold;
      text-align: center;
    }

    .box1 {
      background-color: #3689ff;
      grid-area: box1;
    }

    .box2 {
      background-color: #00cf12;
      grid-area: box2;
    }

    .box3 {
      background-color: #ff9019;
      grid-area: box3;
    }

    .box4 {
      background-color: #ffd000;
      grid-area: box4;
    }
  </style>
</head>

<body>
  <div id="wrapper">
    <div class="box box1">box1</div>
    <div class="box box2">box2</div>
    <div class="box box3">box3</div>
    <div class="box box4">box4</div>
  </div>
</body>

</html>
```

- 아래처럼, `box1`을 2번 써서 해도 안됨 : 다른 영역에 갈때는 class 이름을 하나 더 추가해줘야함

```
<!DOCTYPE html>
<html lang="ko">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>CSS Grid Layout</title>
  <style>
    #wrapper {
      width: 700px;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-template-rows: repeat(4, 100px);
      grid-template-areas:
        "box1 box1 box1"
        "box2 box3 box3"
        "box2 . box4"
        "box1 box1 box1"
    }

    .box {
      padding: 15px;
      color: #fff;
      font-weight: bold;
      text-align: center;
    }

    .box1 {
      background-color: #3689ff;
      grid-area: box1;
    }

    .box2 {
      background-color: #00cf12;
      grid-area: box2;
    }

    .box3 {
      background-color: #ff9019;
      grid-area: box3;
    }

    .box4 {
      background-color: #ffd000;
      grid-area: box4;
    }
  </style>
</head>

<body>
  <div id="wrapper">
    <div class="box box1">box1</div>
    <div class="box box2">box2</div>
    <div class="box box3">box3</div>
    <div class="box box4">box4</div>
    <div class="box box1">box1</div>
  </div>
</body>

</html>
```
