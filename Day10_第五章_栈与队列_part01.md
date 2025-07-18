
### Problem 1: [232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)
- **Ideas**
	- Stack is LIFO, but QUEUE is FIFO
- `pop`
	- Since pop should be the **TOP** element in Stack, which is last element in queue, we should pop the Fist item in. 
	- Have 2 Stack, Put every **TOP** element in the other queue then pop the element, then pop TOP element from second queue.
- `peek`
	- 
```cpp
class MyQueue {
public:

    stack<int> inputStack;
    stack<int> outputStack;

    MyQueue() {}
    
    void push(int x) {
        inputStack.push(x);
    }
    
    int pop() {
        if (outputStack.empty()){
            while (!inputStack.empty()){
                outputStack.push(inputStack.top());
                inputStack.pop();
            }
        }
        int result = outputStack.top();
        outputStack.pop();
        return result;
    }
    
    // peek as a list not as a queue
    int peek() {
        if (outputStack.empty()) {
            while (!inputStack.empty()) {
                outputStack.push(inputStack.top());
                inputStack.pop();
            }
        }
        return outputStack.top(); 
    }
    
    bool empty() {
        return inputStack.empty() && outputStack.empty();
    }
};
```
### Problem 2: [225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/)
- **Ideas:**
	- `pop()`
		- Since both queues are FIFO, If want to pop the top item like a Stack, it's the last element
		- Which means needs to remove the element in front of the last element in Queue, which means move all element to another queue but the last one. 
		- pop the last element, `swap(q1, q2)`;
	- `top()`;
		- Similar to `pop`, but push the last element back instead of pop the element.

```cpp
class MyStack {
public:

    queue<int> q1;
    queue<int> q2;

    MyStack() { }
    
    void push(int x) {
        q1.push(x);
    }
    
    int pop() {
        int size = q1.size();
        size--;
        while(size --){
            q2.push(q1.front());
            q1.pop();
        }

        int result = q1.front();
        q1.pop();

        swap(q1, q2);
        return result;
    }   
    
    int top() {
        int size = q1.size();
        size --;
        while(size --){
            q2.push(q1.front());
            q1.pop();
        }        

        int result = q1.front();
        q2.push(result);
        q1.pop();

        swap(q1, q2);
        return result;
    }
    
    bool empty() {
        return q1.empty();
    }
};
```

### Problem 3: [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
- **Tips:**
	- Stack is the best use, since all the Parentheses comes in pairs.
	- If` ) `exists, there must be a `(` in the stack
	- If stack is empty, or if `)` is the next parentheses ( must be the top item on stack.
	- if `(`, push the opposite side `)` into the stack.
	- So, if the top doesn't match the next element, false

```cpp
class Solution {
public:
    bool isValid(string s) {
        if (s.size() % 2) return false;

        stack<char> st;
        
        for (char c : s) {
            if (c == '(') st.push(')');
            else if (c == '[') st.push(']');
            else if (c == '{') st.push('}');
            else if (st.empty() || c != st.top()) return false;
            else st.pop();
        }
        return st.empty();
    }
};
```

### Problem 4: [1047. Remove All Adjacent Duplicates In String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
- **Tips:**
	- use a stack, since if duplicate char
	- if `s[i] == stack.top()`
		- pop top, move to next char.