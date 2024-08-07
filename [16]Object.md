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

2. `argument`가 2개인 경우 : 삭제할 시작 `index`와 삭제할 크기 `size`를 나타냄, 'index`를 포함하여 `size`개 만큼 요소가 삭제되고, 삭제된 요소들이 배열로 `return`됨

3. `argument`가 1개인 경우 : 삭제할 시작 `index`와 삭제할 크기 `size`와 추가할 요소 `value`를 나타냄. 
`index`를 포함하여 `size`개 만큼 요소가 삭제되고, `index` 위치에 `value`가 추가 됨. `size`가 `0`인 경우 `return` 되지 않고, 추가만 되며 `value` 자체를 배열로 나타내서 1개 이상 추가 가능


## `slice()` : 원하는 위치에 요소를 삭제 (추가하는건 `splice(index, 0, value)`로 하면 되기 때문에 추가는 없음)

`splice()`와 달리 기존 배열을 변경하지 않고 삭제할 만큼의 요소만 배열로 만들어서 `return` 함

1. `argument`가 1개인 경우 : 삭제할 시작 `index`를 나타냄, `index`를 포함하여 뒤의 모든 요소를 배열로 `return`함, 원래 배열은 바뀌지 않음

2. `argument`가 2개인 경우 : 삭제할 시작 `index`와 `size`가 아닌 `end index`을 나타냄. 범위가 `[,)` 이므로, `end index`를 포함하지 않고 배열로 `return`함, 똑같이 원래 배열은 바뀌지 안흥ㅁ


