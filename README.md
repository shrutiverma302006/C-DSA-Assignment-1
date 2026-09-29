o# C-DSA-Assignment-1
Q1. Design and Implement a Stack Using an Array

Aim-
To implement a Stack using an array without using any built-in stack library and perform the following operations:
PUSH(x)
POP()
PEEK()
DISPLAY()
The program should also handle Stack Overflow and Stack Underflow conditions.

Theory-
A Stack is a linear data structure that follows the LIFO (Last In, First Out) principle. The element inserted last is removed first.
For example:
PUSH(10)
PUSH(20)
PUSH(30)

Stack:
| 30 |  <- TOP
| 20 |
| 10 |
If POP() is performed, 30 will be removed first.

Stack Operations-
PUSH(x) – Inserts an element at the top.
POP() – Removes the top element.
PEEK() – Displays the top element without removing it.
DISPLAY() – Displays all elements from top to bottom.
Stack Overflow-
When the stack is already full and we try to insert another element, Stack Overflow occurs.
Stack Underflow-
When the stack is empty and we try to remove or access an element, Stack Underflow occurs.

Algorithm-
PUSH(x)
Check whether top == MAX - 1.
If true, display Stack Overflow.
Otherwise increment top.
Store x at stack[top].
POP()
Check whether top == -1.
If true, display Stack Underflow.
Otherwise display/remove stack[top].
Decrement top.
PEEK()
Check whether top == -1.
If true, display Stack Underflow.
Otherwise display stack[top].
DISPLAY()
Check whether top == -1.
If true, display that the stack is empty.
Otherwise traverse from top to 0 and display the elements.
#include <iostream>
using namespace std;

#define MAX 5

class Stack
{
private:
    int stack[MAX];
    int top;

public:
    Stack()
    {
        top = -1;
    }

    // PUSH operation
    void PUSH(int x)
    {
        if (top == MAX - 1)
        {
            cout << "Stack Overflow!" << endl;
            return;
        }

        top++;
        stack[top] = x;

        cout << x << " pushed into stack." << endl;
    }

    // POP operation
    void POP()
    {
        if (top == -1)
        {
            cout << "Stack Underflow!" << endl;
            return;
        }

        cout << stack[top] << " popped from stack." << endl;
        top--;
    }

    // PEEK operation
    void PEEK()
    {
        if (top == -1)
        {
            cout << "Stack Underflow! Stack is empty." << endl;
            return;
        }

        cout << "Top element: " << stack[top] << endl;
    }

    // DISPLAY operation
    void DISPLAY()
    {
        if (top == -1)
        {
            cout << "Stack is empty." << endl;
            return;
        }

        cout << "Stack elements are:" << endl;

        for (int i = top; i >= 0; i--)
        {
            cout << stack[i] << endl;
        }
    }
};

int main()
{
    Stack s;

    s.PUSH(10);
    s.PUSH(20);
    s.PUSH(30);

    s.DISPLAY();

    s.PEEK();

    s.POP();

    s.DISPLAY();

    return 0;
}
Complexity Analysis-
Operation:
Time Complexity
Space Complexity
PUSH
O(1)
O(1)
POP
O(1)
O(1)
PEEK
O(1)
O(1)
DISPLAY
O(n)
O(1)
The complete stack requires O(n) space, where n is the maximum stack capacity.
Fixed-Size Stack:
If the stack size is fixed, for example MAX = 5, it can contain only 5 elements.
If the user tries:
PUSH(10)
PUSH(20)
PUSH(30)
PUSH(40)
PUSH(50)
PUSH(60)
the sixth insertion cannot be performed because the array is full. Therefore, Stack Overflow occurs.

Q2. Implement a Circular Queue Using an Array?

Aim-
To implement a Circular Queue using an array and perform:
ENQUEUE(x)
DEQUEUE()
FRONT()
DISPLAY()
The implementation must correctly distinguish between a full queue and an empty queue.

Theory-
A Queue is a linear data structure that follows the FIFO (First In, First Out) principle.
The element inserted first is removed first.
A Circular Queue is a queue in which the last position of the array is connected back to the first position.
For an array of size 5:
0 -> 1 -> 2 -> 3 -> 4
^                   |
|___________________|
When rear reaches the last index, it can move back to index 0 if space is available.

Circular Queue Operations-
ENQUEUE(x) – Inserts an element at the rear.
DEQUEUE() – Removes an element from the front.
FRONT() – Displays the front element.
DISPLAY() – Displays all queue elements.
Empty Condition
The queue is empty when:
front == -1
Full Condition
The queue is full when:
(rear + 1) % MAX == front
This condition allows us to use the unused positions at the beginning of the array.

Algorithm-
ENQUEUE(x)
Check whether (rear + 1) % MAX == front.
If true, display Queue Overflow.
If the queue is empty, set front = rear = 0.
Otherwise set:
rear = (rear + 1) % MAX;
Insert the element at queue[rear].
DEQUEUE()
Check whether front == -1.
If true, display Queue Underflow.
Otherwise remove queue[front].
If front == rear, set both to -1.
Otherwise:
front = (front + 1) % MAX;
FRONT()
Check whether the queue is empty.
If empty, display Queue Underflow.
Otherwise display queue[front].
DISPLAY()
Check whether the queue is empty.
Start from front.
Continue until rear is reached.
Use modulo operation to move circularly.
#include <iostream>
using namespace std;

#define MAX 5

class CircularQueue
{
private:
    int queue[MAX];
    int front;
    int rear;

public:
    CircularQueue()
    {
        front = -1;
        rear = -1;
    }

    // ENQUEUE operation
    void ENQUEUE(int x)
    {
        // Check for full queue
        if ((rear + 1) % MAX == front)
        {
            cout << "Queue Overflow! Queue is full." << endl;
            return;
        }

        // If queue is empty
        if (front == -1)
        {
            front = 0;
            rear = 0;
        }
        else
        {
            rear = (rear + 1) % MAX;
        }

        queue[rear] = x;

        cout << x << " inserted into queue." << endl;
    }

    // DEQUEUE operation
    void DEQUEUE()
    {
        if (front == -1)
        {
            cout << "Queue Underflow! Queue is empty." << endl;
            return;
        }

        cout << queue[front] << " removed from queue." << endl;

        // If only one element is present
        if (front == rear)
        {
            front = -1;
            rear = -1;
        }
        else
        {
            front = (front + 1) % MAX;
        }
    }

    // FRONT operation
    void FRONT()
    {
        if (front == -1)
        {
            cout << "Queue is empty." << endl;
            return;
        }

        cout << "Front element: " << queue[front] << endl;
    }

    // DISPLAY operation
    void DISPLAY()
    {
        if (front == -1)
        {
            cout << "Queue is empty." << endl;
            return;
        }

        cout << "Queue elements are: ";

        int i = front;

        while (true)
        {
            cout << queue[i] << " ";

            if (i == rear)
                break;

            i = (i + 1) % MAX;
        }

        cout << endl;
    }
};

int main()
{
    CircularQueue q;

    q.ENQUEUE(10);
    q.ENQUEUE(20);
    q.ENQUEUE(30);
    q.ENQUEUE(40);
    q.ENQUEUE(50);

    q.DISPLAY();

    q.FRONT();

    q.DEQUEUE();
    q.DEQUEUE();

    q.DISPLAY();

    q.ENQUEUE(60);
    q.ENQUEUE(70);

    q.DISPLAY();

    return 0;
}
Comparison: Circular Queue vs Linear Queue

Feature
Linear Queue
Circular Queue
Structure
Linear
Circular
Memory utilization
May leave unused positions
Better utilization of array positions
ENQUEUE
O(1)
O(1)
DEQUEUE
O(1)
O(1)
Space
O(n)
O(n)
Reuses deleted positions
Usually no
Yes
Rear movement
Only forward
Wraps around using modulo

1. Why does a Circular Queue provide better utilization of memory?
   
In a simple linear queue, suppose the array size is 5:
[10] [20] [30] [40] [50]
 F                   R
After deleting the first two elements:
[  ] [  ] [30] [40] [50]
          F         R
Positions 0 and 1 are empty, but a simple linear queue may not be able to use them again if rear has already reached the last index.
A circular queue solves this problem by moving rear back to the beginning:
[60] [70] [30] [40] [50]
 R     R? 
Thus, previously freed positions can be reused.

2. Time Complexity of ENQUEUE and DEQUEUE.

Both operations take:
ENQUEUE = O(1)
DEQUEUE = O(1)
No shifting of elements is required. The front and rear are simply moved using the modulo operation.

3. Space Complexity in a queue.
   
For an array of size n, the circular queue requires:
Space Complexity = O(n)
because the array can store at most n elements.

4. Problem with a Linear Queue When REAR Reaches the Last Index.

Consider:
[  ] [  ] [30] [40] [50]
                    R
Although the first two positions are empty, rear is already at the last index.
A simple linear queue may report Queue Overflow when trying to insert another element because there is no position after rear.
This is sometimes called false overflow or false full condition.
A circular queue avoids this problem by using:
rear = (rear + 1) % MAX;
Therefore, rear can move from the last index back to the first available position.
