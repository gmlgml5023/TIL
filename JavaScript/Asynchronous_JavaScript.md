# [JS] Asynchronous JavaScript

## 1. 비동기

### 1) 개요

- 동기 (Synchronous)
    - 프로그램의 실행 흐름이 순차적으로 진행
    - 하나의 작업이 완료된 후에 다음 작업이 실행되는 방식
- 비동기 (Asynchronous)
    - 특정 작업의 실행이 완료될 때까지 기다리지 않고 다음 작업을 즉시 실행하는 방식
    - 작업의 완료 여부를 신경 쓰지 않고 동시에 다른 작업들을 수행할 수 있음.

### 2) 비동기 방식의 특징

- 병렬적 수행
- 당장 처리를 완료할 수 없고 시간이 필요한 작업들은 백그라운드에서 실행되며 빨리 완료되는 작업부터 처리

## 2. JavaScript와 비동기

### 1) Single Thread 언어, JS

- Thread란?
    - 작업을 처리할 때 실제로 작업을 수행하는 주체
    - multi-thread라면 업무를 수행할 수 있는 주체가 여러 개라는 의미
- JS는 한번에 여러 일을 수행할 수 없다.
    - 한 번에 하나의 일만 수행할 수 있는 Single Thread 언어로 동시에 여러 작업을 처리할 수 없다.
    - 즉, JS는 하나의 작업을 요청한 순서대로 처리할 수 밖에 없음

### 2) JavaScript Runtime

- JS가 동작할 수 있는 환경(Runtime)
    - 브라우저 또는 Node.js
- JS는 Single Thread이므로 비동기 처리를 할 수 있도록 도와주는 환경이 필요

### 3) 브라우저 환경에서 JS 비동기 처리 관련 요소

- JavaScript Engine의 **Call Stack**
    - 요청이 들어올 때마다 순차적으로 처리하는 Stack (LIFO)
    - 기본적인 JS의 Single Thread 작업 처리
- **Web API**
    - JS 엔진이 아닌 브라우저에서 제공하는 runtime 환경
    - 시간이 소요되는 작업을 처리 (setTimeout, DOM Event, 비동기 요청 수행)
- **Task Queue** (Callback Queue)
    - 비동기 처리된 Callback함수가 대기하는 Queue(FIFO)
- **Event Loop**
    - 태스크(작업)가 들어오길 기다렸다가 태스크가 들어오면 이를 처리하고,
    처리할 태스크가 없는 경우엔 잠드는, 끊임없이 돌아가는 자바스크립트 내 루프
    - Call Stack과 Task Queue를 지속적으로 모니터링
    - Call Stack이 비어 있는지 확인 후 비어 있다면,
    Task Queue에서 대기중인 오래된 작업을 Call Stack으로 Push

### 4) 브라우저 환경에서 JS 비동기 처리 동작 방식

> WebAPI에서 처리된 작업이 지속적으로 Task Queue를 거쳐 Event Loop에 의해 Casll Stack에 들어와 순차적으로 실행됨으로써 비동기 작업이 가능한 환경이 됨
> 
- 모든 작업은 Call Stack (LIFO)으로 들어간 후 처리된다.
- 오래 걸리는 작업이 Call Stack으로 들어오면 Web API로 보내 별도로 처리하도록 한다.
- Web API에서 처리가 끝난 작업들은 곧바로 Call Stack으로 들어가지 못하고 Task Queue(FIFO)에 순서대로 들어간다.
- Event Loop가 Call Stack이 비어 있는 것을 계속 체크하고 Call Stack이 빈다면 Task Queue에서 가장 오래된 (가장 먼저 처리되어 들어온) 작업을 Call Stack으로 보낸다.

## 3. Ajax

### 1) 개요

### 1-1) 정의

- 비동기적인 웹 애플리케이션 개발을 위한 기술
- `XMLHttpRequest` 기술을 사용해 복잡하고 동적인 웹 페이지를 구성하는 프로그래밍 방식
- 브라우저와 서버 간의 데이터를 비동기적으로 교환하는 기술
- Ajax를 사용하면 페이지 전체를 새로고침하지 않고도 동적으로 데이터를 불러와 화면을 갱신할 수 있음
- Ajax의 ‘x’는 XML이라는 데이터타입을 의미하긴 하지만, 요즘은 더 가벼운 용량과 JS의 일부라는 장점때문에 JSON을 많이 사용

### 1-2) 목적

- 비동기 통신
    - 웹 페이지 전체를 새로고침하지 않고 서버와 데이터를 주고받을 수 있음
- 부분 업데이트
    - 전체 페이지가 다시 로드되지 않고 HTML 페이지 일부 DOM만 업데이트
    - 페이지의 일부분만 동적으로 갱신할 수 있어 사용자 경험이 향상
- 서버 부하 감소
    - 필요한 데이터만 요청하므로 서버의 부하를 줄일 수 있음

### 1-3) 기존 기술과의 차이


- XHR 객체 생성 및 요청
- 서버는 새로운 페이지를 응답으로 만들지 않고 필요한 부분에 대한 데이터만 처리 후 응답 (JSON 및 기타 데이터)
- 새로운 페이지를 받는 것이 아닌 필요한 부분의 데이터만 받아 기존 페이지의 일부를 수정 (새로고침X)
- 서버에서 모두 처리되던 데이터 처리의 일부분이 이제는 클라이언트 쪽에서 처리되므로 교환되는 데이터양과 처리량이 줄어듦

### 1-4) `XMLHttpRequest` (XHR) 객체

- 웹브라우저와 서버 간의 비동기 통신을 가능하게 하는 JS 객체
- 주요 기능
    - JS를 사용하여 서버에 HTTP 요청을 할 수 있는 객체
    - 웹페이지의 전체 새로고침 없이도 서버로부터 데이터를 가져오거나 보낼 수 있음
    - 이름에 XML이라는 데이터타입이 들어가긴 하지만 XML 뿐만 아니라 모든 종류의 데이터를 가져올 수 있음

### 1-5) 이벤트 핸들러는 비동기 프로그래밍의 한 형태

- 이벤트가 발생할 때마다 호출되는 함수 (콜백함수)를 제공하는 것
- HTTP 요청은 응답이 올 때까지의 시간이 걸릴 수 있는 작업이라 비동기이며,
이벤트 핸들러를 XHR 객체에 연결해 요청의 진행 상태 및 최종 완료에 대한 응답을 받음

### 2) Axios

### 2-1) 정의

- 브라우저와 Node.js에서 사용할 수 있는 Promise 기반의 HTTP 클라이언트 라이브러리
- 클라이언트 및 서버 사이에 HTTP 요청을 만들고 응답을 처리하는 데 사용
- 서버와의 HTTP 요청과 응답을 간편하게 처리할 수 있도록 도와주는 도구
- 브라우저를 위한 XHR 객체 생성
- 간편한 API를 제공하며, Promise 기반의 비동기 요청을 처리
- 주로 웹 애플리케이션에서 서버와 통신할 때 사용

### 2-2) 클라이언트 서버 간 동작


- XHR 객체 생성 및 요청
- 응답 데이터 생성
- JSON 데이터 응답
- Promise 객체 데이터를 활용해 DOM 조작 (웹페이지의 일부분 만을 다시 로딩)

### 2-3) Axios 설치 및 사용

- CDN 방식으로 사용하기
- `<script **src**="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>`
- `Promise` object
    - 자바스크립트에서 비동기 작업을 처리하기 위한 객체
    - 비동기 작업의 최종 완료 (또는 실패)와 그 결과값을 나타냄
    
    ```jsx
    // 1.
    const promiseObj = axios({
      method: 'get',
      url: 'https://api.thecatapi.com/v1/images/search'
    })
    
    console.log(promiseObj) // Promise object
    ```
    
    - 주요 메서드
        
        ```jsx
        promiseObj
          .then((response) => {
            console.log(response)
          })
          .catch((error) => {
            console.log(error)
          })
          
        console.log('안녕하세요')
        ```
        
        - `then()` : 작업이 성공적으로 완료되었을 때 실행될 콜백 함수를 지정
        - `catch()` : 작업이 실패했을 때 실행될 콜백 함수를 지정

### 2-4) Axios 기본 구조

- axios 객체를 활용해 요청을 보낸 후 응답 데이터 promise 객체를 받음
    
    ```jsx
    axios({
      method: 'get',
      url: 'https://api.thecatapi.com/v1/images/search'
    })
      .then((response) => {
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    ```
    
- 성공 처리
    - then 메서드를 사용해서 ‘성공했을 때 수행할 로직’을 작성
    - 서버로부터 받은 응답 데이터를 처리
- 실패 처리
    - catch 메서드를 사용해서 ‘실패했을 때 수행할 로직’을 작성
    - 네트워크 오류나 서버 오류 등의 예외 상황을 처리


- then & catch 특징
    - then(callback)
        - 요청한 작업이 성공하면 callback 실행
        - callback은 이전 작업의 성공 결과를 인자로 전달받음
    - catch(callback)
        - `then()`이 하나라도 실패하면 callback 실행 (남은 then은 중단)
        - callback은 이전 작업의 실패 객체를 인자로 전달받음

### 2-5) Axios 활용 (고양이 사진 가져오기 실습)

```jsx
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
    const URL = 'https://api.thecatapi.com/v1/images/search'
    // 1. axios 요청 처리
    axios({
      method: 'get',
      url: URL
    })
      .then((response) => {
        console.log(response)
        console.log(response.data)
        console.log(response.data[0].url)
      })
      .catch((error) => {
        consol.elog(error)
        console.log('실패했다옹')
      })
    console.log('야옹야옹')
  </script>
```

- The Cat API : 이미지를 요청해서 가져오는 작업을 비동기로 처리하기
- 요청 후 cat api로부터 응답을 기다려야 하는 작업은 비동기로 처리하기 때문에 ‘야옹야옹’ 출력 이후 응답 데이터가 출력되는 것을 확인할 수 있음
- 버튼을 누르면 고양이 이미지를 요청하고 요청이 처리되어 응답이 오면, 응답 데이터에 있는 이미지 주소 값을 img 태그에 넣어 이미지 출력

### 3) Ajax와 Axios

- Ajax
    - 하나의 특정한 기술을 의미하는 것이 아니라
    - 비동기적인 웹 애플리케이션 개발에 사용하는 기술들의 집합을 지칭
- Axios (라이브러리)
    - 클라이언트 및 서버 사이에 HTTP 요청을 만들고 응답을 처리하는 데 사용되는 JS fkdlqmfjfl
    - Promise API를 기반으로 하여 비동기 처리를 더 쉽게 할 수 있음
- 프론트에서 Axios를 활용해 DRF로 만든 API 서버로 요청을 보내고, 받아온 데이터를 비동기적으로 처리하는 로직을 작성하게 됨
- Ajax는 개념이자 접근방식, Axios는 이를 실현하는 구체적인 도구
- Axios는 Ajax를 구현하는 도구 중 하나로, XMLHttpRequest를 추상화하여 더 사용하기 쉽게 만든 라이브러리

## 4. Callback과 Promise

### 1) 비동기 처리의 특성과 관리

- 비동기 처리의 특성
: 비동기 처리의 핵심은 작업이 시작되는 순서가 아니라 완료되는 순서에 따라 처리된다는 것
- 비동기 처리의 어려움
    - 개발자 입장에서 코드의 실행 순서가 불명확하다는 단점 존재
    - 이로 인해 실행 결과를 정확히 예측하며 코드를 작성하기 어려울 수 있음

### 2) 비동기 처리 관리 방법

### 2-1) 비동기 콜백

- 비동기적으로 처리되는 작업이 완료되었을 때 실행되는 함수 (순서를 보장하고자)
- 연쇄적으로 발생하는 비동기 작업을 순차적으로 동작할 수 있게 함
- 작업의 순서와 동작을 제어하거나 결과를 처리하는 데 사용
- 비동기 콜백의 한계
    - 보통 어떤 기능의 실행 결과를 받아서 다른 기능을 수행하기 위해 많이 사용됨.
    - 콜백 지옥 발생
    - 콜백함수는 비동기 작업을 순차적으로 실행할 수 있게 하는 반드시 필요한 로직
    - 비동기 코드를 작성하다 보면 콜백 함수로 인한 콜백 지옥은 빈번히 나타나는 문제이며, 이는 코드의 가독성을 해치고 유지 보수가 어려워짐
        - 다른 표기 형태가 필요하다 !

### 2-2) Promise

- 비동기 작업의 최종 완료 또는 실패를 나타내는 객체
- JS에서 비동기 작업의 결과를 나타내는 객체
- 비동기 작업이 완료되었을 때 결과 값을 반환하거나 실패 시 에러를 처리할 수 있는 기능을 제공
- “**작업이 끝나면 실행시켜줄게**”라는 약속
- Promise 기반의 HTTP 클라이언트 라이브러리가 바로 Axios
- Promise가 제공하는 이점 (비동기 콜백과 비교)
    - **실행 순서의 보장**
        - 콜백 함수 : JS의 Event Loop가 현재 실행중인 Call Stack을 완료하기 전에는 호출되지 않음
        - Promise : then/catch 메서드의 콜백 함수는 Event Queue에 배치되는 순서대로 엄격하게 호출됨
        - 이는 비동기 작업의 실행 순서를 더 예측 가능하게 만듦
    - **유연한 비동기 처리** : Promise는 비동기 작업이 완료된 후에도 then 메서드를 통해 콜백을 추가할 수 있음
    - **체이닝**(chaining)을 통한 연속적인 비동기 처리
        - then 메서드를 여러 번 연결하여 여러 개의 콜백 함수를 순차적으로 실행 가능
        - 각 콜백은 주어진 순서대로 실행되며 이전 Promise의 결과를 다음 then에서 사용할 수 있음
        - 복잡한 비동기 로직을 명확히 표현 가능
    - **에러 처리의 일원화**
        - catch 메서드를 통해 Promise 체인 전체의 에러를 한 곳에서 처리할 수 있음
        - 전통적인 콜백 방식에서 각 콜백마다 에러 처리를 해야 하는 번거로움을 해소

### 2-3) then&catch의 chaining

- axios로 처리한 비동기 로직은 항상 promise 객체를 반환
- 즉, then과 catch는 모두 항상 promise 객체를 반환
    - 계속해서 chaining을 할 수 있음
- then을 계속 이어 나가면서 작성할 수 있게 됨
- then 메서드 chaining의 목적
    - 비동기 작업의 ‘순차적인’ 처리 가능
    - 코드를 보다 직관적이고 가독성 좋게 작성할 수 있도록 도움
- then 메서드 chaining 적용
    
    ```jsx
    .then((response) => {
      // console.log(response)
      // console.log(response.data)
      // console.log(response.data[0].url)
      // 1. 이미지 주소 저장
      const imgUrl = response.data[0].url
      return imgUrl
    })
    
    // 첫번째 then 콜백함수의 반환 값이 이어지는 then 콜백함수의 인자로 전달됨
    .then((imgData) => {
      // 2. img 태그 생성
      const imgTag = document.createElement('img')
      // 3. img태그의 src 속성 값 설정
      imgTag.setAttribute('src', imgData)
      // 4. body의 자식 태그로 img 태그 추가
      document.body.appendChild(imgTag)
    })
    ```
    
- then 메서드 chaining의 장점
    - 가독성 : 비동기 작업의 순서와 의존 관계를 명확히 표현할 수 있어 코드의 가독성이 향상
    - 에러 처리 : 각각의 비동기 작업 단계에서 발생하는 에러를 분할에서 처리 가능
    - 유연성 : 각 단계마다 필요한 데이터를 가공하거나 다른 비동기 작업을 수행할 수 있어서 더 복잡한 비동기 흐름을 구성할 수 있음
    - 코드 관리 : 비동기 작업을 분리하여 구성하면 코드를 관리하기 용이