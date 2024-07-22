- JS에서는 `switch` 문에서 문자열 사용 가능

- `prompt`는 입력 값을 문자열으로 받아들이므로, 숫자형으로 사용하기 위해서는 `Number(prompt(~));`를 해주거나, 정수형으로 사용하기 위해서는 `parseInt(prompt(~));`를 해줘야 함

- 문자열 계산은 `+` 만 연결 연산자로 받아들이고, 나머지는 전부 알아서 숫자형으로 변환되어서, 숫자형으로 계산되어 변수에 return 됨

- `===`와 `!==` 은 값 뿐만 아니라, 자료형까지 고려해서 판단
    - `3 === "3"` 은 `false` : 값은 같아서 `==` 에서는 `true` 이지만, 자료형이 다르기 때문에 `===`는 `false`
    - `3 !== "3"` 은 `true`  : 값은 같아서 `!=` 에서는 `false` 이지만, 자료형이 다르기 때문에 `!==`는 `false`

- 아래처럼, js 코드인 `document.write` 내에서 html 태그를 사용하여 css를 적용할 수 있음
```
for (i = 1; i <= 9; i++) {
	document.write("<div>");
	document.write("<h3>" + i + "단</h3>");
	for (j = 1; j <= 9; j++) {
		document.write(i +" X " + j + " = " + i*j + "<br>");
	}
	document.write("</div>");
}
```

### css 

- 아래는 바로 위의 구구단에 적용된 `css` 코드인데, `div`의 `display` 속성을 만약 `inline`으로 바꾼다면 `div`가 수평배치 되야 할 것 같다고 생각을 했음

- 하지만 `inline`은 기본적으로 텍스트로 취급되고, `div`를 `inline`으로 해줘도 `div` 자체가 `block`의 특성을 가지기 때문에 전체 너비를 가지려고 해서, `block`과 똑같이 배치되버림

- 따라서, `width`, `height`를 가지는 `inline-block`으로 해주거나, `float : left`를 해줘서 `block`의 특성을 무시해줘야함

```
div {
  display: inline-block;
  padding: 0 20px 30px 20px;
  margin: 15px;
  border: 1px solid #ccc;
  line-height: 2;
}

div h3 {
  text-align: center;
  font-weight: bold;
}
```
