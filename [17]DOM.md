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

