# π ν 
# β νλ?
μ½μμ΄ μΌμ΄λλ κ³³μ rear, μ­μ κ° μΌμ΄λλ κ³³μ frontλΌκ³  νλ€.
λν, νμ μμκ° νλλ λ€μ΄μμ§ μμ λλ κ³΅λ°±(empty) μνλΌ νκ³  κ½ μ°¨μ λ μ΄μ μμλ₯Ό μ§μ΄λ£μ§ λͺ»ν κ²½μ° ν¬ν(full) μνλΌκ³  νλ€.

![](https://images.velog.io/images/kcwthing1210/post/b35c7485-1c81-49fb-a28b-6e4535d16502/image.png)

λ€μκ³Ό κ°μ΄ frontμμ λΉΌμ€λ μ°μ°μ dequeue, νμ rearμ μλ‘μ΄ μμλ₯Ό μΆκ°νλ μ°μ°μ enqueueλΌκ³  νλ€. dequeueμ κ²½μ° νκ° κ³΅λ°±(empty) μνμΈμ§ νμΈν΄μΌ νλ©°, enqueueμ κ²½μ° νκ° ν¬ν(full) μνμΈμ§ νμΈν΄μΌ νλ€.

# β μ ν νμ κ΅¬ν
μ ν νλ λ€μκ³Ό κ°μ΄ λ°°μ΄μ ν΅ν΄ κ΅¬νν  μ μλ€. κ΅¬ννλλ° μ¬μ©ν μΈμ΄λ C++μ΄κ³  ννλ¦Ώ ν΄λμ€λ‘ κ΅¬ννμλ€.
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
μ ν νλ μ΄ν΄νκΈ°λ κ΅¬ννκΈ°λ μ½μ§λ§ ν κ°μ§ λ¬Έμ μ μ΄ μλ€. λ€μ μ½λλ₯Ό μ€νν΄λ³Έλ€κ³  μκ°ν΄λ³΄μ.

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

νμ μ¬μ΄μ¦λ 5μ΄κ³  5κ°μ μμλ₯Ό μ½μνκ³  νλλ₯Ό λΉΌκ³  νλλ₯Ό μ½μνλ€. κ·Έλ¬λ©΄ μμ λ€μ΄κ° μμμ κ°μκ° 5κ°λ₯Ό λμ΄κ°λ μΌμ΄ μμ΄μ μ μμ μΌλ‘ μ½μλμ΄μΌ νμ§λ§, queue.enqueue(6);μμ νκ° ν¬ν μνλΌλ λ©μΈμ§λ₯Ό λ°λλ€.
![](https://images.velog.io/images/kcwthing1210/post/b6728059-e4a1-4a8a-9497-fb2bae42e8b0/image.png)

5κ°μ μμλ₯Ό μ½μνμ λ λ°°μ΄μ λ€μκ³Ό κ°μ ννκ° λλ€.
![](https://images.velog.io/images/kcwthing1210/post/94016cdb-3390-449d-83e8-137d3c279a15/image.png)

νλμ μμλ₯Ό λΊμ λ λ°°μ΄μ ννλ λ€μκ³Ό κ°λ€. μ¬κΈ°μ λ¬Έμ λ₯Ό μ μ μλ€. rearμ frontμ κ°μ΄ μκΎΈ μ¦κ°νκΈ°λ§ ν΄μ κ²°κ΅­ λ°°μ΄μ μλΆλΆμ΄ λΉμ΄μλλΌλ λμ΄μ μ½μνμ§ λͺ»νλ κ²½μ°κ° λ°μνλ€. μ΄μ κ°μ κ³΅κ° λ­λΉλ₯Ό λ μ΄μ μ½μν  κ³΅κ°μ΄ μμ λ λ°°μ΄μ μμλ€μ μΈλ±μ€λ₯Ό νλμ© λΉκ²¨μ£Όλ λ°©λ²μΌλ‘ ν΄κ²°ν  μ μμ§λ§, μν νλ‘ κ΅¬ννλ©΄ λ μ½κ² ν΄κ²°ν  μ μλ€.

## β μν νμ κ΅¬ν
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

μ ν νμ λ¬Έμ μ μ λ°°μ΄μ μνμΈ κ²μ²λΌ νμ©ν¨μΌλ‘μ¨ ν΄κ²°ν  μ μλ€. μ¦ μ΄μ κ³Όλ λ€λ₯΄κ² frontμ rearκ° λ°°μ΄μ λ μΈλ±μ€μμ μ¦κ°νλ©΄μ μΈλ±μ€ 0μ κ°λ¦¬ν€λλ‘ νλ©΄ λλ€. μ΄λ λλ¨Έμ§ μ°μ°μΌλ‘ μ½κ² κ΅¬νν  μ μλ€. μ΄ μ½λμμ frontλ ν­μ νμ μ²« λ²μ§Έ μμμ νλ μμ, rearλ λ§μ§λ§ μμλ₯Ό κ°λ¦¬ν¨λ€.

![](https://images.velog.io/images/kcwthing1210/post/905166bd-3311-46ab-b8be-e00a8fdacebb/image.png)
μκΉμ λ§μ°¬κ°μ§λ‘ 5κ°μ μμλ₯Ό μ½μν λͺ¨μ΅μ΄λ€. μννλ‘ κ΅¬νν  μμ κ³΅λ°± μνμ ν¬ν μνλ₯Ό κ΅¬λΆνμ§ λͺ»νλ λ¬Έμ κ° μκΈ°λλ°, μ΄λ ν΄κ²°νκΈ° μν΄ μΈλ±μ€ νλλ λΉμλμλ€. μμ κ·Έλ¦Όμ μλ‘ λ€λ©΄, μΈλ±μ€λ₯Ό νλ λΉμλμ§ μμΌλ©΄ κ³΅λ°± μν, ν¬ν μν λͺ¨λ rearμ frontκ° μΈλ±μ€ 0μ κ°λ¦¬ν€λ λ¬Έμ κ° μκΈ΄λ€.

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

λ€μ μμ μ½λλ₯Ό μλμμΌλ³΄λ©΄ μ ν νλ‘ κ΅¬ννμ λμλ λ¬λ¦¬ ν¬ν μνλΌλ λ©μΈμ§ μμ΄ μ μμ μΌλ‘ μ½μλλ κ²μ νμΈν  μ μλ€.


# π§© Reference
- https://velog.io/@dongchyeon/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%81%90-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EA%B5%AC%ED%98%84

# π μ€ν
## β  μ€νμ΄λ?
μ€νμ ννλ₯Ό μ΄ν΄νκΈ° μν΄μλ νλ§κΈμ€ ν΅μ μκ°νλ©΄ νΈνλ€. μ°λ¦¬λ νλ§κΈμ€ ν΅μμ κ³Όμλ₯Ό λΉΌμ΄λ¨Ήμ λ κ°μ₯ λ§¨ μμ μλ κ³Όμλ₯Ό λΉΌμ΄λ¨ΉμΌλ©°, κ³Όμλ₯Ό λ£μ λλ λ§¨ μμ κ³Όμλ₯Ό λ£κ² λλ€. κ°μ₯ λ¦κ² λ€μ΄μ¨ κ²μ΄ κ°μ₯ μ²«λ²μ§Έλ‘ λκ°λ ννμ΄λ―λ‘ μ΄λ° μμΆλ ₯ ννλ₯Ό LIFO(Last-In First-Out)μ΄λΌκ³  νλ€.

![](https://images.velog.io/images/kcwthing1210/post/98967e6f-6cf5-4edc-a920-728e86c49dda/image.png)

μ€νμ ννλ₯Ό κ·Έλ¦ΌμΌλ‘ λνλΈ κ²μ΄λ€. μ€νμ μλ 1, 2, 3μ μ€νμ μμλΌκ³  λΆλ₯΄λ©°, κ°μ₯ μμ μλ μμλ μ€νμ μλ¨(top)μ΄λΌ λΆλ₯Έλ€.
λν, μ€νμ μμκ° νλλ λ€μ΄μμ§ μμ λλ κ³΅λ°±(empty) μνλΌ νκ³  κ½ μ°¨μ λ μ΄μ μμλ₯Ό μ§μ΄λ£μ§ λͺ»ν κ²½μ° ν¬ν(full) μνλΌκ³  νλ€.

![](https://images.velog.io/images/kcwthing1210/post/d06fe463-14d7-463a-b469-36814f2dc03b/image.png)

λ€μκ³Ό κ°μ΄ μ€νμ top μμλ₯Ό λΉΌμ€λ μ°μ°μ pop, μ€νμ topμ μλ‘μ΄ μμλ₯Ό μΆκ°νλ μ°μ°μ pushλΌκ³  νλ€. popμ κ²½μ° μ€νμ΄ κ³΅λ°±(empty) μνμΈμ§ νμΈν΄μΌ νλ©°, pushμ κ²½μ° μ€νμ΄ ν¬ν(full) μνμΈμ§ νμΈν΄μΌ νλ€.

## β μμ€ μ½λ κ΅¬ν

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

β stack.c

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

# π§© Reference
- https://velog.io/@dongchyeon/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9D-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0

# π Heap
## β ν(Heap)?
ν μλ£κ΅¬μ‘°λ μμ  μ΄μ§ νΈλ¦¬λ₯Ό κΈ°μ΄λ‘ νλ μλ£κ΅¬μ‘°μλλ€. μμ  μ΄μ§νΈλ¦¬λ λ§μ§λ§μ μ μΈν λͺ¨λ  λΈλμμ μμλ€μ΄ κ½ μ±μμ§ μ΄μ§νΈλ¦¬λ₯Ό λ§ν©λλ€.

![](https://images.velog.io/images/kcwthing1210/post/8cf41d77-f127-4de6-b4a0-3c265bf17ff1/image.png)

- νμ μ΅λν(Max heap)κ³Ό μ΅μν(Min Heap)μΌλ‘ λλ μ§λλ€. - μ΅λνμ λΆλͺ¨λΈλμ κ°μ΄ μμλΈλλ€μ κ°λ³΄λ€ ν­μ ν¬κ³ , μ΅μνμ λΆλͺ¨λΈλμ κ°μ΄ μμλΈλμ κ°λ³΄λ€ ν­μ μμ΅λλ€. (μ κ·Έλ¦Όμ μ΅λνμ μμ)
- μ΄λ¬ν μ±μ§ λλ¬Έμ ν­μ λμ¨ν μ λ ¬μν(λ°μ λ ¬ μν)λ₯Ό μ μ§ν©λλ€.
- νμ μ΅λκ° λλ μ΅μκ°μ μ½κ² λ½κΈ° μν μλ£κ΅¬μ‘° μμΌλ‘ μ€λ³΅μ νμ©ν©λλ€.

## β νμ λ°°μ΄λ‘ κ΅¬ννκΈ°
νμ λμ²΄μ μΌλ‘ λ°°μ΄λ‘ κ΅¬νλ©λλ€. μμ μ΄μ§νΈλ¦¬λ₯Ό κΈ°λ³ΈμΌλ‘ νκΈ° λλ¬Έμ λΉμλ κ³΅κ°μ΄ μμ΄ λ°°μ΄λ‘ κ΅¬ννκΈ°μ μ©μ΄ν©λλ€.

μλ κ·Έλ¦Όκ³Ό κ°μ΄ λ£¨νΈλΈλλ₯Ό λ°°μ΄μ 0λ² indexμ μ μ₯νκ³ , κ° λΈλλ₯Ό κΈ°μ μΌλ‘ μΌμͺ½ μμλΈλλ a[iβ2+1], μ€λ₯Έμͺ½ μμλΈλλ a[iβ2+2] μ indexμ μ μ₯λ©λλ€. λν νΉμ  indexμ λΈλμμ λΆλͺ¨λΈλλ a[(iβ1)//2]λ‘ μ°Ύμ μ μμ΅λλ€.
![](https://images.velog.io/images/kcwthing1210/post/517dc696-46d0-4a91-8875-2802fff32fdf/image.png)

## β μ½μκ³Ό μ­μ λ‘ κΉ¨μ§ νμ μ¬κ΅¬μ‘°ννκΈ°(heapify)

μ΅λνμ λΆλͺ¨λΈλλ ν­μ μμλΈλμ κ°λ³΄λ€ ν¬λ€λ μ‘°κ±΄μ κ°μ§κ³  μμ΅λλ€. νμ§λ§ νμμ μ½μ λλ μ­μ κ° μΌμ΄λκ² λλ©΄ κ²½μ°μ λ°λΌ μ΅λνμ μ‘°κ±΄μ΄ κΉ¨μ§ μ μμ΅λλ€. μ΄λ¬ν κ²½μ°μ μ΅λνμ μ‘°κ±΄μ λ§μ‘±ν  μ μκ² λΈλλ€μ μμΉλ₯Ό λ°κΏκ°λ©° νμ μ¬κ΅¬μ‘°ν(heapify) ν΄μ£Όμ΄μΌ ν©λλ€.

μ½μκ³Ό μ­μ μ κ²½μ° λͺ¨λ μ°μ° μμ²΄λ O(1)λ‘ μλνμ§λ§ heapifyμ κ³Όμ μ κ±°μΉκΈ° λλ¬Έμ O(logn)μ μκ°λ³΅μ‘λλ₯Ό κ°μ§κ² λ©λλ€.

### β μ½μ κ³Όμ  κ΅¬νκ³Όμ 
![](https://images.velog.io/images/kcwthing1210/post/f86acf4b-af7d-458f-b69f-51780fe3af7c/image.png)


### β μ­μ κ³Όμ  κ΅¬νκ³Όμ 
![](https://images.velog.io/images/kcwthing1210/post/ff53d335-2143-493b-b6ff-d63ecaf7ecf4/image.png)
![]

## β νμ΄ μλ λ°°μ΄μ νμΌλ‘ λ§λ€κΈ°(build heap)
heapifyμ κ²½μ° κΈ°λ³Έμ μΌλ‘ νμ λ§μ‘±νλ κ²½μ°μμ μ½μ λλ μ­μ κ° λ°μν  λ O(logn)μ μκ°λ³΅μ‘λλ‘ λ€μ νμΌλ‘ λ§λλ κ³Όμ μλλ€. build heapμ μ΄μ λ€λ₯΄κ² μμ νμ μ‘°κ±΄μ λ§μ‘±νμ§ μλ λ°°μ΄μ νμΌλ‘ λ§λλ κ³Όμ μλλ€. μ¬λ¬λ²μ heapify κ³Όμ μ κ±°μΉκΈ° λλ¬Έμ κ²°κ³Όμ μΌλ‘ μκ°λ³΅μ‘λλ O(nlogn)μλλ€.

### β μ¬κ·ν¨μλ₯Ό μ΄μ©ν μ¬κ΅¬μ‘°
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
	
    # λΆλͺ¨λΈλκ° λλ λΈλλ€λ§μ κ³¨λΌμ λ€μμλΆν° heapifyλ₯Ό μ°¨λ‘λ‘ μ€ν
    for i in range((N - 1) // 2, -1, -1):
        make_heap(array, i, heap_size)
       
```

# π§© Reference
- https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%ED%9E%99Heap