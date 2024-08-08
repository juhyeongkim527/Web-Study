# `Object`

자바스크립트에서 Object, 즉 객체는 **프로그램에서 인식할 수 있는 모든 대상**을 가리킨다고 봐도 무방하다. 거의 대부분이 객체로 이루어져서 그런 것 같다.

1. 문서 객체 모델(DOM) : 웹 문서 자체도 객체이고, 그 안에 삽입되는 이미지, 링크, 텍스트 필드 모두 객체이다. 
  - `document`, `image`, `link`

2. 브라우저 관련 객체 : 웹 브라우저에서 사용하는 정보
  - `navigator`, `history`, `location`, `screen`

3. 내장 객체 : 자바스크립트 안에 미리 정의되어 있는 객체
  - `Array`, `Data`

# `Instance`, `Property`, `Method`

- `Instance` : 객체를 통해 만들어진 것, 객체의 `Property`와 `Method`를 그대로 물려 받음

- `Property` : 변수, `field`

- `Method` : 함수

마침표 표기법을 사용하여, `Instance.Property` 또는 `Instance.Method()`로 사용한다.

### 예제

```
var now = new Data();
document.write("현재 시각은 " + now.toLocaleString());
```

# `Array` 객체

## `concat()` : 배열끼리 합쳐서 새로운 배열을 리턴하는 메서드 (기존 배열은 수정하지 않음)

```
var nums = [1, 2, 3];
var chars = ["a", "b", "c", "d"];

// 두 개의 배열 합치기
var numsChars = nums.concat(chars); // [1, 2, 3, "a", "b", "c", "d"]
var charsNums = chars.concat(nums); // ["a", "b", "c", "d", 1, 2, 3]
```

## `join()` : 배열끼리 합쳐서 `string`을 리턴하는 메서드 (`argument`로 구분자 지정 가능, 기본 구분자는 `,`)

```
var string1 = nums.join(); // 1,2,3
var string2 = chars.join('/'); // a/b/c/d
```

## `push()` : 배열의 맨 끝에 요소 추가 (추가 후`length`를 반환)

## `unshift()` : 배열의 맨 앞에 요소 추가 (추가 후`length`를 반환)

## `pop()` : 배열의 맨 끝 요소를 삭제 후 해당 요소 반환

## `shift()` : 배열의 맨 앞 요소를 삭제 후 해당 요소 반환

## `splice()` : 원하는 위치에 요소를 삭제하거나 추가

원하는 위치에 요소를 삭제하거나 추가한 후 삭제한 배열을 `return` 한다. 기존 배열이 수정되는 것에 주의

1. `argument`가 1개인 경우 : 삭제할 시작 `index`를 나타냄, `index`를 포함하여 뒤의 모든 요소가 삭제되어 삭제된 요소들이 배열로 `return`됨

2. `argument`가 2개인 경우 : 삭제할 시작 `index`와 삭제할 크기 `size`를 나타냄, `index`를 포함하여 `size`개 만큼 요소가 삭제되고, 삭제된 요소들이 배열로 `return`됨

3. `argument`가 3개인 경우 : 삭제할 시작 `index`와 삭제할 크기 `size`와 추가할 요소 `value`를 나타냄. 
`index`를 포함하여 `size`개 만큼 요소가 삭제되고, `index` 위치에 `value`가 추가 됨. `size`가 `0`인 경우 `return` 되지 않고, 추가만 되며 `value` 자체를 배열로 나타내서 1개 이상 추가 가능


## `slice()` : 원하는 위치에 요소를 삭제 (추가하는건 `splice(index, 0, value)`로 하면 되기 때문에 추가는 없음)

`splice()`와 달리 기존 배열을 변경하지 않고 삭제할 만큼의 요소만 배열로 만들어서 `return` 함

1. `argument`가 1개인 경우 : 삭제할 시작 `index`를 나타냄, `index`를 포함하여 뒤의 모든 요소를 배열로 `return`함, 원래 배열은 바뀌지 않음

2. `argument`가 2개인 경우 : 삭제할 시작 `index`와 `size`가 아닌 `end index`을 나타냄. 범위가 `[,)` 이므로, `end index`를 포함하지 않고 배열로 `return`함, 똑같이 원래 배열은 바뀌지 안흥ㅁ

# `Date` 객체

- `new Date();` : 현재 날짜 나타내기

- `new Date("2024-08-07");` : 특정 날짜 나타내기

- `new Date("2024-08-07T18:00:00");` : 특정 날짜와 시간 나타내기

1. `YYYY-MM-DD` 형식
  - `new Date("2024")`;
  - `new Date("2024-08")`;
  - `new Date("2024-08-07")`;

2. `YYYY-MM-DDTHH` 형식
  - `new Date("2024-08-07T18:00:00");`
  - `new Date("2024-08-07T18:00:00Z");` : `Z`를 맨 끝에 붙이면 UTC(국제 표준시)를 나타냄

3. `DD/MM/YYYY` 형식
   - `new Date("07/08/2024");`

4. 이름 형식
  - `new Date("Mon Jan 20 2020 15:00:41 GMT+0900 (대한민국 표준시)");`

## `Date` 객체 메서드

1. 날짜 시간 정보 가져오기 : `get`으로 시작

2. 날짜 시간 설정하기 : `set`으로 시작

3. 날짜 시간 형식 바꾸기 : `toLocaleString()` - 현재 날짜와 시간을 현지 시간으로 표시, `toString()` - `Date` 객체 타입을 문자열로 표시

---

아래와 같이 `document.querySelector(.class명 or #id명).innerText = 변수명` 을 통해, 태그 사이에 변수를 출력할 수 있음

`innerText`는 `querySelector`에서 선택된 태그에서 `Text`만 가져오는거고 `innerHTML`은 태그 내에 있는 내부 태그와 텍스트를 전부 가져오는거임

```
<body>
  <div id="container">
    <h1>책 읽기</h1>
    <p><span class="accent" id="result"></span>일 연속으로 <br> 책 읽기를 달성했군요.</p>
    <p>축하합니다!</p>
  </div>  

  <script>
    var now = new Date("2020-10-15");       // 오늘 날짜를 객체로 지정
    var firstDay = new Date("2020-10-01");   // 시작 날짜를 객체로 지정

    var toNow = now.getTime();         // 오늘까지 지난 시간(밀리 초)
    var toFirst = firstDay.getTime();  // 첫날까지 지난 시간(밀리 초) 
    var passedTime = toNow - toFirst;  // 첫날부터 오늘까지 지난 시간(밀리 초)

    passedTime = Math.round(passedTime/(1000*60*60*24));  // 밀리 초를 일 수로 계산하고 반올림

    document.querySelector('#result').innerText = passedTime;
  </script>
</body>
```

# `Math` 객체

`Math` 객체는 따로 `Instance`를 생성하지 않고 바로 `Math.property`, `Math.method()` 로 사용한다.

`Math` 에는 다양한 프로퍼티와 메서드가 존재한다.

# 브라우저 객체

웹 브라우저 창에 웹 문서가 표시되는 순간 브라우저는 HTML 소스를 해석하여 관련된 객체를 만들어 내는데, 가장 먼저 만들어지는 객체가 `window` 객체이다.

`window` 객체는 최상위 요소의 객체이고, 해당 요소의 하위 요소로 차례대로 웹 문서나 주소 표시줄과 같은 하위 객체를 만들어낸다.

![image](https://github.com/user-attachments/assets/e3300a88-9f1e-4247-914c-65301f216d3c)

브라우저와 관련된 객체는 `window, document, navigator, history, location, screen` 등 여러 요소가 있고, 중요 요소들을 차례대로 살펴보자.

# `window` 객체

가장 상위 요소의 객체이고, 여러 property와 method가 존재한다. `alert()`, `prompt()`등의 method도 전부 `window` 객체의 메서드이고, 원래는 `window.alert();` 처럼 사용해야 하지만, 최상위 객체라는 특별한 성질 때문에 `alert()`로 생략해서 쓸 수 있다.

## `open()` method

새 브라우저 창을 여는 메서드로, 팝업창과 같이 새 창을 띄울 때 많이 사용된다.

`open(경로, 창 이름, 창 옵션)` 의 형태를 가지며, 경로는 새 창에 표시할 `html` 문서나 사이트의 경로를 나타낸다.

창 이름은 팝업창의 이름을 지정하는데, 창 이름이 지정되어있지 않으면 이미 팝업창이 떠있어도 웹 문서를 새로고침하면 계속 똑같은 팝업창이 뜨는 반면, 창 이름을 지정해주면 새로고침을 해줘도 해당 팝업이 떠있다면 다시 뜨지 않게 된다.

창 옵션은 `left, top, width, height` 속성을 지니며, 창 옵션이 없으면 왼쪽 상단에 붙어서 새로운 창이 뜬다.

그리고, `open()` 메서드는 사이트의 팝업이 차단되어 있으면 뜨지 않는데, 만약 이런 경우 `open()`은 `null`을 리턴하기 때문에, 리턴값을 보고 팝업이 차단되어있는지 `if(open() == null)`로 확인하여 `alert()`나 다른 요소로 팝업 차단이 되었음을 사용자에게 알릴 수 있다.

그리고 팝업 창을 닫는 것은 브라우저의 창닫기를 해서 할 수도 있지만, `button`에 `onclick = "javascript:window.close()"`와 같이 작성하여 연결할 수도 있다.

# `document` 객체

웹 페이지마다 하나씩 있으며, `<body>` 태그를 만나면 만들어지고, `HTML 문서`의 정보가 담겨 있다.

# `navigator` 객체

해당 객체에는 웹 브라우저의 버전, 플러그인 설치 정보, 온/오프라인 등의 여러 `정보`가 들어있고, 이 정보는 사용자에게는 수정 권한 없이 웹 문서를 가져와서 보여줄 수만 있다.

웹 브라우저의 종류에 따라 웹 문서를 해석하고 실행하는 `랜더링 엔진`과 `자바스크립트 엔진`이 다르기 때문에, 모든 사용자에게 브라우저 상관없이 똑같은 웹 브라우저를 만들기 위해서는 사용자의 웹 브라우저 정보를 알아야 하기 때문에 `naviagtor` 객체를 이용한다.

예를 들어 아직 표준화되지 않은 CSS 속성 앞에는 브라우저 벤더를 의미하는 prefix를 지정한다. 

웹 브라우저의 정보를 파악할 때 `navigator.userAgent` 프로퍼티를 많이 이용하고, 해당 프로퍼티를 통해 사용자의 웹브라우저 정보를 알 수 있다. 요즘에는 같은 자바스크립트 엔진을 사용하는 브라우저가 많아져서 해당 프로퍼티는 사용하지 않는 추세인 것 같다.

# `history` 객체

브라우저에서 `뒤로`, `앞으로`, `주소 표시줄을 통해 이동` 한 사이트의 주소가 `배열` 형태로 저장되는 객체이다. 보안 문제 때문에 `read-only`이다.

# `location` 객체

브라우저의 주소 표시줄과 관련된 객체로, `location` 객체에는 현재 문서의 `URL 주소 정보`가 포함되어있다.

이 정보를 편집하거나 읽어와서 현재 브라우저 창에서 열어야 할 사이트나 문서를 지정할 수 있다. 예를 들어, `location.reload()`는 새로고침을 하는 메서드, `location.replace("URL")`은 입력한 URL로 주소를 대체하는 메서드이다.

`replace()`를 쓰면 현재 문서 자체가 대체되기 때문에 `뒤로` 버튼이 먹히지 않는다. (`assign()`은 같은 기능이지만 `history`를 기억)

## page 591 : 팝업 창에서 클릭한 내용을 메인 창에 나타내기

1. `main.html`에서 `doit-event.html` 파일을 팝업 창으로 열고, 해당 팝업의 `window`의 `creator`를 `main.html`으로 설정

```
var popWin = window.open("doit-event.html", "popup", "width=750, height=600");
popWin.creator = self;
```

2. 
  - 팝업을 `onclick`시 `loadURL(url)` 함수가 정의되도록 하고, 인수로 `this.href`를 전달 후, `return false;`로 기본 동작(링크 클릭시 `doit-main.html`로 이동)을 안하도록 설정
  - `loadURL` 함수를 정의하여 앞에서 설정한 `window.creator`의 `location`을 전달한 `url`로 설정 후, 현재 팝업을 `window.close();`로 닫기
  
  - 주의할 점은 `doit-event.html`에서 정의한 `loadURL()` 함수는 해당 파일 내에서만 호출할 수 있고, `main.html`에서 호출 불가능하다.
  - 그리고, `loadURL`에서 `window.creator.assign(url)`으로 하려고 했는데, `window.creator.location.assign(url);`로 해야한다.
  - 그 이유는 `assign()`은 `location` 객체의 `method`이기 때문이다.

```
<div id="container">
  <h1>이벤트 공지</h1>
  <img src="images/doit.jpg">
  <p><a href="doit-main.html" onclick="loadURL(this.href);return false;">자세히 보기</a></p>
</div>
<script>
  function loadURL(url) {
    window.creator.location = url;
    // window.creator.location.assign(url);
    window.close();
  }
</script>
```

# `screen` 객체

웹 브라우저에서 사용자의 화면 크기나 화면과 관련된 정보를 알아낼 때 사용하는 객체이다.

사용자의 화면 방향을 잠그는 `lockOrientation()`이나, 잠근 화면의 방향을 해제하는 `unlockOrientation()` 메서드를 많이 사용한다.

## page 595 : 팝업 창을 화면 가운데에 표시하기

```
<script>
  function openCenter(rel, name, w, h) {
    var left = (screen.availWidth - w) / 2;
    var top = (screen.availHeight - h) / 2;
    var opt = "left = " + left + ",top = " + top + ", width = " + w + ", height = " + h
    window.open(rel, name, opt);
  }

  openCenter("notice.html", "pop", 500, 400);
</script>
```

600 페이지에서 버튼을 클릭시 팝업 창을 화면 가운데에 표시하는 것은, `document.querySelector(#bttn).onclick = 함수이름`, 또는 `document.getElementById(bttn).onclick = 함수이름` 으로도 수행 가능
