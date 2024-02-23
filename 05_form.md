1. `<form></form>` 태그 안에 작성할 폼 작성
   - 옵션은 아래와 같이 여러가지가 있음
   - `method` : get, post처럼 http method 지정
   - `name` : **자바스크립트**로 폼을 제어할 때 사용할 폼 이름 지정
   - `action` : form 내용을 처리해 줄 **서버 프로그랭**믈 지정
   - `target` : action 속성 안에서 지정한 스크립트 파일을 다른 위치에서 열도록
2. `<form></form>` 태그 안에 `<fieldset></fieldset>` 폼 영역 구성
 - `<fieldset></fieldset>` 안에 `<legend></lengend>`로 영역 이름 설정
3. 안에 `<input>`이나 `<select>`태그로 여러 입력 설정
   - **`<label for = 'id'>`는 `<input id='id'>`에 연결하여 사용하고 input에 문자를 붙일 때 사용**
   - `<select>` 태그에는 `<option>` 태그가 들어가고 value로 서버에 값 전달 (selected 옵션 사용 가능)
   - `<input type = 'text' list='id'>`로 `<datalist id ='id'>`에 연결 가능
   - `<textarea>`는 input과 다르게 여러줄 가능
   - `value, required, auto, placeholder, checked, autofocus, selected` 등 여러가지 옵션 사용 가능
   - `value`는 어떤 type이 오느냐에 따라 다른데 대부분 text 타입이 아니면 **서버에 보낼 값**을 여기에 넣음  
ex) `<label>사과<input type = 'radio' name = 'fruits' value = 'apple'></label>` 또는 `<input type = 'text' value = 'default input value'>`
   - `radio`는 같은 `name` 옵션들과 엮어서 사용 (`checkbox`도 같은 `name`으로 묶음) ex) `<input type = 'radio' name ='test'>`
   - `<button>`은 `<input type = "submit | reset">`과 기능이 거의 동일하지만, `<form>` 밖에서 사용가능하고 css와 아이콘을 이용하여 꾸밀 수 있
