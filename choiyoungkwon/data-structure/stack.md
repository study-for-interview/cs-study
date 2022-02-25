# Stack

# 스택(Stack)의 개념

한 쪽 끝에서만 자료를 넣고 뺄 수 있는 LIFO(Last In First Out) 형식의 자료 구조

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fby1qnT%2FbtqBE1v1UlX%2FzbnXdYnGAXhMYbcDCca6WK%2Fimg.png)

# 스택(Stack)의 연산
스택(Stack)는 LIFO(Last In First Out) 를 따른다. 즉, 가장 최근에 스택에 추가한 항목이 가장 먼저 제거될 항목이다.

- pop(): 스택에서 가장 위에 있는 항목을 제거한다.
- push(item): item 하나를 스택의 가장 윗 부분에 추가한다.
- peek(): 스택의 가장 위에 있는 항목을 반환한다.
- isEmpty(): 스택이 비어 있을 때에 true를 반환한다.


연산 시간 복잡도
| 연산 | 시간복잡도 |
| --- | --- |
| Insertion | O(1) | 
| Deletion | O(1) | 
| Search | O(n) | 

# 스택(Stack) 사용 사례

스택(Stack)의 사용 사례
재귀 알고리즘을 사용하는 경우 스택이 유용하다.

    - 재귀 알고리즘
        - 재귀적으로 함수를 호출해야 하는 경우에 임시 데이터를 스택에 넣어준다.
        - 재귀함수를 빠져 나와 퇴각 검색(backtrack)을 할 때는 스택에 넣어 두었던 임시 데이터를 빼 줘야 한다.
        - 스택은 이런 일련의 행위를 직관적으로 가능하게 해 준다.
        - 또한 스택은 재귀 알고리즘을 반복적 형태(iterative)를 통해서 구현할 수 있게 해준다.
    - 웹 브라우저 방문기록 (뒤로가기)
    - 실행 취소 (undo)
    - 역순 문자열 만들기
    - 수식의 괄호 검사 (연산자 우선순위 표현을 위한 괄호 검사)
        - Ex) 올바른 괄호 문자열(VPS, Valid Parenthesis String) 판단하기
    - 후위 표기법 계산

참고 : 

https://devuna.tistory.com/22

https://gmlwjd9405.github.io/2018/08/03/data-structure-stack.html

https://im-developer.tistory.com/121
