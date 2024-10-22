## 1. 변수

### 1) JavaScript 문법 학습 개요

- ECMAScript 2015 (ES6) 이후의 명제를 따름
- 권장 스타일 가이드
    https://standardjs.com/rules-kokr.html
    

### 2) 변수 작성 규칙

- 식별자 (변수명) 작성 규칙
    - 반드시 문자, 달러 `$` 또는 밑줄 `_` 로 시작
    - 대소문자를 구분
    - 예약어 사용 불가
        - for, if, function 등
- 식별자 (변수명) Naming case
    - 카멜케이스 (CamelCase)
    : 변수, 객체, 함수에 사용
    - 파스칼케이스 (PascalCase)
    : 클래스, 생성자에 사용
    - 대문자 스네이크 케이스 (SNAKE_CASE)
    : 상수(constants)에 사용

### 3) 변수 선언 키워드

### 3-1) `let`

- 블록스코프 (block scope)를 갖는 지역 변수를 선언
- **재할당 가능,** 재선언 불가능
- ES6에서 추가
- let은 선언 시 초기값이 없다면 undefined가 초기화시에 할당

```jsx
let number = 10  //1. 선언 및 초기값 할당
number = 20      //2. 재할당 가능
///////////////////////////////////////////
let number = 10  //1. 선언 및 초기값 할당
let number = 20  //2. 재선언 불가능
```

### 3-2) `const`

- 블록스코프를 갖는 지역 변수를 선언
- **재할당 불가능,** 재선언 불가능
- ES6에서 추가
- 선언 시 반드시 초기값 설정 필요

```jsx
// 1. 선언 및 초기값 할당
const number = 10

// 2. 재할당 불가능
number = 10

// 3. 재선언 불가능
const number = 20

// 선언 시 반드시 초기값 설정 필요
const number // const' declarations must be initialized
```

### 3-3) `var`

### 4) 블록 스코프 (block scope)

- if, for, 함수 등의 중괄호(`{}`) 내부를 가리킴
- 블록 스코프를 가지는 변수는 블록 바깥에서 접근 불가능

```jsx
let x = 1

if (x==1) {
  let x = 2
  console.log(x)   //2
}

console.log(x)     //1
```

### 5) 어떤 변수 선언 키워드를 사용해야 할까?

- const를 기본으로 사용
- 필요한 경우에만 let으로 전환
    - 재할당이 필요한 경우
    - let을 사용하는 것은 해당 변수가 의도적으로 변경될 수 있음을 명확히 나타냄
    - 코드의 유연성을 확보하면서도 const의 장점을 최대한 활용할 수 있음
- const를 기본으로 사용해야 하는 이유
    - 코드의 의도 명확화
        - 해당 변수가 재할당되지 않을 것임을 명확히 표현
        - 개발자들에게 변수의 용도와 동작을 더 쉽게 이해할 수 있게 해줌
    - 버그 예방
        - 의도치 않은 변수 값 변경으로 인한 버그를 예방
        - 큰 규모의 프로젝트나 팀 작업에서 중요

## 2. DOM

### 1) 개요

- 웹 브라우저에서의 JavaScript
- 웹 페이지의 동적인 기능을 구현

### 2) JavaScript 실행 환경 종류

- HTML script 태그
    
    ```html
    <body>
      <script>
        console.log('hello')
      </script>
    </body>
    ```
    
- js 확장자 파일
    
    ```jsx
    // hello.js
    console.log('Hello')
    ```
    
    ```html
    // index.html
    <body>
      <script src="hello.js"></script>
    </body>
    ```
    
- 브라우저 Console
  
    

### 3) Document structure

- HTML 문서는 상자들이 중첩된 형태로 볼 수 있음
- 브라우저가 문서를 표현하기 위해 사용하는 데이터 구조는 우측 이미지와 같은 모양을 가짐
- 각 상자는 객체이며 개발자는 이 객체와 상호작용하여 어떤 HTML 태그를 나타내는지, 어떤 콘텐츠가 포함되어 있는지 등을 알아낼 수 있음
- 이 표현을 Document Object Model, 또는 줄여 DOM이라고 부름

### 4) DOM

- The Document Object Model
- 웹 페이지(Document)를 구조화된 객체로 제공하여 프로그래밍 언어가 페이지 구조에 접근할 수 있는 방법을 제공
- 문서 구조, 스타일, 내용 등을 변경할 수 있도록 함
- DOM API
    - 다른 프로그래밍 언어가 웹페이지에 접근 및 조작할 수 있도록 페이지 요소들을 객체 형태로 제공하며 이에 따른 메서드 또한 제공

### 4-1) document 객체

- 웹페이지를 나타내는 DOM 트리의 최상위 객체
- HTML 문서의 모든 콘텐츠에 접근하고 조작할 수 있는 진입점
- DOM에서 모든 요소, 속성, 텍스트는 하나의 객체
- 모두 document 객체의 하위 객체로 구성됨
- 예시
    - HTML의 <title> 변경하기
    
    ```jsx
    document.title
    document.title = 'Hello :)'
    ```
    

### 4-2) DOM Tree

- HTML 태그를 나타내는 elements의 node는 문서의 구조를 결정
- 이들은 다시 자식 node를 가질 수 있음 (ex. document.body)
    - 객체 간 상속 구조가 존재

    

### 4-3) DOM 핵심

- 문서의 요소들을 객체로 제공하여 다른 프로그래밍 언어에서 접근하고 조작할 수 있는 방법을 제공하는 API

## 3. DOM 선택

### 1) DOM 조작 시 기억해야 할 것

> 웹페이지를 동적으로 만들기 == 웹페이지를 조작하기
> 
- 조작 순서
: 조작하고자 하는 요소를 **선택** (또는 탐색) → 선택된 요소의 콘텐츠 또는 속성을 **조작**

### 2) 선택 메서드

- `document.querySelector(selector)`
    - 요소 한 개 선택
    - 제공한 선택자와 일치하는 element 한 개 선택
    - 제공한 선택자를 만족하는 첫 번째 element 객체를 반환 (없다면 null 반환)
- `document.querySelectorAll(selector)`
    - 요소 여러 개 선택
    - 제공한 선택자와 일치하는 여러 element를 선택
    - 제공한 선택자를 만족하는 NodeList를 반환
- 실습

```jsx
<!-- selecthtml -->

<body>
  <h1 class="heading">DOM 선택</h1>
  <a href="https://www.google.com/">google</a>
  <p class="content">content1</p>
  <p class="content">content2</p>
  <p class="content">content3</p>
  <ul>
    <li>list1</li>
    <li>list2</li>
  </ul>

  <script>
    console.log(document.querySelector('.heading'))
    console.log(document.querySelector('.content'))
    console.log(document.querySelectorAll('.content'))
    console.log(document.querySelectorAll('ul > li'))
  </script>
</body>

</html>

```


## 4. DOM 조작

### 1) 속성 (attribute) 조작

- 클래스 속성 조작 메서드 `classList` property
: 요소의 클래스 목록을 DOMTokenList(유사배열) 형태로 반환
    - `element.classList.add()` : 지정한 클래스 값을 추가
    - `element.classList.remove()` : 지정한 클래스 값을 제거
    - `element.classList.toggle()`  : 클래스가 존재한다면 제거하고 false를 반환 (존재하지 않으면 클래스를 추가하고 true를 반환)
    - 실습 : add()와 remove()메서드를 사용해 클래스 값을 추가 혹은 제거
        
        ```jsx
        // 속성 요소 조작
        
        // 1. 클래스 속성 조작
        // h1 요소를 선택
        const h1Tag = document.querySelector('.heading')
        // h1 요소의 클래스 목록 확인
        console.log(h1Tag.classList)
        
        // h1 요소의 클래스 목록에 red 클래스 추가
        h1Tag.classList.add('red')
        console.log(h1Tag)
        console.log(h1Tag.classList)
        
        // h1 요소의 클래스 목록에 red 클래스 삭제
        h1Tag.classList.remove('red')
        console.log(h1Tag.classList)
        
        console.log(h1Tag.classList.toggle('red'))
        console.log(h1Tag.classList)
        ```
        
- 일반 속성 조작 메서드
    - `Element.getAttribute()` : 해당 요소에 지정된 값을 반환 (조회). 없으면 null값
    - `Element.setAttribute(name, value)`
        - 지정된 요소의 속성 값을 설정
        - 속성이 이미 있으면 기존 값을 갱신 (그렇지 않으면 지정된 이름과 값으로 새 속성이 추가)
    - `Element.removeAttribute()` : 요소에서 지정된 이름을 가진 속성 제거
    - 실습
        
        ```
        // 2. 일반 속성 조작
        // a 요소 선택
        const aTag = document.querySelector('a')
        console.log(aTag.getAttribute('href'))
        
        // a 요소의 href 속성 값을 naver로 변경
        aTag.setAttribute('href', 'https://www.naver.com/')
        console.log(aTag.getAttribute('href'))
        
        // a 요소의 href 속성 값 삭제
        aTag.removeAttribute('href')
        console.log(aTag.getAttribute('href'))
        ```
        

### 2) HTML 콘텐츠 조작

- `textContent` property : 요소의 텍스트 콘텐츠를 표현
- 실습
    
    ```jsx
    // HTML 콘텐츠 조작
    // h1 요소 선택
    const h1Tag = document.querySelector('.heading')
    console.log(h1Tag.textContent)
    
    // h1 요소의 콘텐츠 값을 변경
    h1Tag.textContent = '내용 수정'
    console.log(h1Tag.textContent)
    ```
    

### 3) DOM 요소 조작

- `document.createElement(tagname)` : 생성
    - 작성한 tagname의 HTML 요소를 생성하여 반환
- `Node.appendChild()` : 추가
    - 한 Node를 특정 부모 Node의 자식 NodeList 중 마지막 자식으로 삽입
    - 추가된 Node 객체를 반환
- `Node.removeChild()` : 삭제
    - DOM에서 자식 Node를 제거
    - 제거된 Node를 반환
- 실습
    
    ```
    // 생성
    const h1Tag = document.createElement('h1')
    // console.log(h1Tag)
    h1Tag.textContent = '제목'
    console.log(h1Tag)
    
    // 추가
    const divTag = document.createElement('div')
    divTag.appendChild(h1Tag)
    console.log(divTag)
    
    // 삭제
    const pTag = document.querySelector('p')
    divTag.removeChild(pTag)
    console.log(pTag)
    
    ```
    

### 4) 스타일 조작

- `style` property : 해당 요소의 모든 속성 목록을 포함하는 속성
- style 조작 실습
    
    ```jsx
    const pTag = document.querySelector('p')
    
    console.log(pTag.style)
    pTag.style.color = 'crimson'
    pTag.style.fontSize = '3rem'
    pTag.style.border = '2px solid black'
    ```
    

## 5. 참고
### 1) DOM 속성 확인 Tip

- 개발자도구 - Elements  Properties
- 선택한 해당 요소의 모든 DOM 속성 확인 가능


### 2) Node

- DOM의 기본 구성 단위
- DOM 트리의 각 부분은 Node라는 객체로 표현됨
    - Document Node ⇒ HTML 문서 전체를 나타내는 노드
    - Element Node ⇒ HTML 요소를 나타내는 노드 (예를 들어 <p>)
    - Text Node ⇒ HTML 텍스트 (Element Node 내의 텍스트 컨텐츠를 나타냄)
    - Attribute Node ⇒ HTML 요소의 속성을 나타내는 노드

### 3) NodeList

- DOM 메서드를 사용해 선택한 Node의 목록
- 배열과 유사한 구조를 가짐
- Index로만 각 항목에 접근 가능
- JavaScript의 배열 메서드 사용 가능
- `querySelectorAll()` 에 의해 반환되는 NodeList는 DOM의 변경사항을 실시간으로 반영하지 않음
    - DOM이 나중에 변경되더라도 이전에 이미 선택한 NodeList 값은 변하지 않음

### 4) Element

- Node 하위 유형
- Element는 DOM 트리에서 HTML 요소를 나타내는 특별한 유형의 Node
- 예를 들어 p, div, span, body 등의 HTML 태그들이 Element 노드를 생성
- Node의 속성과 메서드를 모두 가지고 있으며 추가적으로 요소 특화된 기능 (ex. className, innerHTML, id 등)을 가지고 있음
- 모든 Element는 Node이지만, 모든 Node가 Element인 것은 아님

### 5) 변수 선언 키워드 `var`

- ES6 이전에 변수 선언에 사용했던 키워드
- 재할당 가능, 재선언 가능
- 함수 스코프 (function scopre)를 가짐
- “호이스팅”되는 특성으로 인해 예기치 못한 문제 발생 가능
    - 선언하기 전 사용할 수 있음
- 변수 선언 시  var, const, let 키워드 중 하나를 사용하지 않으면 자동으로 var 선언됨

### 6) 함수 스코프 (function scope)

- 함수의 중괄호 내부를 가리킴
- 함수스코프를 가지는 변수는 함수 바깥에서 접근 불가능

```jsx
functon foo() {
  var x = 1
  console.log(x)  // 1
}

console.log(x)  //ReferenceError : x is not defined
```

### 7) 호이스팅 (hoisting)

- 변수 선언이 끌어올려지는 현상
    - var로 선언한 변수는 선언 위치와 상관없이 함수 시작 지점. 전역에서는 코드가 시작될 때 처리됨
    - 변수에 무언가를 할당하기 전까진 undefined를 가짐
    
    ```jsx
    console.log(name)  // undefined
    var name = '홍길동' // 선언 및 할당
    ```
    
    ```jsx
    // 위 코드와 동일하게 동작
    var name
    console.log(name) // undefined
    
    var name = '홍길동'
    ```