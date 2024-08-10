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

# DOM에서 노드 추가, 삭제하기

처음에는 화면에 내용이 보이지 않다가, 버튼을 클릭하는 등의 이벤트가 발생하면 내용을 보여주는 동작을 만들 때, 앞에서 처럼 CSS의 `display` 속성을 바꿔서 만들 수 있지만, DOM 트리에 새로운 노드를 추가해서 해당 노드의 내용을 보여주는 방식을 사용할 수도 있다.

이때 주의할 점은 `요소 노드`를 추가할 때, 단순히 요소 노드 하나만 추가하는 것이 아니라 그 내부의 `텍스트 요소`나 `속성 노드`도 함께 추가해야 한다는 것이다.

이제 노드의 추가 과정을 살펴보자.

## 텍스트 노드를 사용하는 새로운 요소 노드를 추가하기

### 1. 요소 노드 만들기 : `document.createElement(노드명)`

예를 들어, `<p>` 태그를 가지는 요소 노드를 만들고 싶다면, `var newP = document.createElement("p");` 를 통해 새로운 요소 노드를 만들 수 있다.

### 2. 텍스트 노드 만들기 : `document.createTextNode(노드명)`

`<p>` 태그 내에는 텍스트 노드가 자식 노드로 들어가야 하기 때문에 `var textNode = document.createTextNode("텍스트 내용~~~");` 을 통해 새로운 텍스트 노드를 만들 수 있다.

### 3. 자식 노드 연결하기 : `부모노드.appendChild(자식노드)`

이제 `<p>` 태그에 텍스트 노드를 연결하고, 연결된 노드를 다시 원하는 위치의 `<div id = "info"></div>` 라는 부모 노드에 연결하기 위해서 2번 `appendChild()` 메서드를 사용하면 된다.

1. `newP.appendChild(textNode)`

2. `document.getElementById("info").appendChild(newP);`

## 4. [더보기]를 누르면, 해당 요소 노드가 추가되도록 소스 코드 완성하기

태그 내에 `onclick` 속성을 통해 `addP` 함수가 호출되도록 하였고, 한번 호출된 이후로 다시 [더보기]를 클릭하면 해당 요소가 여러번 추가되지 않게 하기 위해 `this.onclick ='';` 코드를 추가하였다.

태그 내에서 이벤트 처리기 함수를 등록할 때에는 태그 밖에서 `onclick=`이나 `addEventListener()`를 사용하는 방식과 달리 `addP();` 처럼 함수에 `()`를 추가로 작성해줘야 한다.

그리고, 태그 내에서 호출된 `addP()` 내부에서 `this`를 참조하면 `() => {}`로 래핑한 것과 같이 이벤트가 발생한 요소를 가리키지 않기 때문에, 태그 내에서 `this.onclick = '';`을 써줘야 한다.

참고로, `querySelectorAll`이나 `getElements~`와 같이 여러 개의 `노드 리스트`나 `HTMLCollection`을 리턴하는 경우, 내부에 요소가 1개만 존재하더라도 항상 `for`문을 통해 접근해야 한다.

```
<body>
  <div id="container">
    <h1>DOM을 공부합시다</h1>
    <a href="#" onclick="addP(); this.onclick='';">더 보기</a>
    <div id="info"></div>
  </div>
  <script>
    function addP() {
      var newP = document.createElement("p");
      var txtNode = document.createTextNode("DOM은 Document Object Model의 줄임말입니다.");
      newP.appendChild(txtNode);
      document.getElementById("info").appendChild(newP);
    }
  </script>
</body>
```

# 속성 값이 있는 새로운 요소 추가하기

![image](https://github.com/user-attachments/assets/0b9034c0-d189-4fd3-93b4-e3d62e231ffa)

## 1. 요소 노드 만들기 : `document.createElement(노드명)`

`var newImg = document.createElement("img");`

## 2. 속성 노드 만들기 : `document.createAttribute(속성명)`

예를 들어, `<img>` 태그에 `src` 속성 노드를 만들기 위해서는 `var srcNode = document.createAttribute("src");` 를 해준 후, `srcNode.value = "images/dom.jpg";` 처럼 다시 속성 값을 대입해줘야 한다.

## 3. 속성 노드 연결하기 : `요소명.setAttributeNode(속성노드)` 

요소 노드와 속성 노드는 자식 노드를 연결하는 방식처럼 `appendChild()` 메서드를 사용하여 연결하지 않고, `setAttribute()` 메서드를 통해 연결한다.

`newImg.setAttributeNode(srcNode);`와 같이 사용해주면 된다.

## 4. 자식 노드 연결하기 : `부모노드.appendChild(자식노드)`

마지막으로 위와 같이 `info`라는 `id`를 가지는 요소 노드에 `img` 요소 노드를 연결하기 위해 `document.getElementById("info").appendChild(newImg);` 를 통해 연결한다.

## 5. [더보기]를 누르면, 새로 추가한 `img` 요소 노드가 추가되도록 소스 코드 완성하기

```
<div id="container">    
    <h1>DOM을 공부합시다</h1>
    <a href="#" onclick="addContents(); this.onclick='';">더 보기</a>    
    <div id="info"></div>
  </div>
  <script>
    function addContents() {
      var newImg = document.createElement("img");
      var srcNode = document.createAttribute("src");
      var altNode = document.createAttribute("alt");
      srcNode.value = "images/dom.jpg";
      altNode.value = "돔 트리 예제 이미지";
      newImg.setAttributeNode(srcNode);
      newImg.setAttributeNode(altNode);

      document.getElementById("info").appendChild(newP);
      document.getElementById("info").appendChild(newImg);
    }
  </script>
```

## page 633 : 텍스트 필드에 입력한 값을 화면에 표시하기

1. `<form>` 태그에서 `subject`를 `id`로 가지는 `<input>` 태그에 입력한 값을 가지고 와서 `<ul>` 태그를 가지는 요소 노드에 `<li>` 태그를 가지는 새로운 요소 노드를 추가할 계획을 가지고 소스 코드를 작성한다.

2. `<input>` 태그 안에 사용자가 입력한 값이 존재하기 때문에 `subject` id명으로 접근하여, 해당 노드에 입력된 값인 `value`를 가져온 후, 텍스트 노드를 요소 노드에 추가한 후 `subject` 요소 노드에 해당 노드를 추가해준다.

3. `subject.value = "";` 으로 `click` 후에는 `value`를 이미 받아왔기 때문에 텍스트 필드에 사용자가 입력한 값은 지워준다.

4. `button` 클릭시 해당 이벤트 처리기가 등록되도록 아래에 등록한 후, `return false`는 원래 `<form>` 태그의 `<button>`의 기능인 submit 역할을 취소하기 위함이다.

```
var newItem = document.createElement("li");
var subject = document.getElementById("subject");
var newText = document.createTextNode(subject.value);

newItem.appendChild(newText);
document.getElementById("itemList").appendChild(newItem);
```


```
<body>
  <div id="container">
    <h1>Web Programming</h1>
    <p>공부할 주제를 기록해 보세요</p>
    <form action="">
      <input type="text" id="subject" autofocus>
      <button>추가</button>
    </form>
    <hr>
    <ul id="itemList"></ul>
  </div>
  <script>
    function newRegister() {
      var newItem = document.createElement("li");
      var subject = document.getElementById("subject");
      var newText = document.createTextNode(subject.value);

      newItem.appendChild(newText);
      document.getElementById("itemList").appendChild(newItem);

      subject.value = "";
    }

    var button = document.querySelector("button");
    button.onclick = () => {
      newRegister();
      return false;
    }
  </script>
</body>
```

### 참고 : `appendChild()`는 항상 노드 리스트의 제일 끝에 자식 노드를 추가하는데, `insertBefore()`를 사용하면 노드 리스트의 제일 앞에 추가해서, 제일 위에 마지막에 입력한 텍스트 필드의 값이 보이게 할 수 있다.

`itemList.appendChild(newItem);` -> `itemList.insertBefore(newItem, itemList.childNodes[0]);`

# 노드 삭제하기

DOM 트리에서 특정 노드를 삭제하기 위해서는, 무조건 부모 노드를 통해서 삭제해야 한다. 따라서, 먼저 부모 노드를 찾기 위한 프로퍼티가 필요하다.

## 부모 노드 찾기 : `자식노드.ParentNode`

해당 프로퍼티는 `parentNode` 프로퍼티이고, 찾고자 하는 노드에 `노드.parentNode`로 찾을 수 있다.

## 노드 삭제하기 : `부모노드.removeChild(자식노드)`

이후, `removeChild()` 메서드를 통해서 접근한 `노드.parentNode`에서 `노드.parent.removeChild(노드)`를 통해 해당 노드를 삭제하면 된다.

예를 들어, `li` 노드를 삭제하기 위해서는 `li.parentNode.removeChild(li)`로 삭제할 수 있다.

# page 638 : 입력한 항목을 클릭할 경우 삭제하기

1. `var li_list = document.querySelectorAll("li");` 를 통해 추가된 새로운 노드를 전부 `li_list`인 노드 리스트에 저장한다.

2. 새로운 노드가 추가될 때 마다 모든 노드에 `addEventListener` 메서드를 통해 `click`시 해당 노드가 삭제되도록 이벤트 처리기를 추가한다.
	- 앞에서 설명했듯이 익명 함수가 아닌 화살표 함수로 쓰면 `this`가 이벤트가 발생한 요소를 가리키지 못해서 익명 함수로 꼭 써줘야 함

```
function newRegister() {
  var newItem = document.createElement("li");  // 요소 노드 추가
  var subject = document.querySelector("#subject");  // 폼의 텍스트 필드
  var newText = document.createTextNode(subject.value);  // 텍스트 필드의 값을 텍스트 노드로 만들기
  newItem.appendChild(newText);  // 텍스트 노드를 요소 노드의 자식 노드로 추가

  var itemList = document.querySelector("#itemList");  // 웹 문서에서 부모 노드 가져오기 
  itemList.insertBefore(newItem, itemList.childNodes[0]);  // 자식 노드중 첫번째 노드 앞에 추가

  subject.value = "";

  var li_list = document.querySelectorAll("li");

  li_list.forEach(li => {
  li.addEventListener("click", function () {
    if (this.parentNode)
      this.parentNode.removeChild(this);
  })
});
}
```
