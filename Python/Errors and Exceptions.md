# 에러와 예외 `Errors and Exceptions`

## 1. 버그
### 1) 버그 `bug`
- 소프트웨어에서 발생하는 오류 ?또는 결함
- 프로그램의 예상된 동작과 실제 동작 사이의 불일치

### 2) 디버깅 `debugging`
- 소프트웨어에서 발생하는 버그를 찾아내고 수정하는 과정
- 프로그램의 오작동 원인을 식별하여 수정하는 작업

### 3) 디버깅 방법
- `print` 함수를 활용
  - 특정 함수 결과
  - 반복/조건 결과 등 나눠서 생각
  - 코드를 bisection으로 나눠서 생각
- 개발 환경 (text editor, IDE) 등에서 제공하는 기능 활용
  - breakpoint, 변수 조회 등
- [Python tutor](https://pythontutor.com/) 활용 (단순 파이썬 코드인 경우)
- 뇌 컴파일, 눈 디버깅 등

<br>

## 2. 에러
### 1) 에러 `Error`
- 프로그램 실행 중 발생하는 예외 상황
### 2) 파이썬의 에러 유형
- **문법 에러** `Syntax Error` <br> - 프로그램의 구문이 올바르지 않은 경우 발생 <br> (오타, 괄호 및 콜론 누락 등의 문법적 오류)
    - Invalid Syntax
        ```python
        while # SyntaxError: invalid syntax
        ```
    - assign to literal
        ```python
        5=3 # SyntaxError: cannot assign to literal
        ```
    - EOL (End of Line)
        ```python
        print('hello
        # SyntaxError: EOL while scanning string literal
        ```
    - EOF (End of File)
        ```python
        print(
        #SyntaxError: unexpected EOF while parsing
        ```
- **예외** `Exception` <br> - 프로그램 실행 중 감지되는 에러 <br> - 내장 예외 : 예외 상황을 나타내는 예외 클래스들. 파이썬에서 이미 정의되어 있으며, 특정 예외 상황에 대한 처리를 위해 사용 <br> [참고자료] (https://docs.python.org/ko/3/library/exceptions.html#ValueError)

    <br>

    - `ZeroDivisionError` : 나누기 또는 모듈로 연산의 두 번째 인자가 0일 때 발생
        ```python
        10/0 # ZeroDivisionError: division by zero
        ```
    - `NameError` : 지역 또는 전역 이름을 찾을 수 없을 때 발생
        ```python
        print(name_error) # NameError: name 'name_error' is not defined
        ```
    - `TypeError`
      - 타입 불일치
        ```python
        '2' + 2  # TypeError: can only concatenate str (not "int") to str
        ```
      - 인자 누락        
        ```python
        sum()  # TypeError: sum() takes at least 1 positional argument (0 given)
        ```
        
      - 인자 초과   
        ```python
        sum(1, 2, 3)  # TypeError: sum() takes at most 2 arguments (3 given)
        ```
        
      - 인자 타입 불일치    
        ```python
        import random
        random.sample(1, 2)
        # TypeError: Population must be a sequence.  For dicts or sets, use sorted(d).
        ```

    - `ValueError` : 연산이나 함수에 문제가 없지만 부적절한 값을 가진 인자를 받았고, 상황이 IndexError 처럼 더 구체적인 예외로 설명되지 않는 경우 발생
            
        ```python
        int('1.5') # ValueError: invalid literal for int() with base 10: '3.5'
        
        range(3).index(6) # ValueError: 6 is not in range
        ```
            
    - `IndexError` : 시퀀스 인덱스가 범위를 벗어날 때 발생
            
        ```python
        empty_list = []
        empty_list[2]
        # IndexError: list index out of range
        ```
        
    - `KeyError` : 딕셔너리에 해당 키가 존재하지 않는 경우
        
        ```python
        person = {'name': 'Alice'}
        person['age']  # KeyError: 'age'
        ```
            
    - `ModuleNotFoundError` : 모듈을 찾을 수 없을 때 발생
        
        ```python
        import hahaha  # ModuleNotFoundError: No module named 'hahaha'
        ```
            
    - `ImportError` : 임포트 하려는 이름을 찾을 수 없을 때 발생
            
        ```python
        from random import hahaha
        # ImportError: cannot import name 'hahaha' from 'random'
        ```
            
    - `KeyboardInterrupt` : 사용자가 Control-C 또는 Delete를 누를 때 발생, 무한루프 시 강제 종료
            
        ```python
        while True:
            continue
        
        '''
        Traceback (most recent call last):
          File "...", line 2, in <module>
            continue
        KeyboardInterrupt
        '''
        ```
            
    - `IndentationError` : 잘못된 들여쓰기와 관련된 문법 오류
            
            ```python
            for i in range(10):
                print(i) # IndentationError: expected an indented block
            ```
<br>
            
## 3. 예외 처리
- 예외가 발생했을 때 프로그램이 비정상적으로 종료되지 않고, 적절하게 처리할 수 있도록 하는 방법

### 1) 예외 처리 사용 구문
- `try` : 예외가 발생할 수 있는 코드 작성
- `except` : 예외가 발생했을 때 실행할 코드 작성
- `else` : 예외가 발생하지 않았을 때 실행할 코드 작성
- `finally` : 예외 발생 여부와 상관없이 항상 실행할 코드 작성
    
```python
try:
    x = int(input('숫자를 입력하세요: '))
    y = 10 / x
except ZeroDivisionError:
    print('0으로 나눌 수 없습니다.')
except ValueError:
    print('유효한 숫자가 아닙니다.')
else:
    print(f'결과: {y}')
finally:
    print('프로그램이 종료되었습니다.')

```

### 2) try & except
- try 블록 안에는 예외가 발생할 수 있는 코드를 작성
- except 블록 안에는 예외가 발생했을 때 처리할 코드를 작성
- 예외가 발생하면 프로그램 흐름은 try 블록을 빠져나와 해당 예외에 대응하는 except 블록으로 이동
```python
try:
    # 예외가 발생할 수 있는 코드

except 예외:
    # 예외 처리 코드
```

### 3) 복수 예외 처리
- 100을 사용자가 입력한 값으로 나누고 출력하는 코드를 작성해보시오.
    - 먼저, 발생 가능한 에러가 무엇인지 예상해보기
        
        ```python
        num = int(input('100으로 나눌 값을 입력하시오 : '))
        print(100 / num)
        ```
        
- 100을 사용자가 입력한 값으로 나누고 출력하는 코드를 작성해보시오.
    - 먼저, 발생 가능한 에러가 무엇인지 예상해보기
        
        ```python
        num = int(input('100으로 나눌 값을 입력하시오 : '))
        print(100 / num)
        
        # int(’a’)
        # 100/int(’0’)
        ```
        
- 100을 사용자가 입력한 값으로 나누고 출력하는 코드를 작성해보시오.
    - 먼저, 발생 가능한 에러가 무엇인지 예상해보기
        
        ```python
        num = int(input('100으로 나눌 값을 입력하시오 : '))
        print(100 / num)
        
        """
        int(’a’)
        문자열을 int로 형변환 : ValueError
        """
        
        """
        100 / 0
        0으로 숫자를 나눔 : ZeroDivisionError
        """
        ```
        
- 100을 사용자가 입력한 값으로 나누고 출력하는 코드를 작성해보시오.
    - 발생가능한 에러를 모두 명시하거나 & 별도로 작성하기
    - 모두 명시
        
        ```python
        try:
            num = int(input('100으로 나눌 값을 입력하시오 : '))
            print(100 / num)
        except (ValueError, ZeroDivisionError):
            print('제대로 입력해주세요.')
        ```
        
    - 별도 작성
        
        ```python
        try:
            num = int(input('100으로 나눌 값을 입력하시오 : '))
            print(100 / num)
        except ValueError:
            print('숫자를 넣어주세요.')
        except ZeroDivisionError:
            print('0으로 나눌 수 없습니다.')
        except:
            print('에러가 발생하였습니다.')
        ```

### 4) else & finally

- `else`
    - 예외가 발생하지 않았을 때 추가 작업을 진행
- `finally`
    - 예외 발생 여부와 상관없이 항상 실행할 코드를 작성
    
    ```python
    try:
        x = int(input('숫자를 입력하세요: '))
        y = 10 / x
    except ZeroDivisionError:
        print('0으로 나눌 수 없습니다.')
    except ValueError:
        print('유효한 숫자가 아닙니다.')
    else:
        print(f'결과: {y}')
    finally:
        print('프로그램이 종료되었습니다.')
    ```
<br>

## 4. 예외 처리 주의사항

### 1) 내장 예외의 상속 계층구조 주의

- 아래와 같이 예외를 작성하면 코드는 2번째 except 절에 이후로 도달하지 못함
    
    ```python
    try:
        num = int(input('100으로 나눌 값을 입력하시오 : '))
        print(100 / num)
    except BaseException:
        print('숫자를 넣어주세요.')
    # 하단 블록에 도달하지 못함
    except ZeroDivisionError:
        print('0으로 나눌 수 없습니다.')
    except:
        print('에러가 발생하였습니다.')
    ```

- 내장 예외 클래스는 상속 계층구조를 가지기 때문에 except 절로 분기 시 반드시 하위 클래스를 먼저 확인 할 수 있도록 작성해야 함
    
    ```python
    try:
        num = int(input('100으로 나눌 값을 입력하시오 : '))
        print(100 / num)
    except BaseException: # 하위 예외 클래스 확인 필요
        print('숫자를 넣어주세요.')
    except ZeroDivisionError: # 하위 예외 클래스 확인 필요
        print('0으로 나눌 수 없습니다.')
    except:
        print('에러가 발생하였습니다.')
    ```

### 2) 예외 객체 다루기

- `as` 키워드
    - 예외객체 : 예외가 발생했을 때 예외에 대한 정보를 담고 있는 객체
    - `except` 블록에서 예외 객체를 받아 상세한 예외 정보를 활용 가능
        
        ```python
        my_list = []
        
        try:
            number = my_list[1]
        except IndexError as error:
            print(f'{error}가 발생했습니다.')
        
        # list index out of range가 발생했습니다.
        ```    
- **try-except와 if-else**
    - `try-except`와 `if-else`를 함께 사용할 수 있음
        
        ```python
        try:
            x = int(input('숫자를 입력하세요: '))
            if x < 0:
                print('음수는 허용되지 않습니다.')
            else:
                print('입력한 숫자:', x)
        except ValueError:
            print('오류 발생')    
        ```
        

<br>

## 5. 예외처리와 값 검사에 대한 2가지 접근 방식

### 1) EAFP

- 예외처리를 중심으로 코드를 작성하는 접근 방식 : try-except

### 2) LBYL

- 값 검사를 중심으로 코드를 작성하는 접근 방식 : if-else