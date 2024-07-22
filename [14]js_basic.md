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
