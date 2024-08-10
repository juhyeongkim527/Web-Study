# 문서 객체 모델 : DOM(Document Object Model)

자바 스크립트에서 사용자의 동작이나 어떤 조건에 의해 웹 문서의 요소들을 독립적으로 제어하여 반응하게 하기 위해서는, 각 요소들을 따로 구분하여 정보를 알고 있어야 한다.

**자바스크립트를 이용하여 웹 문서에 접근하고 제어할 수 있도록 객체를 사용해 웹 문서를 체계적으로 정리하는 방법**을 문서 객체 모델이라고 한다.

`HTML` 언어로 작성한 웹 문서의 DOM을 `HTML DOM`이라고 하며, `XML DOM`도 있지만 HTML DOM에 초점을 맞추어 설명을 한다.

`DOM`은 웹 문서 자체를 하나의 객체로 정의하고, 웹 문서 내부의 요소들도 각각 객체로 정의한다.

예를 들어 웹 문서 전체는 `document` 객체이고, 내부의 이미지 요소는 `image` 객체이다. 16장에서 본 브라우저 객체처럼 웹 문서에도 여러 `property`와 `method`가 존재한다.

## DOM Tree

DOM은 웹 문서의 요소를 부모 요소와 자식 요소로 구분한다. 문서 안의 요소 뿐만 아니라 `Text`와 같은 ***문서 안의 내용** 이나 ***속성*** 또한 자식으로 나타낸다.

예를 들어, `h1` 요소에서 사용한 `Do it`이라는 `Text`도 `h1` 요소의 자식 요소인 `text` 요소가 되고, `image` 요소의 `alt` 속성또한 자식 요소가 된다. 

트리의 각 요소를 `node`라고 하며, DOM Tree의 시작 노드인 `html` 노드를 `root` 노드라고 한다.

DOM을 구성하는 기본 원칙은 다음과 같다.

1. 모든 HTML 태그는 `요소(element) 노드`이다.

2. HTML 태그에서 사용하는 텍스트 내용은 자식 노드인 `텍스트(text) 노드`이다.

3. HTML 태그에 있는 속성은 자식 노드인 `속성(attribute) 노드`이다.

4. 주석은 `주석(comment) 노드`이다.

![image](https://github.com/user-attachments/assets/e25eb327-6fc9-4a94-bd2e-14392111427c)

# DOM 요소에 접근하고 속성 가져오기

## `id` 선택자로 접근하기 : `요소명.getElementById("id명")`

`id` 속성은 한 요소에만 사용할 수 있기 때문에 `argument`로 전달한 `id명`을 가지는 DOM 요소에 접근할 수 있다. 하나의 요소만 리턴하고, `HTMLCollection` 객체로 저장된다.

**`HTMLCollection` 객체는 배열과 비슷하고 사용법도 비슷하지만 배열과 완전히 똑같지는 않다.**

## `class` 선택자로 접근하기 : `요소명.getElementsByClassName("class명")`

`class` 선택자는 여러 요소에 중복하여 사용할 수 있기 때문에, 해당 메서드를 사용하면 여러개의 요소를 `HTMLCollection` 객체에 담아서 리턴하게 된다. 따라서, 이름도 `Elements`이다.

## `태그` 이름으로 접근하기 : `요소명.getElementsByTagName("태그명")`

`class`와 마찬가지로 `argument`로 전달된 태그 선택자를 가지는 여러 요소들이 `HTMLCollection` 객체에 담겨서 리턴되게 된다.

## 다양한 방법으로 접근하기 : `노드.querySelector("선택자")`, `노드.querySelectorAll("선택자 또는 태그")`

`argument`로 `id명`, `class명`, `태그명` 등 여러 요소를 전달해서 가져올 수 있다. `querySelector`는 요소가 중복될 경우 첫번째로 나오는 요소만 리턴하게 되고, `querySelectorAll`은 모든 요소를 리턴하게 된다.

`id`는 `#id명` 으로, `class`는 `.class명`으로 전달해서 구분해야하고, 태그의 경우 `태그명`으로 이름만 써주면 된다.

해당 메서드의 리턴 타입은 `노드` 이거나 `노드 리스트(node list)`이고, 이것 또한 배열과 비슷하지만 완전히 같은 것은 아니라고 생각하면 된다.

## 웹 요소의 내용을 수정 : `innerText`, `innerHTML`

앞에서도 많이 봤듯이 `querySelector`나 `getElement~` 메서드를 통해 요소를 가져온 후 `.inner~`를 붙여서 해당 요소의 내용을 수정할 수 있는 `property`이다.

`innerText`는 가져온 요소의 텍스트 내용만 가져오기 때문에 `HTML` 태그를 반영할 수 없고, `innerHTML`은 `HTML` 요소도 가져오기 때문에 `HTML` 태그를 반영할 수 있다.

`innerText`가 가져오는건 텍스트만 가져오지만, `innerText`에 대입을 할 때는 해당 요소 내의 `HTML` 요소를 전부 무시한 후 자식 요소를 모두 갈아끼우기 때문에 대입한 텍스트 요소만 남게된다.

예를 들어, 아래 함수에서 `innerText`를 쓰면, `<em>` 태그가 반영되지 않고 `<em>` 태그까지 그대로 출력되고, `innerHTML`을 쓰면 `<em>` 태그가 반영된다.

```
function inntext() {
  document.getElementById("current").innerText = "<em>" + now + "</em>";
}
function innhtml() {
  document.getElementById("current").innerHTML = "<em>" + now + "</em>";
}
```

<img width="546" alt="image" src="https://github.com/user-attachments/assets/3f3b48d2-1cb2-4967-9bd8-8ca9dddff738">
<img width="450" alt="image" src="https://github.com/user-attachments/assets/b43392b2-ca39-4645-8d99-1203e7adcf2c">

## 속성을 가져오기, 수정하기 : `getAttribute()`, `setAttribute()`

앞에서 웹 요소를 가져오는 방법으로 요소를 가져와서, 해당 요소의 속성 값을 가져오거나 수정할 수 있는 메서드이다. 단일 요소에만 메서드를 수행할 수 있기 때문에, `querySelectorAll`과 같은 메서드로 가져온 경우,

```
const items = document.querySelectorAll('.item');

// 각 요소에 대해 반복하며 "src" 속성을 가져옵니다. (<img> 태그의 속성이라고 가정)
items.forEach(item => {
    const value = item.getAttribute("src");
    console.log(value);
});
```

이러한 방식으로 반복문을 돌며 속성을 가져오거나 변경시켜야 한다.

# DOM 에서 이벤트 처리하기

웹 문서에서 이벤트가 발생하면 이벤트 처리기를 연결해야 한다. 예전에 배운 방식대로 태그 안에 `onclick` 속성을 통해 이벤트 처리기 함수나 동작을 직접 작성해도 되지만, 이렇게 되면 태그안에 내용이 너무 길어지거나 `js` 파일과 분리하기 힘든 단점이 있기 때문에 아래의 방식을 많이 사용한다.

## `DOM 요소`에 함수(이벤트 처리기) 직접 연결하기

예전에 사용했던 적이 있는데, `요소명.on+event이름 = 함수이름` 형식으로 사용할 수 있다.

아래와 같은 방식으로 `id`가 `cup`인 요소에 `click` 이벤트 발생시 익명 함수로 이벤트 처리기를 연결할 수도 있고, 아예 함수를 따로 선언하여 쓸 수도 있다.

함수를 아예 선언해서 쓸 때, 위에서도 얘기했지만, `parameter`를 전달하려면 `function() {함수 이름(paramter)}`으로 한번 래핑해줘야한다. 또는 `() => {함수 이름(paramter)}`와 같이 화살표 함수 형식으로 써도 된다.

근데, 이 부분은 더 공부해야 하겠지만, 익명 함수 대신 화살표 함수를 쓸 때는 `paramter`로 `this`를 전달하지 못하기 떄문에 `this`를 전달할 때는 익명함수를 써야된다. 익명 함수는 이벤트가 발생한 요소를 가리키지만, 화살표 함수는 lexical한 상위 요소를 가리키기 때문이다.

```
var cup = document.querySelector("#cup");  // id = cup인 요소를 가져옴
cup.onclick = function(){
  alert("이미지를 클릭했습니다");
}
```

그리고, 해당 방식으로 이벤트 처리기를 연결하면, `click` 이라는 이벤트에 `1개의 이벤트 처리기`만 연결할 수 있기 때문에 가장 마지막에 연결한 이벤트 처리기로 덮어씌워져서 여러개의 이벤트 처리기를 연결할 수 없다.

## `addEventListener()` 메서드를 사용하여 연결하기

`onclick`과 같이 `on+event이름`을 통해 이벤트 처리기를 연결하면, 요소 하나 당 1개의 이벤트 처리기만 연결할 수 있는데, `addEventListener` 메서드를 사용하면 한 요소에 `여러 개의 이벤트 처리기`를 연결할 수 있다.

`addEventListener("event이름", 이벤트 처리기, 캡처 여부);` 형식으로 사용하고 `;`를 꼭 마지막에 붙여야 한다. 이벤트 처리기에는 익명 함수도 사용할 수 있다.

`캡처 여부`는 기본 값이 `false`이며, `false`인 경우 발생한 이벤트가 자식 노드 -> 부모 노드로 전달되는 거고, `true`는 부모 노드 -> 자식 노드로 전달되는 것이다. 예를 들어 `false`인 경우 자식 노드에서 `click` 이벤트가 발생하면, 부모 노드에도 `click` 이벤트가 전달되어 부모 노드를 클릭하지 않았음에도 부모 노드의 `click`에 대한 이벤트 처리기가 같이 호출되는 것이다.

그리고, 이벤트 처리기에 `paramter`가 존재하는 경우, `function() {}`으로 래핑해주거나 `() => {}` 처럼 화살표 함수를 쓸 수 있다.

마찬가지로 유의할 점은 `this`와 관련된 `paramter`를 넘길 때는 익명 함수를 쓰는건 괜찮지만 화살표 함수로는 넘길 수 없기 때문에 이를 유의해야한다.

## `event` 객체

이벤트 정보를 저장하는 객체이다. 어떤 이벤트가 발생했는지에 대한 정보, 이벤트가 발생한 요소 등을 저장하고 있다. `event` 객체에는 여러 프로퍼티와 메서드가 존재한다.

`event` 객체는 이벤트의 정보와 이벤트가 발생한 요소의 이름은 가지고 있지만, 요소 자체는 가지고 있지 않기 때문에 이벤트가 발생한 요소에 접근하려면 `this` 키워드를 사용해야한다.

아래는 `event` 객체를 사용하여, `click`시 발생한 이벤트의 정보를 보여주는 예제이다.

```
<body>
	<div id="container">
    <img src="images/cup-1.png" id="cup">		
  </div>	

	<script>
		var cup = document.querySelector("#cup");  // id = cup인 요소를 가져옴
		cup.onclick = function(event) {
			alert("이벤트 유형: " + event.type + ", 이벤트 발생 위치 : " + event.pageX + "," + event.pageY);	
		}
	</script>
</body>
```

## `CSS 속성`에 접근하기 : `document.요소명.style.속성명`

요소를 가져온 후 `style.속성명`을 붙여서 `CSS 속성`에 접근할 수 있다. 일반 속성들은 `getAttribute`로 가져오지만 CSS 속성은 `.style`을 통해 가져와야 한다.

그리고 `background-color`처럼 하이픈이 붙은 속성들은 `backgroundColor`로 두번째 단어의 첫번째 문자를 대문자로 바꿔주면 된다.

아래는 `rect`라는 `class`를 가지는 요소 위로 마우스를 이동시켰을 때(`mouseover`, `mouseout` 이벤트), CSS 속성을 바꾸는 예제이다.

```
<body>
	<div id="container">
		<p>도형 위로 마우스 포인터를 올려놓으세요.</p>
		<div id="rect"></div>
	</div>	
	
	<script>
		var myRect = document.querySelector("#rect");
		myRect.addEventListener("mouseover", function() {  // mouseover 이벤트 처리
			myRect.style.backgroundColor = "green";  // myRect 요소의 배경색 
			myRect.style.borderRadius = "50%";  // myRect 요소의 테두리 둥글게 처리
		});
		myRect.addEventListener("mouseout", function() {  // mouseout 이벤트 처리
			myRect.style.backgroundColor = "";  // myRect 요소의 배경색 지우기 
			myRect.style.borderRadius = "";  // myRect 요소의 테두리 둥글게 처리 안 함
		});
	</script>
</body>
```

## page 620 : 라이트 박스 효과 만들기

1. `pic` 이라는 클래스를 가지는 요소들을 가져와서 `pics`에 저장한다.

2. `pics`에 저장된 `노드 리스트` 들을 순회하며, `addEventListener`를 통해 `click` 이벤트 발생 시 `showLightbox`라는 이벤트 처리기 함수를 등록해준다.
  - `forEach` 와 화살표 함수를 사용하였음

3. `showLightbox` 함수
     1. `this` 키워드를 통해 이벤트가 발생한 요소의 "data-src" 속성 값을 가져와서 `bigLocation`에 저장해준 후,
     2. `setAttribute`를 통해 `lightboxImage`의 `src` 속성을 `bigLocation`에 저장된 속성값으로 변경시켜준 후,
     3. 원래 보이지 않았던 `lightbox`의 요소를 `display` 속성을 변경시켜 보이게 해준다.

4. `lightbox` 요소가 다시 클릭되면, 보이지 않게 하기 위해 `click`시 `display`를 다시 안보이도록 바꿔주도록 이벤트 처리기를 등록해준다.
   
```
<body>
  <div class="row">
    <ul>
      <li><img src="images/tree-1-thumb.jpg" data-src="images/tree-1.jpg" class="pic"></li>
      <li><img src="images/tree-2-thumb.jpg" data-src="images/tree-2.jpg" class="pic"></li>
      <li><img src="images/tree-3-thumb.jpg" data-src="images/tree-3.jpg" class="pic"></li>
      <li><img src="images/tree-4-thumb.jpg" data-src="images/tree-4.jpg" class="pic"></li>
      <li><img src="images/tree-5-thumb.jpg" data-src="images/tree-5.jpg" class="pic"></li>
      <li><img src="images/tree-6-thumb.jpg" data-src="images/tree-6.jpg" class="pic"></li>
    </ul>
  </div>
  <div id="lightbox">
    <img src="images/tree-1.jpg" alt="" id="lightboxImage">
  </div>
  <script>
    var pics = document.querySelectorAll(".pic");
    var lightbox = document.getElementById("lightbox");
    var lightboxImage = document.getElementById("lightboxImage");

    lightbox.onclick = function () {
      this.style.display = "none";
    }

    pics.forEach(pic => {
      pic.addEventListener("click", showLightbox);
    })

    // for (var i = 0; i < pics.length; i++) {
    //   pic[i].addEventListener("click", showLightbox);
    // }

    function showLightbox() {
      var bigLocation = this.getAttribute("data-src");
      lightboxImage.setAttribute("src", bigLocation);
      lightbox.style.display = "block";
    }
  </script>
</body>
```
