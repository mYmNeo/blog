---
title: Implement Stack using Queues
tags:
  - leetcode
  - algorithm
date: 2016-05-09 15:41:43
---
>
Implement the following operations of a stack using queues.

+ push(x) -- Push element x onto stack.
+ pop() -- Removes the element on top of the stack.
+ top() -- Get the top element.
+ empty() -- Return whether the stack is empty.

**Notes:**

+ You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.
+ Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
+ You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).
>

### Analysis:
双队列
+ push的时候记录最后一次push的元素,这样top的时候就可以迅速直到top的结果
+ pop,弹出队列元素到新队列里面,剩余最后一个元素的时候停止
+ top,返回对应变量
+ empty,队列的empty
### Time and space complexity:
time:

push $\Theta (1)$

pop  $\Theta (n)$

top $\Theta (1)$

empty $\Theta (1)$
### Code:
```cpp
class Stack {
public:
    // Push element x onto stack.
    void push(int x) {
        mock.push(x);
    }

    // Removes the element on top of the stack.
    void pop() {
        std::queue<int> tmp;
        while (mock.size() > 1) {
            tmp.push(mock.front());
            mock.pop();
        }
        mock.swap(tmp);    
    }

    // Get the top element.
    int top() {
        return mock.back();
    }

    // Return whether the stack is empty.
    bool empty() {
        return mock.empty();
    }
private:
    std::queue<int> mock;
};
```
