Q1.Design and implement a stack using an array without using any built-in stack library. Perform the following operations:
•	PUSH(x)
•	POP()
•	PEEK()
•	DISPLAY()
Your program must handle both Stack Overflow and Stack Underflow conditions.
Additional Task:
Explain the time complexity and space complexity of each operation. Also discuss what happens when the stack size is fixed and the user attempts to insert more elements than its capacity.
Answer-
A stack is a linear data structure that follows LIFO (Last In, First Out).
C Program
#include <stdio.h>

#define MAX 5

int stack[MAX];
int top = -1;

// PUSH operation
void push(int x) {
    if (top == MAX - 1) {
        printf("Stack Overflow! Stack is full.\n");
    } else {
        top++;
        stack[top] = x;
        printf("%d pushed into stack.\n", x);
    }
}

// POP operation
void pop() {
    if (top == -1) {
        printf("Stack Underflow! Stack is empty.\n");
    } else {
        printf("%d popped from stack.\n", stack[top]);
        top--;
    }
}

// PEEK operation
void peek() {
    if (top == -1) {
        printf("Stack is empty.\n");
    } else {
        printf("Top element is: %d\n", stack[top]);
    }
}

// DISPLAY operation
void display() {
    if (top == -1) {
        printf("Stack is empty.\n");
    } else {
        printf("Stack elements are:\n");
        for (int i = top; i >= 0; i--) {
            printf("%d\n", stack[i]);
        }
    }
}

int main() {
    int choice, x;
    while (1) {
        printf("\n--- STACK MENU ---\n");
        printf("1. PUSH\n");
        printf("2. POP\n");
        printf("3. PEEK\n");
        printf("4. DISPLAY\n");
        printf("5. EXIT\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
      switch (choice) {
            case 1:
                printf("Enter element: ");
                scanf("%d", &x);
                push(x);
                break;
            case 2:
                pop();
                break;
            case 3:
                peek();
                break;
            case 4:
                display();
                break;
            case 5:
                return 0;
            default:
                printf("Invalid choice!\n");
        }
    }
}
Time and Space Complexity
Operation
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
Overall stack space: O(MAX) because the array has a fixed capacity.
Stack Overflow
If the stack size is fixed at 5 and 5 elements are already stored, trying to insert another element causes Stack Overflow.
Example:
Stack: 50 40 30 20 10
Top = 4

PUSH(60)
→ Stack Overflow
→ 60 is not inserted
Stack Underflow
If the stack is empty and POP() or PEEK() is performed, it causes Stack Underflow.
Stack is empty

POP()
→ Stack Underflow

Q2. Implement a Circular Queue using an array. The queue should support:
•	ENQUEUE(x)
•	DEQUEUE()
•	FRONT()
•	DISPLAY()
The implementation must correctly distinguish between a full queue and an empty queue.
Additional Task:
Compare the circular queue with a simple linear queue and explain:
1.	Why a circular queue provides better utilization of memory.
2.	Time complexity of ENQUEUE and DEQUEUE.
3.	Space complexity of the queue.
4.	What problem occurs in a linear queue when REAR reaches the last index even though unused positions exist at the beginning?
Answer-
C Program: Circular Queue Using Array
#include <stdio.h>
#define MAX 5

int queue[MAX];
int front = -1, rear = -1;

void enqueue(int x)
{
    if ((rear + 1) % MAX == front)
    {
        printf("Queue Overflow\n");
        return;
    }
    if (front == -1)
        front = 0;
    rear = (rear + 1) % MAX;
    queue[rear] = x;
    printf("%d inserted\n", x);
}

void dequeue()
{
    if (front == -1)
    {
        printf("Queue Underflow\n");
        return;
    }
    printf("%d deleted\n", queue[front]);
    if (front == rear)
    {
        front = rear = -1;
    }
    else
    {
        front = (front + 1) % MAX;
    }
}

void peek()
{
    if (front == -1)
        printf("Queue is Empty\n");
    else
        printf("Front = %d\n", queue[front]);
}

void display()
{
    if (front == -1)
    {
        printf("Queue is Empty\n");
        return;
    }
    int i = front;
    printf("Queue: ");
    while (1)
    {
        printf("%d ", queue[i]);
        if (i == rear)
            break;
        i = (i + 1) % MAX;
    }
    printf("\n");
}

int main()
{
    enqueue(10);
    enqueue(20);
    enqueue(30);
    enqueue(40);
    enqueue(50)
    display();
    dequeue();
    dequeue();
    enqueue(60);
    enqueue(70);
    display();
    peek();
    return 0;
}
Comparison: Circular Queue vs Linear Queue
Learn more
Point
Circular Queue
1. Memory utilization
Reuses empty positions created after DEQUEUE(), so memory is utilized efficiently.
2. ENQUEUE
O(1)
DEQUEUE
O(1)
3. Space complexity
O(n), where n is queue capacity.
4. Problem in linear queue
When REAR reaches the last index, insertion stops even if empty spaces exist at the beginning. This causes wastage of memory and is called false overflow.
Key condition
Queue Full:
(rear + 1) % MAX == front
Queue Empty:
front == -1
Main advantage: Circular queue allows REAR to wrap around to the beginning and reuse previously freed spaces.
1. Why does a circular queue provide better utilization of memory?
Answer-
A circular queue reuses the empty spaces created at the beginning after DEQUEUE(). Therefore, no memory space is wasted.
2. Time complexity of ENQUEUE and DEQUEUE:
Answer-
ENQUEUE: O(1)
DEQUEUE: O(1)
Both operations take constant time because they only update front or rear.
3. Space complexity of the queue:
Answer-
The space complexity is O(n), where n is the maximum size of the queue.
4. What problem occurs in a linear queue when REAR reaches the last index?
Answer-
In a linear queue, when REAR reaches the last index, no more elements can be inserted, even if there are empty positions at the beginning. This is called false overflow and causes wastage of memory.



