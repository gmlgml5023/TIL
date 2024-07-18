# Modules

## 1. 모듈

- 한 파일로 묶인 변수와 함수의 모음
- 특정한 기능을 하는 코드가 작성된 파이썬 파일 (`.py`)
- 예시
    - math 내장 모듈
    - 파이썬이 미리 작성해둔 수학 관련 변수와 함수가 작성된 모듈
    
    ```python
    import math
    
    print(math.pi)  # 3.141592653589793
    
    print(math.sqrt(4))  # 2.0
    ```

<br>

## 2. 모듈 활용

### 1) 모듈 import

> 모듈을 가져오는 방법

- `import`문 사용

    ```
    import math
    
    print(math.sqrt(4))
    ```

- `from` 절 사용

    ```
    from math import sqrt

    print(sqrt(4))
`    ``

> 모듈 사용하기

- `. (dot)` 연산자
: “점의 왼쪽 객체에서 점의 오른쪽 이름을 찾아라” 라는 의미

    ```python
    # 모듈명.변수명
    print(math.pi)

    # 모듈명.함수명
    print(math.sqrt(4))
    ```

> 모듈 주의사항
 
- 서로 다른 모듈이 같은 이름의 함수를 제공할 경우 문제 발생

    ```python
    # 모듈명.변수명
    print(math.pi)

    # 모듈명.함수명
    print(math.sqrt(4))
    ```

    ```python
    # 모듈명.변수명
    print(math.pi)

    # 모듈명.함수명
    print(math.sqrt(4))
    ```

- 마지막에 `import`된 이름으로 대체됨.

> `as` 키워드
 
- as 키워드를 사용하여 별칭(alias)을 부여
→ 두 개 이상의 모듈에서 동일한 이름의 변수, 함수 클래스 등을 가져올 때 발생하는 이름 충돌 해결

    ```python
    from math import sqrt
    from my_math import sqrt as my_sqrt
  
     sqrt(4)
     my_sqrt(4)
    ```

### 2) 사용자 정의 모듈

- 직접 정의한 모듈 사용하기
    - 모듈 my_math.py 작성
    - 두 수의 합을 구하는 add 함수 작성
    - my_math 모듈 import 후 add 함수 호출


<br>

## 3. 파이썬 표준 라이브러리 (Python Standard Library)

- 파이썬 언어와 함께 제공되는 다양한 모듈과 패키지의 모음
- 모듈 → 패키지 → 라이브러리
- https://docs.python.org/ko/3/library/index.html

### 1) 패키지 (Package)

- 연관된 모듈들을 하나의 디렉토리에 모아놓은 것
- 패키지 사용하기
    - 아래와 같은 디렉토리 구조로 작성
        
        ```markdown
            📦...
             ┣ 📜sample.py
             ┣ 📂my_package
             ┃ ┣ 📂math
             ┃ ┃ ┗ 📜my_math.py
             ┃ ┣ 📂statistics
             ┃ ┃ ┗ 📜tools.py
        ```
        
    - 패키지 3개 : my_package, math(서브패키지), statistics
    - 모듈 2개 : my_math, tools        
    - 각 패키지의 모듈을 import하여 사용하기
        
        ```python
            # sample.py
        
            from my_package.math import my_math
            from my_package.statistics import tools
        
            print(my_math.add(1, 2))  # 3
            print(tools.mod(1, 2))  # 1
        ```
        

### 2) PSL 내부 패키지

- 설치 없이 바로 `import`하여 사용

### 3) 외부 패키지 (외부 라이브러리)

- `pip`를 사용하여 설치 후 `import` 필요

### 4) pip 파이썬 패키지 관리자

- 외부 패키지들을 설치하도록 도와주는 파이썬의 패키지 관리 시스템
- PyPI(Python Package Index)에 저장된 외부 패키지들을 설치

### 5) 패키지 설치

- 최신 버전 / 특정 버전 / 최소 버전을 명시하여 설치할 수 있음
    
    ```bash
    $ pip install SomePackage
    $ pip install SomePackage==1.0.5
    $ pip install SomePackage>=1.0.4
    ```
    
- requests 외부 패키지 설치 및 사용 예시
    
    ```python
    ! pip install requests # 파이썬 전역 환경에 설치한 것
    
    import requests
    
    url = 'https://random-data-api.com/api/v2/users'
    response = requests.get(url).json()
    
    print(response)
    ```
    

### 6) 패키지 사용 목적

- 모듈들의 이름공간을 구분하여 충돌을 방지
- 모듈들을 효율적으로 관리하고 재사용할 수 있도록 돕는 역할
