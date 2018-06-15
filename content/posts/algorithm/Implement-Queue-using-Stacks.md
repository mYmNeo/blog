---
title: Implement Queue using Stacks
tags:
  - leetcode
  - algorithm
date: 2016-05-07 09:39:54
---
>
>Implement the following operations of a queue using stacks.
>
>+ push(x) -- Push element x to the back of queue.
>+ pop() -- Removes the element from in front of queue.
>+ peek() -- Get the front element.
>+ empty() -- Return whether the queue is empty.
>
>**Notes:**
>+ You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
>+ Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard >operations of a stack.
>+ You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).
>

### Analysis:
+ push,正常的方式push进去,如果stack为空的时候就记录第一入栈的数,该数值用来记录peek需要的值
+ pop,取栈顶值放到新的栈中直到stack的元素只剩下一个,退栈的时候记录peek的值
+ peek,返回peek值
+ empty,返回stack的empty
### Time and space complexity:
time:

push $\Theta (1)$

pop  $\Theta (n)$

peek $\Theta (1)$

empty $\Theta (1)$
### Code:
```cpp
class Queue {
public:
    // Push element x to the back of queue.
    void push(int x) {
        if (mock.empty()) {
            top = x;
        }
        mock.push(x);
    }

    // Removes the element from in front of queue.
    void pop(void) {
        std::stack<int> tmp;
        while (mock.size() > 1) {
            tmp.push(mock.top());
            mock.pop();
            top = tmp.top();
        }
        mock.pop();
        while (!tmp.empty()) {
            mock.push(tmp.top());
            tmp.pop();
        }
    }

    // Get the front element.
    int peek(void) {
        return top;
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return mock.empty();
    }
private:
    std::stack<int> mock;
    int top;
};
```
