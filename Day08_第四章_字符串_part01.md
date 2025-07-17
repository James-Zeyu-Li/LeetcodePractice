### Problem 1: [344. Reverse String](https://leetcode.com/problems/reverse-string/)
- **First Thought:**
	- Use 2 pointers, one from the back one from front, swap the positions until the mid point of the array.
	
```cpp
class Solution {
public:
    void reverseString(vector<char>& s) {
        int left = 0;
        int right = s.size()-1;

        while (left < right){
            swap(s[left], s[right]);
            left ++;
            right --;
        }
    }
};
```

### Problem 2: [541. Reverse String II](https://leetcode.com/problems/reverse-string-ii/)
- **First Thought:**
	- Fast and slow pointers
	- moves at the speed of K
- **Problems:**
	- Not sure how to reverse the first k numbers.
- **Tips:** 
	- **can use a for loop to move at 2k speed directly.**
	- Reverse Function 
		- reverse(s.begin(), s.end())
			- s = "12345"
			- s = "54321"
	
	```cpp
class Solution {
public:
    string reverseStr(string s, int k) {
        
        int slow = 0;
        int fast = 0;

        for(int i = 0; i < s.size(); i += (2*k)){
            if(i+k <= s.size()){
                reverse(s.begin()+i, s.begin()+i+k );
            } else {
                reverse(s.begin() + i, s.end());
            }
        }    
        return s;    
    }
};
```

### Problem 3: [54. 替换数字（第八期模拟笔试](https://kamacoder.com/problempage.php?pid=1064)
- **First Thought:**
	- Find the numbers
	- Create a new String with the replaced word

- **Problems:**
	- The size of the String is unknown
	- How to change the size of the String inplace without extra space

- **Tips**
	- Find out how many numbers there are, counter
	- expand size of number * 5 size
	- Add the chars from back to front replace num by chars