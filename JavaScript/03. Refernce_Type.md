# [JS] 참조 자료형 01

# ReferenceType

## 1.  함수 Function

- 참조 자료형에 속하며 모든 함수는 Function object

### 1) 함수 구조

```jsx
function name ([param[, param, [..., param]]]) {
	tatements
	return value
}
```

- function 키워드
- 함수의 이름
- 함수의 매개변수
- 함수의 body를 구성하는 statements
- return 값이 없다면 undefined를 반환

### 2) 함수 정의 2가지 방법

- **선언식 (function declaration)**
    - 예시
        
        ```jsx
        function funcName () {
        	statements
        }
        ```
        
        ```jsx
        function add (num1, num2) {
        	return num1 + num2
        }
        
        add(1, 2)  // 3
        ```
        
    - 호이스팅 됨
        
        ```jsx
        // 이 코드도 오류가 안남
        
        add(1, 2)  // 3
        
        function add (num1, num2) {
        	return num1 + num2
        }
        ```
        
        - 선언이 끌어올려 짐
    - 코드의 구조와 가독성 면에서는 표현식에 비해 장점이 있음
- **표현식 (function expression)**
    - 예시
        
        ```jsx
        const funcName = function () {
        	statements
        }
        ```
        
        ```jsx
        const sub = function (num1, num2) {
        	return num1 - num2
        }
        
        sub(2, 1)  // 1
        ```
        
    - 호이스팅 되지 않음
        
        ```jsx
        // ReferenceError : Cannot access 'sub' before initialization
        console.log(sub(2, 1))  // 1
        
        const sub = function (num1, num2) {
        	return num1 - num2
        }
        ```
        
        - 변수 선언만 호이스팅되고 함수 할당은 실행 시점에 이루어짐
    - 함수 이름이 없는 ‘익명 함수’를 사용할 수 있음
- 함수 표현식 사용을 권장!! 하는 이유
    - 예측 가능성
    : 호이스팅의 영향을 받지 않아 코드의 실행 흐름을 더 명확하게 예측할 수 있음
    - 유연성
    : 변수에 할당되므로 함수를 값으로 다루기 쉬움
    - 스코프 관리
    : 블록 스코프를 가지는 `let`이나 `const`와 함께 사용하여 더 엄격한 스코프 관리가 가능

### 3) 매개변수

- 매개변수 정의 방법
    - 기본 함수 매개변수
    - 나머지 매개변수

### 3-1) 기본 함수 매개변수 (Default function parameter)

- 전달하는 인자가 없거나 undefined가 전달될 경우 이름 붙은 매개변수를 기본값으로 초기화
    
    ```jsx
    const greeting = function (name = 'Anonymous') {
    	return `Hi ${name}`
    }
    
    console.log(greeting())
    ```
    

### 3-2) 나머지 매개변수 (Rest parameters)

- 임의의 수의 인자를 ‘배열’로 허용하여 가변 인자를 나타내는 방법
- 작성 규칙
    - 함수 정의 시 나머지 매개변수는 하나만 작성할 수 있음
    - 나머지 매개변수는 함수 정의에서 매개변수 마지막에 위치해야 함.

```jsx
const myFunc = function (param1, param2, ...restPrams) {
	rerturn [param1, param2, restParams]
}

console.log(myFunc(1, 2, 3, 4, 5))  // [1, 2, [3, 4, 5]]
console.log(myFunc(1, 2))  // [1, 2, []]
```

- 매개변수와 인자 개수의 불일치를 허용한다.
    - 매개변수 개수 > 인자 개수
    ⇒ 누락된 인자는 undefined로 할당. 오류 ❌
        
        ```jsx
        const threeArgs = function (param1, param2, param3) {
        	return [param1, param2, param3]
        }
        
        console.log(threeArgs())  // [undefined, undefined, undefined]
        console.log(threeArgs(1))  // [1, undefined, undefined]
        console.log(threeArgs(2, 3))  // [2, 3, undifined]
        ```
        
    - 매개변수 개수 < 인자 개수
    ⇒ 초과 입력한 인자는 사용하지 않음. 그냥 무시함!!. 오류 ❌
        
        ```jsx
        const noArgs = function () {
        	return 0
        }
        console.log(noArgs(1, 2, 3))  // 0
        
        const twoArgs = function (param1, param2) {
        	return [param1, param2]
        }
        console.log(twoArgs(1, 2, 3))  // [1, 2]
        ```
        

### 4) Spread syntax (`...`, 전개구문)

- 배열이나 문자열과 같이 반복 가능한 항목을 펼치는 것. (확장, 전개)
- 전개 대상에 따라 역할이 다름
    - 배열이나 객체의 요소를 개별적인 값으로 분리
    - 다른 배열이나 객체의 요소를 (풀어내서) 현재 배열이나 객체에 추가 등
- 전개구문 활용처
    - 함수와의 사용
        - 함수 호출 시 인자 확장
        - 나머지 매개변수 (압축)
    - 객체와의 사용 → 나중에 객체파트에서 진행
    - 배열과의 활용 → 나중에 배열파트에서 진행
- 전개구문 활용 (함수와의 사용)
    - 인자 확장 (함수 호출 시)
        
        ```jsx
        function myFunc(x, y, z) {
        	return x + y + z
        }
        
        let numbers = [1, 2, 3]
        console.log(myFunc(...numbers))  // 6
        // 개수는 맞아야 함.
        ```
        
    - 나머지 매개변수 (함수 선언 시)
        
        ```jsx
        function myFunc2(x, y, ...restArgs) {
        	return [x, y, restArgs]
        }
        
        console.log(myFunc2(1, 2, 3, 4, 5))  // [1, 2, [3, 4, 5]]
        console.log(myFunc2(1, 2)) // [1, 2, []]
        ```
        

### 5) 화살표 함수 표현식

- 함수 표현식의 간결한 표현볍
    
    ```jsx
    const arrow = function (name) {
    	return `hello, ${name}`
    }
    ```
    
    ```jsx
    const arrow = name => `hello, ${name}`
    ```
    
- 작성 과정
    - 1단계
    : function 키워드 제거 후 매개변수와 중괄호 사이에 화살표 `=>` 작성
    - 2단계
    : 함수의 매개변수가 하나 뿐이라면, 매개변수의 `()` 제거 가능
    (단, 생략하지 않는 것을 권장)
    - 3단계
    : 함수 본문의 표현식이 한 줄이라면, `{}` 와 `return` 제거 가능
        
        ```jsx
         const arrow1 = function (name {
        	return `hello, ${name}`
        }
        
        // 1차 변경 : function 키워드 삭제 후 화살표 작성
        const arrow2 = (name) => {return `hello, ${name}`}
        
        // 2차 변경 : 인자의 소괄호 삭제 (인자가 1개일 경우에만 가능)
        const arrow3 = name => {return `hello, ${name}`}
        
        // 3차 변경 : 함수 본문이 return을 포함한 표현식 1개일 경우에만 가능
        const arrow4 = name => `hello, ${name}`
        ```
        
- 화살표 함수 심화
    
    ```jsx
    // 1. 인자가 없다면 () or _ 로 표시 가능
    const noArgs1 = () => 'No args'
    const noArgs2 = _ => 'No args'
    
    // 2-1 object를 return한다면 return을 명시적으로 작성해야 함
    const returnObject1 = () => { return { key: 'value' } }
    
    // 2-2 return을 작성하지 않으려면 객체를 소괄호로 감싸야 함.
    const returnObject2 = () => ({key: 'value'})                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    
    ```
    

## 2. 객체 (object)

- 키로 구분된 데이터 집합을 저장하는 자료형

### 1) 구조 및 속성

### 1-1) 객체 구조

- 중괄호 (`{}`)를 이용해 작성
- 중괄호 안에는 `key: value` 쌍으로 구성된 속성 (property)를 여러 개 작성 가능
- key는 문자형만 허용
- value는 모든 자료형 허용
- 예시
    
    ```jsx
    const user = {
      name: 'Alice',
      'key with space': true,
      greeting: function () {
        return 'hello'
      }
    }
    ```
    

### 1-2) 속성 참조

- 점(`.` , chaining operator) 또는 대괄호 (`[]`)로 객체 요소 접근
- key 이름에 띄어쓰기 같은 구분자가 있으면 대괄호 접근만 가능 !!
- 조회
    
    ```jsx
    // 조회
    console.log(user.name) // Alice
    console.log(user['key with space']) // true
    ```
    
- 추가
    
    ```jsx
    // 추가
    user.address = 'korea'
    console.log(user) // {name: 'Alice', key with space: true, address: 'korea', greeting: ƒ}
    
    ```
    
- 수정
    
    ```jsx
    // 수정
    user.name = 'Bella'
    console.log(user.name) // Bella
    
    ```
    
- 삭제
    
    ```jsx
    // 삭제
    delete user.name
    console.log(user) // {key with space: true, address: 'korea', greeting: ƒ}
    ```
    
- `in` 연산자
: 속성이 객체에 존재하는지 여부를 확인
    
    ```jsx
    	
    // in 연산자
    console.log('greeting' in user) // true
    console.log('country' in user) // false
    ```
    

### 2) 메서드

- 객체 속성에 정의된 함수
- Method 사용 예시
    - `object.method()` 방식으로 호출
    - 메서드는 객체를 ‘행동’할 수 있게 함
    
    ```jsx
    console.log(user.greeting())  // hello
    ```
    

### 3) `this` keyword

- 객체에 대한 특정한 작업을 수행할 수 있음
- 함수나 메서드를 호출한 객체를 가리키는 키워드
- 함수 내에서 객체의 속성 및 메서드에 접근하기 위해 사용
- Method & this 사용 예시
    
    ```jsx
    // Method & this 예시
    const person = {
      name: 'Alice',
      greeting: function () {
        return `Hello my name is ${this.name}`
      },
    }
    
    console.log(person.greeting()) // Hello my name is Alice
    ```
    

### 3-1) 함수를 `호출하는 방법` 에 따라 가리키는 대상이 다름

| 호출 방법 | 대상 |
| --- | --- |
| 단순 호출 | 전역 객체 (window 라는 객체) |
| 메서드 호출 | 메서드를 호출한 객체 |
- 단순 호출 시 `this` 
: 가리키는 대상 ⇒ 전역객체
    
    ```jsx
    // 1.1 단순 호출 시 this
    const myFunc = function () {
      return this
    }
    console.log(myFunc()) // window
    ```
    
    - 만약 밑에 호출하는 console.log  코드가 없으면 ???
    → this는 무엇을 가리키는지 아직 모른다 !!!
- 메서드 호출 시 `this` 
: 가리키는 대상 ⇒ 메서드를 호출한 객체
    
    ```jsx
    const myObj = {
      data: 1,
      myFunc: function () {
        return this
      }
    }
    console.log(myObj.myFunc()) // myObj
    ```
    

### 3-2) 중첨된 함수에서의 `this` 문제점과 해결책

- 문제점
    
    ```jsx
    const myObj2 = {
      numbers: [1, 2, 3],
      myFunc: function () {
        this.numbers.forEach(function (number) {
          console.log(this) // window
        })
      }
    }
    console.log(myObj2.myFunc())
    ```
    
    - 첫번째 this 메소드로서 호출되고 있기 때문에 this는 myObj2를 가르킴
    - 두번째 this : 일반적인 함수 호출이기 때문에 this가 window를 가르킴
    - 콜백함수 : 어떤 인자로 들어가게 되는 함수. numbers가 3개기 때문에 forEach함수가 3번 호출됨
- 해결책
    
    ```
    const myObj3 = {
      numbers: [1, 2, 3],
      myFunc: function () {
        this.numbers.forEach((number) => {
          console.log(this) // myObj3
        })
      }
    }
    console.log(myObj3.myFunc())
    ```
    
    - 화살표 함수는 자신만의 this를 가지지 않기 때문에 외부 함수 (myFunc)에서의 this 값을 가져옴.
    - 화살표함수는 부모의 this 값을 허용함
    - 저 함수의 부모는 `function()` . 저 친구의 tihs는 myObj3이다.

### 3-3) JavaScript `this` 정리

- JavaScript의 함수는 호출될 때 this를 암묵적으로 전달받음
- JavaScript에서 this는 함수가 ‘**호출되는 방식**’에 따라 결정되는 현재 객체를 나타냄
- Python의 self와 Java의 this가 선언 시 이미 값이 정해지는 것에 비해
↔ JavaScript의 this는 함수가 **호출되기 전까지 값이 할당되지 않고 호출 시에 결정**됨 (동적 할당)
- this가 미리 정해지지 않고 호출 방식(2가지)에 의해 결정되는 것의
    - 장점
    : 함수 (메서드)를 하나만 만들어 여러 객체에서 재사용 가능
    - 단점
    : 이런 유연함이 실수로 이어질 수 있다는 것

### 4) 추가 객체 문법

### 4-1) 단축 속성

- 키 이름과 값으로 쓰이는 변수의 이름이 같은 경우 단축 구문 사용 가은

```jsx
const name = 'Alice'
const age = 30

// 일반적 방법
const user1 = {
  name: name,
  age: age
}

// 단축 구문
const user2 = {
  name,
  age,
}

```

### 4-2) 단축 메서드

- 메서드 선언 시 `functon` 키워드 생략 가능

```jsx
const myObj1 = {
  myFunc: function () {
    return 'Hello'
  }
}

// 단축 메서드
const myObj2 = {
  myFunc() {
    return 'Hello'
  }
}
```

### 4-3) 계산된 속성 (Computed Property Name)

- 키가 대괄호 `[]` 로 둘려싸여 있는 속성
- 고정된 값이 아닌 변수 값 사용 가능
→ key를 유연하게 바꿀 수 있다.

```jsx

// 3. 계산된 속성
const product = prompt('물건 이름을 입력해주세요')
const prefix = 'my'
const suffix = 'property'

const bag = {
  [product]: 5,
  [prefix + suffix]: 'value',
}

console.log(bag) // {연필: 5, myproperty: 'value'}
```

### 4-4) 구조 분해 할당 (destructing assignment)

- 알고 있으면 잘 활용 가능 !!
- 배열 또는 객체를 분해하여 객체 속성을 변수에 쉽게 할당할 수 있는 문법

```jsx
const userInfo = {
  firstName: 'Alice',
  userId: 'alice123',
  email: 'alice123@gmail.com'
}

const firstName = userInfo.name
const userId = userInfo.userId
const email = userInfo.email

const { firstName } = userInfo  // 이게 동작하려면, userInfo 배열에 key가 같아야 함.
const { firstName, userId } = userInfo
const { firstName, userId, email } = userInfo  // 변수 세개가 탄생한 것 !!

console.log(firstName, userId, email)
```

- 함수의 ‘매개변수’로 객체 구조 분해 할당 활용 가능
    
    ```jsx
    const person = {
      name: 'Bob',
      age: 35,
      city: 'London',
    }
    
    function printInfo({ name, age, city }) {
      console.log(`이름: ${name}, 나이: ${age}, 도시: ${city}`)
    }
    
    printInfo(person)
    ```
    

### 4-5) object with ‘전개 구문

- `객체 복사` : 객체 내부에서 객체 전개
- 얕은 복사에 활용 가능

```jsx
const obj = { b: 2, c: 3, d: 4 }
const newObj = {a:1, ...obj, e: 5}
console.log(newObj) // {a: 1, b: 2, c: 3, d: 4, e: 5}
```

### 4-6) 유용한 객체 메서드

- `Object.keys()`
- `Object.values()`

```jsx
const profile = {
  name: 'Alice',
  age: 30
}

console.log(Object.keys(profile)) // ['name', 'age']
console.log(Object.values(profile)) // ['Alice', 30]
```

### 4-7) Optional chaining (`?.`)

- 속성이 없는 중첩 객체를 에러 없이 접근할 수 있는 방법
- 만약 참조 대상이 null 또는 undefined라면 에러가 발생하는 것 대신 평가를 멈추고 undefined를 반환

```jsx
const user = {
  name: 'Alice',
  greeting: function () {
    return 'hello'
  }
}

console.log(user.address.street)
// Uncaught TypeError: Cannot read properties of undefined (reading 'street')

console.log(user.address?.street)  // undefined : 에러가 발생하지 않음

console.log(user.nonMethod()) // Uncaught TypeError: user.nonMethod is not a function
console.log(user.nonMethod?.())  // undefined : 에러가 발생하지 않음

```

- 만약 Optional chaining을 사용하지 않는다면 다음과 같이 `&&` 연산자를 사용해야 함
    
    ```jsx
    const user = {
      name: 'Alice',
      greeting: function () {
        return 'hello'
      }
    }
    
    // 아래 예시 코드 논리상 user는 반드시 있어야 하지만 address는 필수 값이 아님
    // user에 값을 할당하지 않은 문제가 있을 때 바로 알아낼 수 있어야 하기 때문
    console.log(user.address && user.address.street) // undefined
    ```
    
- 장점
    - 참조가 누락될 가능성이 있는 경우 연결된 속성으로 접근할 때 더 짧고 간단한 표현식을 작성할 수 있음
    - 어떤 속성이 필요한지에 대한 보증이 확실하지 않는 경우에 객체의 내용을 보다 편리하게 탐색할 수 있음
- 주의사항
    - Optional chaining은 존재하지 않아도 괜찮은 대상에만 사용해야 함. (남용X)
        - 왼쪽 평가대상이 없어도 괜찮은 경우에만 선택적으로 사용
        - 중첩 객체를 에러 없이 접근하는 것이 사용 목적이기 때문
        
        ```jsx
        // 아래 예시 코드 논리상 user는 반드시 있어야 하지만 address는 필수 값이 아님
        // user에 값을 할당하지 않은 문제가 있을 때 바로 알아낼 수 있어야 하기 때문
        
        // Bad
        user?.address?.street
        
        // Good
        user.address?.street
        ```
        
    - Optional chaining 앞의 변수는 반드시 선언되어 있어야 함
        
        ```jsx
        console.log(myObj?.address)  // Uncaught ReferenceError: myObbj is not defined
        ```
        
- Optional chaining 정리
    - `obj.prop` : obj가 존재하면 `obj.prop`을 반환하고 그렇지 않으면 undefined 반환
    - `obj?.[prop]` : obj가 존재하면 `obj[prop]`을 반환하고, 그렇지 않으면 undefined 반환
    - `obj?.method()` : obj가 존재하면 `obj.method()` 를 호출하고, 그렇지 않으면 undefined 반환

### 5) JSON

- JavaScript Object Notation
- key-value 형태로 이루어진 자료 표기법
- JS 의 Object와 유사한 구조를 가지고 있지만
JSON은 형식이 있는 문자열
- JS에서 JSON을 사용하기 위해서는 Object 자료형으로 변경해야 함
- Object ↔ JSON 변환하기
    
    ```jsx
    const jsObject = {
      coffee: 'Americano',
      iceCream: 'Cookie and cream'
    }
    
    // Object -> JSON
    const objToJson = JSON.stringify(jsObject)
    console.log(objToJson)  // {"coffee":"Americano","iceCream":"Cookie and cream"}
    console.log(typeof objToJson)  // string
    
    // JSON -> Object
    const jsonToObj = JSON.parse(objToJson)
    console.log(jsonToObj)  // { coffee: 'Americano', iceCream: 'Cookie and cream' }
    console.log(typeof jsonToObj)  // object
    ```
    

### 6) 참고 - 클래스

- 객체를 생성하기 위한 템플릿
- 객체의 속성, 메서드를 정의하는 청사진 역할
- 클래스 기본 문법
    - class 키워드
    - 클래스 이름
    - 생성자 메서드 `constructor()`
    
    ```jsx
    class MyClass {
    	// 여러 메서드를 정의할 수 있음
    	constructor() {...}
    	method1() { }
    	method2() { }
    	method3() { }
    	...
    }
    ```
    

- 클래스 특징
    - ES6에서 도입
    - 생성자 함수를 사용하여 객체를 생성하는 이전의 방식을 객체 지향적으로 표현하고자 만들어짐
    - 그래서 클래스는 내부적으로 생성자 함수를 기반으로 동작함
    
    ```jsx
    // [참고] : 생성자 함수 표현 방식 (과거)
    function Member(name, age) {
      this.name = name
      this.age = age
      this.sayHi = function () {
        console.log(`Hi, I am ${this.name}`)
      }
    }
    ```
    
    ```jsx
    // 클래스 (현재)
    class Member {
    	constructor(name, age) {
    		this.name = name
    		this.age = age
    	}
    	sayHi() {
    		console.log(`Hi, I am ${this.name}`)
    	}
    }
    
    const member3 = new Member('Alice', 20)
    
    console.log(member3)  // Member {name: 'Alice', age: 20 }
    console.log(member3.name)  // Alice
    member3.sayHi()  // Hi I am Alice
    ```
    

## 3. 배열

- Object : 키로 구분된 데이터 집합을 저장하는 자료형. ⇒ 이제는 순서가 있는 collection이 필요
- Array : 순서가 있는 데이터 집합을 저장하는 자료구조
- 배열 구조
    - 대괄호 `[]` 를 이용해 작성
    - 요소의 자료형은 제약 없음
    - `length` 속성을 사용해 배열에 담긴 요소 개수 확인 가능

```jsx
const names = ['Alice', 'Bella', 'Cathy']

// 요소 조회
console.log(names[0]) // Alice
console.log(names[1]) // Bella
console.log(names[2]) // Cathy

// 길이
console.log(names.length) // 3

// 수정
names[0] = 'Gahee'
console.log(names)
```

### 1) 배열 메서드 (주요)

- `push()` : 배열 끝에 요소를 추가
    
    ```jsx
    const names = ['Alice', 'Bella', 'Cathy']
    
    names.push('Dan')
    console.log(names)  // ['Alice', 'Bella', 'Cathy', 'Dan']
    ```
    
- `pop()` : 배열 끝 요소를 제거하고, 제거한 요소를 반환
    
    ```jsx
    const names =  ['Alice', 'Bella', 'Cathy', 'Dan']
    
    console.log(names.pop())  // Dan
    console.log(names)  // ['Alice', 'Bella', 'Cathy']
    ```
    
- `unshift()` : 배열 앞에 요소를 추가
    
    ```jsx
    names.unshift('Eric')
    console.log(names)  // ['Eric', 'Alice', 'Bella', 'Cathy']
    ```
    
- `shift()` : 배열 앞 요소를 제거하고, 제거한 요소를 반환
    
    ```jsx
    console.log(names.shift())  // Eric
    console.log(names)  // ['Alice', 'Bella', 'Cathy']
    ```
    

### 2) Array helper methods

- 개요
    - 배열 조작을 보다 쉽게 수행할 수 있는 특별한 메서드 모음
    - ES6에 도입
    - 배열의 각 요소를 순회하며 각 요소에 대해 함수(콜백함수)를 호출
    - 대표 메서드 : `forEach()`, `filter()`, `every()`, `some()`, `reduce()`
    - 메서드 호출 시 인자로 함수(콜백함수)를 받는 것이 특징
- **콜백 함수 (Callback function)**
    - 다른 함수에 인자로 전달되는 함수
    - 외부 함수 내에서 호출되어 일종의 루틴이나 특정 작업을 진행
    - 예시
        
        ```jsx
        // 1
        // 콜백 함수를 3번 호출함
        const numbers1 = [1, 2, 3]
        numbers.forEach(function (num) {
          console.log(num ** 2)
        })
        ```
        
        ```jsx
        // 2
        const numbers2 = [1, 2, 3]
        const callBackFunction = function (num) {
          console.log(num ** 2)
        }
        // callBackFunction 함수에 ()를 붙이면 안됨. 바로 호출이 되기 때문
        // 함수 이름만 전달하기
        numbers.forEach(callBackFunction)
        ```
        

### 2-1) `forEach()`

- 배열의 각 요소를 반복하며 모든 요소에 대해 (콜백)함수를 호출
- 반환값 없음
- 구조 : `arr.forEach(callback(item[, index[, array]]))`
    - `item` : 처리할 배열의 요소
    - `index` : 처리할 배열 요소의 인덱스 (선택인자)
    - `array` : `forEach`를 호출한 배열 (선택 인자)
    - 반환 값 : undefined
- 예시
    
    ```jsx
    const names = ['Alice', 'Bella', 'Cathy']
    
    // 일반 함수 표기
    names.forEach(function (name) {
    	console.log(name
    })
    ```
    

### 2-2) `map()`

- 배열의 모든 요소에 대해 함수를 호출하고, 반환된 호출 결과 값을 모아 새로운 배열을 반환
- 구조 : `arr.map(callback(item[, index[, array]]))`
    
    ```jsx
    const newArr = array.map(function (item, index, array) {
    	// do something
    })
    ```
    
    - forEach의 매개변수와 동일
    - 반환값
        - 배열의 각 요소에 대해 실행한 **callback의 결과를 모은 새로운 배열**
        - forEach 동작원리와 같지만 forEach와 달리 새로운 배열을 반환함
- 예시 : 배열을 순회하며 각 객체의 name 속성 값을 추출하기 (for …of 와 비교)
    
    ```jsx
    // 1. for...of 와 비교
    const persons = [
      { name: 'Alice', age: 20 },
      { name: 'Bella', age: 21 }
    ]
    
    // 1.1 for...of
    let result1 = []
    for (const person of persons) {
      result1.push(person.name)
    }
    console.log(result1) // ['Alice', 'Bella']
    
    // 1.2 map
    const result2 = persons.map(function (person) {
      return person.name
    })
    console.log(result2) // ['Alice', 'Bella']
    
    ```
    
- 활용
    
    ```jsx
    // 2. 화살표 함수 표기
    const names = ['Alice', 'Bella', 'Cathy']
    
    const result3 = names.map(function (name) {
      return name.length
    })
    
    const result4 = names.map((name) => {
      return name.length
    })
    
    console.log(result3) // [5, 5, 5]
    console.log(result4) // [5, 5, 5]
    ```
    
    ```jsx
    // 3. 커스텀 콜백 함수
    const numbers = [1, 2, 3]
    const myCallbackFunction = function (number) {
      return number * 2
    }
    
    const doubleNumber = numbers.map(myCallbackFunction)
    
    console.log(doubleNumber) // [2, 4, 6]
    ```
    
- python에서의 map 함수와 비교
    - python의 map에 square 함수를 인자로 ㅂ

### 2-3) 배열 순회 종합

```jsx
// 배열 순회 종합
const names = ['Alice', 'Bella', 'Cathy']

// for loop
for (let idx = 0; idx < names.length; idx++) {
  console.log(names[idx])
}

// for...of
for (const name of names) {
  console.log(name)
}

// forEach
names.forEach((name) => {
  console.log(name)
})
```

| 방식 | 특징 | 비고 |
| --- | --- | --- |
| for loop | - 배열의 인덱스를 이용하여 각 요소에 접근
- break, continue 사용 가능 |  |
| for … of | - 배열 요소에 바로 접근 가능
- break, continue 사용 가능 |  |
| forEach() | - 간결하고 가독성이 높음. callback 함수를 이용하여 각 요소를 조작하기 용이
- break, continue 사용 불가 | 사용 권장 |

### 3) 기타 Array Helper Methods

| 메서드 | 역할 |
| --- | --- |
| filter | 콜백 함수의 반환 값이 참인 요소들만 모아서 새로운 배열을 반환 |
| find | 콜백 함수의 반환 값이 참이면 해당 요소를 반환 |
| some | 배열의 요소 중 적어도 하나라도 콜백 함수를 통과하면 true를 반환하며 즉시 배열 순회 중지. 반면에 모두 통과하지 못하면 false를 반환 |
| every | 배열의 모든 요소가 콜백 함수를 통과하면  true를 반환. 반면에 하나라도 통과하지 못하면 즉시 false를 반환하고 배열 순회 중지 |

### 4) 배열 whit 전개구문

- 배열 복사

```jsx
// 배열 복사 (with 전개 구문)
let parts = ['어깨', '무릎']
let lyrics = null

console.log(lyrics) // [ '머리', '어깨', '무릎', '발' ]
```

### 5) 참고

### 5-1) 콜백 함수의 이점

- **함수의 재사용성 측면**
    - 함수를 호출하는 코드에서 콜백 함수의 동작을 자유롭게 변경할 수 있음
    - 예를 들어, map 함수는 콜백함수를 인자로 받아 배열의 각 요소를 순회하며 콜백 함수를 실행
    - 이때, 콜백 함수는 각 요소를 변환하는 로직을 담당하므로, map 함수를 호출하는 코드는 간결하고 가독성이 높아짐
- **비동기적 처리 측면**
    - 코드가 12345 순서대로 작성되어있어도 그 순서가 달라짐.
    
    ```jsx
    console.log('a')
    
    setTimeout(() => {
    	console.log('b')
    }, 3000)
    
    console.log('c')
    
    // a
    // c
    // b
    ```
    
    - setTimeout 함수는 콜백 함수를 인자로 받아 일정 시간이 지난 후에 실행됨.
    - 이때, setTimeout 함수는 비동기적으로 콜백함수를 실행하므로, 다른 코드의 실행을 방해하지 않음 (추후 자세히 진행 예정)

### 5-2) forEach에서 break하는 대안

- `forEach` 에서는 break 키워드를 사용할 수 없음
- 대신 some과 every의 특징을 활용해 마치 break를 사용하는 것처럼 활용할 수 있음
    
    ```jsx
    const array = [1, 2, 3, 4, 5]
    
    // some
    // - 배열의 요소 중 적어도 하나라도 콜백 함수를 통과하는지 테스트
    // - 콜백 함수가 배열 요소 적어도 하나라도 참이면 true를 반환하고 순회 중지
    // - 그렇지 않으면 false를 반환
    
    const isEvenNumber = array.some(function (element) {
      return element % 2 === 0
    })
    
    console.log(isEvenNumber) // true
    ```
    
    ```jsx
    // every
    // - 배열의 모든 요소가 콜백 함수를 통과하는지 테스트
    // - 콜백 함수가 모든 배열 요소에 대해 참이면 true를 반환
    // - 그렇지 않으면 false를 반환하고 순회 중지
    
    const isAllEvenNumber = array.every(function (element) {
      return element % 2 === 0
    })
    
    console.log(isAllEvenNumber) // false
    ```
    
- some을 활용한 예시
: 콜백함수가 true를 반환하면 즉시 순회를 중단하는 특징을 활용
    
    ```jsx
    // [forEach를 break 하는 대안]
    // some과 every의 특징을 이용하여 마치 forEach에서 break를 사용하는 것처럼 구현할 수 있음
    const names = ['Alice', 'Bella', 'Cathy']
    
    // 1. some
    // - 콜백 함수가 true를 반환하면 some 메서드는 즉시 중단하고 true를 반환
    names.some(function(name) {
      if (name === 'Bella') {
        return true
      }
      return false
    })
    ```
    
- every를 활용한 예시
: 콜백 함수가 false를 반환하면 즉시 순회를 중단하는 특징을 활용
    
    ```jsx
    // 2. every
    // - 콜백 함수가 false를 반환하면 every 메서드는 즉시 중단하고 false를 반환
    names.every(function (name) {
      console.log(name)
      if (name === 'Bella') {
        return false
      }
      return true
    })
    ```
    

### 5-3) “배열은 객체다.”

- 배열도 키와 속성들을 담고 있는 참조 타입의 객체
- 배열의 요소를 대괄호 접근법을 사용해 접근하는 건 객체 문법과 같음.
    - 배열의 키는 숫자
- 숫자형 키를 사용함으로써 배열은 객체 기본 기능 이외에도 ‘순서가 있는 컬렉션’을 제어하게 해주는 특별한 메서드를 제공하는 것
- 배열은 인덱스를 키로 가지며 length 속성을 갖는 특수한 객체
    
    ```jsx
    const numbers = [1, 2, 3]
    console.log(Object.getOwnPropertyDescriptors(numbers))
    ```
    