### Problem 1: [454. 4Sum II](https://leetcode.com/problems/4sum-ii/)
- **First Thought:**
	- Basically no idea other than use forloops
- **Problems:**
	- O(n^4)
- **Tips:**
	- Add up array1 and array 2, calculate a sum and set as key, appear count as val
	- then loop through 3 and 4, compare with the added result
		- if exists, add the value of the corresponding key with c + d.
```cpp
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        
        unordered_map<int, int> map;

        for(int a : nums1){
            for (int b : nums2){
                 map[a+b]++;
            }
        }     

        int count = 0;
        for (int c : nums3){
            for (int d : nums4){
                if (map.find(0 - (c + d)) != map.end()) {
                    count += map[0 - (c + d)];
                }
            }
        }   

        return count;
    }
};
```


### Problem 2: [383. Ransom Note](https://leetcode.com/problems/ransom-note/)
- **First Thought:**
	- Add all the letters from `magazine` into a map with number as key and appearance as value.
	- Then go through `ransomNote`  if any value goes into less than 0, return false. 

- **Problems:** Idea is the same but there is a better time complexity version, use array instead of map
- **Tips:**
	-  Check if ransomNote is larget than magazine it's definitely false.
	- Use array, use letter - a to start from 0 for array

```cpp
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        
        int record[26] = {0};

        if (ransomNote.size() > magazine.size()){
            return false;
        }

        for (int i = 0; i < magazine.size(); i++){
            record[magazine[i]-'a'] ++;
        }

        for (int j = 0; j < ransomNote.length(); j++) {
            record[ransomNote[j]-'a']--;
            if(record[ransomNote[j]-'a'] < 0) {
                return false;
            }
        }
        return true;
    }
};
```


### Problem 3: [15. 3Sum](https://leetcode.com/problems/3sum/)
- **First Thought:** 
	- Pointers would be helpful, since i, j, k won't be the same position with each other. 
	- 3 pointers, one from front, one from back and the last one from 
	- One for loop for the first pointer, one in the middle and last one from the back. 
- **Problems:**
	- duplicate numbers
	- The method it's still brute force solution

- **Tips:**
	- can sort the array first
	- Then the last position is the largest, the first will be the smallest
	- If the current first position + last position + mid position < 0, needs to find a larger number, 
		- mid pointer move right
		- if mid it's at the position before last, move first into second, move the mid pointer back to the next position
		- until the result is zero.
	- If the number and previous number it's the same, skip the number. 


### Problem 4: [18. 4Sum](https://leetcode.com/problems/4sum/)
- **First Thought:**
	- Sort the Array
	- use pointers, similar to the last question, add another loop
- **Tips:**
	- The exceptions
		- DO NOT: if first number k > target return false 
			- if there are more than one negative number, proceed to add more numbers.
			- Target could be negitive.
		- CORRECT VERSION: if numbers K > 0, Target > 0, K > Target, return false.
		- `Numbers[k] == numbers[k-1]` continue ----skip k, same number, remove duplicate
