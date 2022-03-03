# 🎁 큐 
# ✅ 큐란?
삽입이 일어나는 곳을 rear, 삭제가 일어나는 곳을 front라고 한다.
또한, 큐에 요소가 하나도 들어있지 않을 때는 공백(empty) 상태라 하고 꽉 차서 더 이상 요소를 집어넣지 못하 경우 포화(full) 상태라고 한다.

![](https://images.velog.io/images/kcwthing1210/post/b35c7485-1c81-49fb-a28b-6e4535d16502/image.png)

다음과 같이 front에서 빼오는 연산을 dequeue, 큐의 rear에 새로운 요소를 추가하는 연산을 enqueue라고 한다. dequeue의 경우 큐가 공백(empty) 상태인지 확인해야 하며, enqueue의 경우 큐가 포화(full) 상태인지 확인해야 한다.

# ✅ 선형 큐의 구현
선형 큐는 다음과 같이 배열을 통해 구현할 수 있다. 구현하는데 사용한 언어는 C++이고 템플릿 클래스로 구현하였다.
```c

#include <iostream>
using namespace std;

template <class T> class Queue {
private:
    int front;
    int rear;
    int size;
    T *elements;
public:
    Queue(int size) {
        front = 0;
        rear = 0;
        this->size = size;
        elements = new T[size];
    }

    ~Queue() {
        delete[] elements;
    }

    bool isEmpty() {
        return front == rear;
    }

    bool isFull() {
        return rear == size;
    }

    void enqueue(T elem) {
        if (isFull()) {
            cout << "Error : Queue is Full!" << endl;
        } else {
            elements[rear++] = elem;
        }
    }

    T dequeue() {
        if (isEmpty()) {
            cout << "Error : Queue is Empty!" << endl;
        } else {
            return elements[front++];
        }
    }

    T peek() {
        if (isEmpty()) {
            cout << "Error : Queue is Empty!" << endl;
        } else {
            return elements[front + 1];
        }
    }
    
    void display() {
        for (int i = front; i < rear; i++) {
            cout << elements[i] << " ";
        }
        cout << endl;
    }
};
```
선형 큐는 이해하기도 구현하기도 쉽지만 한 가지 문제점이 있다. 다음 코드를 실행해본다고 생각해보자.

```c
#include "queue.h"

int main() {
    Queue<int> queue(5);

    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    queue.enqueue(4);
    queue.enqueue(5);
    queue.display();
    cout << queue.dequeue() << endl;
    queue.enqueue(6);

    queue.display();

    return 0;
}
```

큐의 사이즈는 5이고 5개의 요소를 삽입하고 하나를 빼고 하나를 삽입한다. 그러면 안의 들어간 요소의 개수가 5개를 넘어가는 일이 없어서 정상적으로 삽입되어야 하지만, queue.enqueue(6);에서 큐가 포화 상태라는 메세지를 받는다.
![](https://images.velog.io/images/kcwthing1210/post/b6728059-e4a1-4a8a-9497-fb2bae42e8b0/image.png)

5개의 요소를 삽입했을 때 배열은 다음과 같은 형태가 된다.
![](https://images.velog.io/images/kcwthing1210/post/94016cdb-3390-449d-83e8-137d3c279a15/image.png)

하나의 요소를 뺐을 때 배열의 형태는 다음과 같다. 여기서 문제를 알 수 있다. rear와 front의 값이 자꾸 증가하기만 해서 결국 배열의 앞부분이 비어있더라도 더이상 삽입하지 못하는 경우가 발생한다. 이와 같은 공간 낭비를 더 이상 삽입할 공간이 없을 때 배열의 요소들의 인덱스를 하나씩 당겨주는 방법으로 해결할 수 있지만, 원형 큐로 구현하면 더 쉽게 해결할 수 있다.

## ✅ 원형 큐의 구현
```c
#include <iostream>
using namespace std;

template <class T> class Queue {
private:
    int front;
    int rear;
    int size;
    T *elements;
public:
    Queue(int size) {
        front = 0;
        rear = 0;
        this->size = size + 1;
        elements = new T[size];
    }

    ~Queue() {
        delete[] elements;
    }

    bool isEmpty() {
        return front == rear;
    }

    bool isFull() {
        return (rear + 1) % size == front;
    }

    void enqueue(T elem) {
        if (isFull()) {
            cout << "Error : Queue is Full!" << endl;
        } else {
            rear = (rear + 1) % size;
            elements[rear] = elem;
        }
    }

    T dequeue() {
        if (isEmpty()) {
            cout << "Error : Queue is Empty!" << endl;
        } else {
            front = (front + 1) % size;
            return elements[front];
        }
    }

    T peek() {
        if (isEmpty()) {
            cout << "Error : Queue is Empty!" << endl;
        } else {
            return elements[(front + 1) % size];
        }
    }
    
    void display() {
        int maxi = (front < rear) ? rear : rear + size;
        for (int i = front + 1; i <= maxi; i++) {
            cout << elements[i % size] << " ";
        }
        cout << endl;
    }
};
```

선형 큐의 문제점을 배열을 원형인 것처럼 활용함으로써 해결할 수 있다. 즉 이전과는 다르게 front와 rear가 배열의 끝 인덱스에서 증가하면은 인덱스 0을 가리키도록 하면 된다. 이는 나머지 연산으로 쉽게 구현할 수 있다. 이 코드에서 front는 항상 큐의 첫 번째 요소의 하나 앞을, rear는 마지막 요소를 가리킨다.

![](https://images.velog.io/images/kcwthing1210/post/905166bd-3311-46ab-b8be-e00a8fdacebb/image.png)
아까와 마찬가지로 5개의 요소를 삽입한 모습이다. 원형큐로 구현할 시에 공백 상태와 포화 상태를 구분하지 못하는 문제가 생기는데, 이는 해결하기 위해 인덱스 하나는 비워두었다. 위의 그림을 예로 들면, 인덱스를 하나 비워두지 않으면 공백 상태, 포화 상태 모두 rear와 front가 인덱스 0을 가리키는 문제가 생긴다.

```c
#include "queue.h"

int main() {
    Queue<int> queue(5);

    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    queue.enqueue(4);
    queue.enqueue(5);
    queue.display();
    cout << queue.dequeue() << endl;
    queue.enqueue(6);

    queue.display();

    return 0;
}
```

다시 위의 코드를 작동시켜보면 선형 큐로 구현했을 때와는 달리 포화 상태라는 메세지 없이 정상적으로 삽입되는 것을 확인할 수 있다.


# 🧩 Reference
- https://velog.io/@dongchyeon/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%81%90-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EA%B5%AC%ED%98%84

# 🎁 스택
## ✅  스택이란?
스택의 형태를 이해하기 위해서는 프링글스 통을 생각하면 편하다. 우리는 프링글스 통에서 과자를 빼어먹을 때 가장 맨 위에 있는 과자를 빼어먹으며, 과자를 넣을 때도 맨 위에 과자를 넣게 된다. 가장 늦게 들어온 것이 가장 첫번째로 나가는 형태이므로 이런 입출력 형태를 LIFO(Last-In First-Out)이라고 한다.

![](https://images.velog.io/images/kcwthing1210/post/98967e6f-6cf5-4edc-a920-728e86c49dda/image.png)

스택의 형태를 그림으로 나타낸 것이다. 스택에 있는 1, 2, 3을 스택의 요소라고 부르며, 가장 위에 있는 요소는 스택의 상단(top)이라 부른다.
또한, 스택에 요소가 하나도 들어있지 않을 때는 공백(empty) 상태라 하고 꽉 차서 더 이상 요소를 집어넣지 못하 경우 포화(full) 상태라고 한다.

![](https://images.velog.io/images/kcwthing1210/post/d06fe463-14d7-463a-b469-36814f2dc03b/image.png)

다음과 같이 스택의 top 요소를 빼오는 연산을 pop, 스택에 top에 새로운 요소를 추가하는 연산을 push라고 한다. pop의 경우 스택이 공백(empty) 상태인지 확인해야 하며, push의 경우 스택이 포화(full) 상태인지 확인해야 한다.

## ✅ 소스 코드 구현

```c
#include <stdbool.h>

#ifndef _STACK_
#define _STACK_

typedef struct stack {
        int* element;
        int size;
        int top;
} stack;
typedef stack* Stack;

Stack createStack(int n);
bool isFull(Stack stack);
void push(Stack stack, int elem);
bool isEmpty(Stack stack);
int pop(Stack stack);
int peek(Stack stack);
void printStack(Stack stack);

#endif
```

✔ stack.c

```c
Stack createStack(int n) {
    Stack stack = (Stack)malloc(sizeof(Stack));
    stack->element = (int*)malloc(sizeof(int) * n);
    stack->size = n;
    stack->top = -1;

    return stack;
}

bool isFull(Stack stack) {
    if (stack->top == stack->size - 1)
        return true;
    else
        return false;
}

void push(Stack stack, int elem) {
    if (!isFull(stack)) {
        stack->top++;
        stack->element[stack->top] = elem;
    }
}

bool isEmpty(Stack stack) {
    if (stack->top == -1)
        return true;
    else
        return false;
}

int pop(Stack stack) {
    if (!isEmpty(stack)) {
        return stack->element[stack->top--];
    }
}

int peek(Stack stack) {
    if (!isEmpty(stack)) {
        return stack->element[stack->top];
    }
}

void printStack(Stack stack) {
    for (int i = 0; i < stack->top + 1; i++) {
        printf("%d ", stack->element[i]);
    }
    printf("\n");
}
```

# 🧩 Reference
- https://velog.io/@dongchyeon/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9D-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0

# 🎁 Heap
## ✅ 힙(Heap)?
힙 자료구조는 완전 이진 트리를 기초로 하는 자료구조입니다. 완전 이진트리는 마지막을 제외한 모든 노드에서 자식들이 꽉 채워진 이진트리를 말합니다.

![](https://images.velog.io/images/kcwthing1210/post/8cf41d77-f127-4de6-b4a0-3c265bf17ff1/image.png)

- 힙은 최대힙(Max heap)과 최소힙(Min Heap)으로 나눠집니다. - 최대힙은 부모노드의 값이 자식노드들의 값보다 항상 크고, 최소힙은 부모노드의 값이 자식노드의 값보다 항상 작습니다. (위 그림은 최대힙의 예시)
- 이러한 성질 때문에 항상 느슨한 정렬상태(반정렬 상태)를 유지합니다.
- 힙은 최댓값 또는 최솟값을 쉽게 뽑기 위한 자료구조 임으로 중복을 허용합니다.

## ✅ 힙을 배열로 구현하기
힙은 대체적으로 배열로 구현됩니다. 완전이진트리를 기본으로 하기 때문에 비었는 공간이 없어 배열로 구현하기에 용이합니다.

아래 그림과 같이 루트노드를 배열의 0번 index에 저장하고, 각 노드를 기점으로 왼쪽 자식노드는 a[i∗2+1], 오른쪽 자식노드는 a[i∗2+2] 의 index에 저장됩니다. 또한 특정 index의 노드에서 부모노드는 a[(i−1)//2]로 찾을 수 있습니다.
![](https://images.velog.io/images/kcwthing1210/post/517dc696-46d0-4a91-8875-2802fff32fdf/image.png)

## ✅ 삽입과 삭제로 깨진 힙을 재구조화하기(heapify)

최대힙의 부모노드는 항상 자식노드의 값보다 크다는 조건을 가지고 있습니다. 하지만 힙에서 삽입 또는 삭제가 일어나게 되면 경우에 따라 최대힙의 조건이 깨질 수 있습니다. 이러한 경우에 최대힙의 조건을 만족할 수 있게 노드들의 위치를 바꿔가며 힙을 재구조화(heapify) 해주어야 합니다.

삽입과 삭제의 경우 모두 연산 자체는 O(1)로 작동하지만 heapify의 과정을 거치기 때문에 O(logn)의 시간복잡도를 가지게 됩니다.

### ✔ 삽입 과정 구현과정
![](https://images.velog.io/images/kcwthing1210/post/f86acf4b-af7d-458f-b69f-51780fe3af7c/image.png)


### ✔ 삭제과정 구현과정
![](https://images.velog.io/images/kcwthing1210/post/ff53d335-2143-493b-b6ff-d63ecaf7ecf4/image.png)
![]

## ✅ 힙이 아닌 배열을 힙으로 만들기(build heap)
heapify의 경우 기본적으로 힙을 만족하는 경우에서 삽입 또는 삭제가 발생할 때 O(logn)의 시간복잡도로 다시 힙으로 만드는 과정입니다. build heap은 이와 다르게 아예 힙의 조건을 만족하지 않는 배열을 힙으로 만드는 과정입니다. 여러번의 heapify 과정을 거치기 때문에 결과적으로 시간복잡도는 O(nlogn)입니다.

### ✔ 재귀함수를 이용한 재구조
![](https://images.velog.io/images/kcwthing1210/post/f3ad0dd3-6f09-43fb-9f76-21e6fdf3d66b/image.png)

```python
def make_heap(array, index, heap_size):
        parent = index
        left_child = 2 * parent + 1
        right_child = 2 * parent + 2

        if left_child < heap_size and array[left_child] > array[parent]:
            parent = left_child
        if right_child < heap_size and array[right_child] > array[parent]:
            parent = right_child
        if parent != index:
            array[parent], array[index] = array[index], array[parent]
            make_heap(array, parent, heap_size)
	
    # 부모노드가 되는 노드들만을 골라서 뒤에서부터 heapify를 차례로 실행
    for i in range((N - 1) // 2, -1, -1):
        make_heap(array, i, heap_size)
       
```

# 🧩 Reference
- https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%ED%9E%99Heap