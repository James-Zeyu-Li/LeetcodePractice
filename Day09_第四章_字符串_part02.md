### Problem 1: [151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)
- **First Thought:**
	- Remove Extra spaces, resize the String 
		- Use two pointers, a fast pointers and a slow pointers
			- Slow pointers point to the first letter that is not a " "
			- Fast pointer points to the letter that is not a " "
			- If letter's next it's all " " space and reaches the end, remove all the space in the end.
	- reverse the words
- **Problems:**
	- If use the reverse function, all the letters will be reverse
	- How to reverse the chars back.

- **Tips:**
	- Have a `pointer` to find the location of the first ' ' after the first word
	- use a counter, count the chars from beginning that is not a ' '
	- Reverse the segment `reverse(s.begin() + start, s.begin() + end);`
	- Start next from the `pointer + 1` location

```cpp
class Solution {
public:
    string reverseWords(string s) {
        
        int slow = 0;

        for(int fast = 0; fast <s.size(); fast ++){
            if (s[fast] != ' '){

                if (slow != 0){
                    s[slow++] = ' ';
                }

                while (fast < s.size() && s[fast] != ' '){
                    s[slow ++] = s[fast ++];
                }
            }
        }

        s.resize(slow);

        reverse(s.begin(), s.end());

        int start = 0;
        for( int end = 0; end <= s.size (); ++end){
            if (end == s.size() || s[end] == ' '){
                reverse(s.begin() + start, s.begin() + end);
                start = end + 1;
            }
        }

        return s;
    }
};
```

### Problem 2: [卡码网：55.右旋转字符串](https://programmercarl.com/kamacoder/0055.%E5%8F%B3%E6%97%8B%E5%AD%97%E7%AC%A6%E4%B8%B2.html)
- **First Thought:**
	- Calculate the length separate the String into two segments
	- If the length of the String is smaller than K, skip
	- Reverse the segment size - k to end
	- Reverse 0 to size - k - 1
	- Then reverse all the chars

```cpp
void rightRotate(string &s, int k) {
    int n = s.size();
    if (n == 0 || k <= 0) return;
    k %= n; 
    
    reverse(s.begin() + (n - k), s.end());
    
    reverse(s.begin(), s.begin() + (n - k));
    
    reverse(s.begin(), s.end());
}
```

### Problem 3: [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)
暂时跳过



### Problem 4: [459. Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern/)
暂时跳过