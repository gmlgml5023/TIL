# Control of flow

## 1. 제어문 (Control Statement)

- 코드의 실행흐름을 제어하는 데 사용되는 구문
- 조건에 따라 코드 블록을 실행하거나 반복적으로 코드를 실행
- 제어문 종류
    - 조건문 : `if`, `elif`, `else`
    - 반복문 : `for`, `while`
    - 반복문 제어 : `break`, `continue`, `pass`

<br>

## 2. 조건문 (Conditional Statement)

- 주어진 조건식을 평가하여 해당 조건이 참(True)인 경우에만 코드 블록을 실행하거나 건너뜀

### 1) 파이썬 조건문에 사용되는 키워드 : `if` statement

- 기본 구조
    
    ```python
    if 표현식:
        코드 블록
    elif 표현식:
        코드 블록
    else:
        코드 블록
    ```
    
- 복수 조건문 : 조건식을 동시에 검사하는 것이 아니라 순차적으로 비교

    ```python
    dust = 35

    if dust > 150:
        print('매우 나쁨')
    elif dust > 80:
        print('나쁨')
    elif dust > 30:
        print('보통')
    else:
        print('좋음')
    ```

- 중첩 조건문

    ```python
    dust = 480

    if dust > 150:
        print('매우 나쁨')
        """
        중첩 조건문
        """
        if dust > 300:
            print('위험해요! 나가지 마세요!')
    elif dust > 80:
        print('나쁨')
    elif dust > 30:
        print('보통')
    else:
        print('좋음')
    ```

<br>

## 3. 반복문 (**Loop Statement**)

- 주어진 코드 블록을 여러 번 반복해서 실행하는 구문
    - 특정 작업을 반복적으로 수행
    - 주어진 조건이 참인 동안 반복해서 실행
- 파이썬 반복문에 사용되는 키워드
    - `for` : 특정 작업을 반복적으로 수행
    - `while` : 주어진 조건이 참인 동안 반복해서 실행

### 1) 파이썬 조건문에 사용되는 키워드 : **`for` statement**

- 임의의 시퀀스의 항목들을 그 시퀀스에 들어있는 순서대로 반복
- for statement의 기본 구조
    
    ```python
    for 변수 in 반복 가능한 객체:
        코드 블록
    ```
    
- 반복 가능한 객체 `iterable` 
: 반복문에서 순회할 수 있는 객체 (시퀀스 객체 뿐만 아니라 dict, set 등도 포함)

> **for문 원리**
> 
- 리스트 내 첫 항목이 반복 변수에 할당되고 코드블록이 실행
- 다음으로 반복 변수에 리스트의 2번째 항목이 할당되고 코드블록이 다시 실행
- ... 마지막으로 반복 변수에 리스트의 마지막 요소가 할당되고 코드블록이 실행

    ```python
    items = ['apple', 'banana', 'coconut']

    for item in items:
        print(item)

    """
    apple
    banana
    coconut
    """
    ```

> **타입 별 순회**
> 
- 문자열 순회
    
    ```python
    country = 'Korea'
    
    for char in country:
        print(char)
    
    """
    K
    o
    r
    e
    a
    """
    ```
    
- range 순회
    
    ```python
    for i in range(5):
        print(i)
    
    """
    0
    1
    2
    3
    4
    """
    ```
    
- dict 순회
    
    ```python
    my_dict = {
        'x': 10,
        'y': 20,
        'z': 30,
    }
    
    for key in my_dict:
        print(key)
        print(my_dict[key])
    
    """
    x
    10
    y
    20
    z
    30
    """
    ```
    
- 인덱스로 리스트 순회
    - 리스트의 요소가 아닌 인덱스로 접근하여 해당 요소들을 변경하기
    
    ```python
    numbers = [4, 6, 10, -8, 5]
    
    for i in range(len(numbers)):
        numbers[i] = numbers[i] * 2
    
    print(numbers) # [8, 12, 20, -16, 10]
    ```
    

> 중첩된 반복문
> 
- 안쪽 반복문은 outers 리스트의 각 항목에 대해 한 번씩 실행됨
- print가 호출되는 횟수 => `len(outers) * len(inners)`
    
    ```python
    outers = ['A', 'B']
    inners = ['c', 'd']

    for outer in outers:
        for inner in inners:
            print(outer, inner)

    """
    A c
    A d
    B c
    B d
    """
    ```
    

- 중첩 리스트 순회
: 안쪽 리스트 요소에 접근하려면 바깥 리스트를 순회하면서 중첩 반복을 사용해 각 안쪽 반복을 순회
    
    ```python
    elements = [['A', 'B'], ['c', 'd']]

    for elem in elements:
        print(elem)

    """
    ['A', 'B']
    ['c', 'd']
    """

    elements = [['A', 'B'], ['c', 'd']]

    for elem in elements:
        for item in elem:
            print(item)

    """
    A
    B
    c
    d
    """
    ```
    
<br>

### 2) 파이썬 조건문에 사용되는 키워드 : **`while` statement**

- 주어진 조건식이 **참(True)인 동안 코드를 반복**해서 실행 == 조건식이 **거짓(False)가 될 때 까지 반복**
- while statement의 기본 구조
    
    ```python
    while 조건식:
        코드 블록
    ```
    
- 사용자 입력에 따른 반복
: while문을 사용한 특정 입력 값에 대한 종료 조건 활용하기
    
    ```python
     number = int(input('양의 정수를 입력해주세요.: '))
    
     while number <= 0:
         if number < 0:
             print('음수를 입력했습니다.')
         else:
             print('0은 양의 정수가 아닙니다.')
    
         number = int(input('양의 정수를 입력해주세요.: '))
    
     print('잘했습니다!')
     """
     양의 정수를 입력해주세요.: 0
     0은 양의 정수가 아닙니다.
     양의 정수를 입력해주세요.: -1
     음수를 입력했습니다.
     양의 정수를 입력해주세요.: 1
     잘했습니다!
     """
    ```
    
- while 문은 반드시 종료 조건이 필요

<br>

## 4. 적절한 반복문 활용하기

- `for`
    - 반복 횟수가 명확하게 정해져 있는 경우에 유용
    - 예를 들어 리스트, 튜플, 문자열 등과 같은 시퀀스 형식의 데이터를 처리할 때
- `while`
    - 반복 횟수가 불명확하거나 조건에 따라 반복을 종료해야 할 때 유용
    - 예를 들어 사용자의 입력을 받아서 특정 조건이 충족될 때까지 반복하는 경우

<br>

## 5. 반복 제어

- for문과 while은 매 반복마다 본문 내 모든 코드를 실행하지만 때때로 일부만 실행하는 것이 필요할 때가 있음
- 반복문 제어 키워드
    - `break` : 반복을 즉시 중지
        
        ```python
        # break
        
        for i in range(10):
            if i == 5:
                break
            print(i)  # 0 1 2 3 4
        ```
        
    - `continue` : 다음 반복으로 건너뜀
        
        ```python
        # continue
        
        for i in range(10):
            if i % 2 == 0:
                continue
            print(i)  # 1 3 5 7 9
        ```
        
    - `pass` : 아무런 동작도 수행하지 않고 넘어감
        
        ```python
        # pass
        
        for i in range(10):
            pass  # 아무 작업도 안함
        ```
        
<br>

## 6. List comprehension

- 간결하고 효율적인 리스트 생성 방법
- 구조
    
    ```python
    [expression for 변수 in iterable]
    list(expression for 변수 in iterable)
    
    [expression for 변수 in iterable if 조건식]
    list(expression for 변수 in iterable if 조건식)
    ```
    
<br>

## 7. 성능 비교

- list comprehension
    - 대부분의 경우 가장 빠르고 파이썬스러운(Pythonic) 방법
- map
    - 특정 상황(예: 기존 함수를 사용할 때)에서 리스트 컴프리헨션과 비슷하거나 약간 더 빠를 수 있음
- loop
    - 일반적으로 가장 느리다고 알려져 있지만,
    python 버전이 올라가면서 다른 방식과 비슷하거나 때로는 더 나은 결과를 보이기도 함
    - 복잡한 로직이 필요한 경우에는 여전히 유용하게 사용될 수 있음
- 결론
    - 성능 차이는 대부분의 경우 미미하므로,
    코드의 가독성과 유지보수성을 고려하여 상황에 맞는 적절한 방법을 선택하는 것을 권장

## 7. enumerate(iterable, start=0)

- iterable 객체의 각 요소에 대해 인덱스와 함께 반환하는 내장함수