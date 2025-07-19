### Problem 1: [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
- **What's Reverse Polish Notation**
	- **1st** understanding : Regular expression to a tree and then Post Order Traversal the Tree
	- **2:** Understand through Stack
		- `3 + 4 * 5`
			- Stack
			- Push `3` → Stack: `[3]`
			- Push `4` → Stack: `[3, 4]`
			- Push `5` → Stack: `[3, 4, 5]`
			- Multiply `4 * 5` → Stack: `[3, 20]`
			- Add `3 + 20` → Stack: `[23]`
		- If met `+-*/` pop numbers and do the operation
		- If met number, push to stack.
	- **C++ tips**
		- *Type transfer*
			- `stoi`  String to int
			- `stol`   String to long
			- `stoll`  String to long long
			- `stof`   String to float
			- `stod`   String to double
		- `" "` it's for char or String, since question's tokens are in String only `" "` is useable.
		- `' '` it's for char only

```cpp
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;

        for (int i = 0; i < tokens.size(); i++) {
            if (tokens[i] == "+" || tokens[i] == "-" || tokens[i] == "*" || tokens[i] == "/") {
                int num1 = st.top();
                st.pop();
                int num2 = st.top();
                st.pop();
                if (tokens[i] == "+") st.push(num2 + num1);
                if (tokens[i] == "-") st.push(num2 - num1);
                if (tokens[i] == "*") st.push(num2 * num1);
                if (tokens[i] == "/") st.push(num2 / num1);
            } else {
                st.push(stoll(tokens[i]));
            }
        }
        int result = st.top();
        st.pop();
        return result;
    }
};
```

### Problem 2: [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)
- **Ideas:** 
	- use Priority Queue
		- pop discarded item
		- push new item
		- return largest number
	- !!! When the next element is larger than previous element, **pop the element directly!**
	- example :
		- k = 3
		- 1, 2, -1, -3, 5
		- push 1
		- push 2
			- 2 > 1 
			- pop 1
		- push -1 < 2, do nothing, `[2, -1]`
			- get max value =2
		- push -3 , all element > -1 , `[2, -1, -3]`
			- get max value = 2
		- since k = 3, pop3, push 5, 
			- 5 > all elements
			- pop -1, pop -3
			- max value = 5
- **Tips C++:**
	- deque, 
		- two sided operation, front and back
			- push_front()
			- push_back()
			- `int val = deque[1]`
		- Iterator supported, random access supported
	- queue
		- Strictly FIFO, no random access
- **Helper Function Private and Public**
	- For class Solution, helper class MyQueue it's private within the class. 
	- Within the Helper MyQueue everything it's public.
	
```cpp
class Solution {
private:

    class MyQueue{
    public:
        deque<int> que;

        void pop(int value){
            if(!que.empty() && value == que.front()){
                que.pop_front();
            }
        }

        void push(int value){
            while(!que.empty() && value > que.back()){
                que.pop_back();
            }
            que.push_back(value);
        }

        int front(){
            return que.front();
        }
    };


public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        MyQueue que;
        vector<int> result;

        for(int i = 0; i < k; i++){
            que.push(nums[i]);
        }

        result.push_back(que.front());

        for (int i = k; i < nums.size(); i++) {
            que.pop(nums[i - k]);
            que.push(nums[i]);
            result.push_back(que.front());
        }
        return result;
    }
};
```

### Problem 3: [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
- Not finished yet, will makeup tomorrow