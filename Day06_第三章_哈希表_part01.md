### Problem 1: [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)
- **First Thought:**
	- 1: Sort the Strings and compare : O(nlogn) time complexity
	- 2: Use a hashMap: o(n)
		- Create a empty hashmap
		- count the character,
			- if in S, + 1 for the character
			- If in t , - 1 for the character.
			- All value should be 0 if Anagram
- **Tip:** ASCII code of letters can turn letters into numbers.
	- Use the letter - a can use 0-25 for A - Z;

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        int record[26] = {0};

        for (int i=0; i<s.size(); i++){
            record[s[i] - 'a']++;            
        }

        for (int j=0; j<t.size(); j++){
            record[t[j] - 'a']--;            
        }

        for(int n=0; n<26; n++){
            if(record[n] != 0) {
                return false;
            }
        }
        return true;
    }
};
```


### Problem 2: [349. Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/)
- **First Thought:**
	- brute force solution: loop through all numbers 
- **Tips:**
	- If asking about anything unique, hash set will be the thing to think about first
		- set: ordered, can not duplication, find O(log n), add delete O(log n)
		- unordered_set : not ordered, no duplicate,  find O(1), add delete O(1)
		- multiset: Ordered, can duplicate,  find O(log n), add delete O(log n);

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> resultSet;
        int hash[1005] = {0}; // set larget than 1000 to avoid over boundary 
        
        for (int num : nums1) {
            hash[num] = 1;
        }
        
        for (int num : nums2) {
            if (hash[num] == 1){
                resultSet.insert(num);
            }
        }
        return vector<int>(resultSet.begin(), resultSet.end());
    }
};
```

### Problem 3: [202. Happy Number](https://leetcode.com/problems/happy-number/)
- **First Thought:**
	- Happy number : if 19 -》 1^2 + 9^2 = 82 -> 8^2 + 2^2 = 68 ... -> = 1it's happy
	- Then the problem will be , when does the result starts the infinity loop
- **Error Note**
	- could use n/=10 to quickly remove the last digit of n
	- Important set operations - set.find(), set.end(), set.insert()
	- Don't forget to set n=sum after each round of calculation.
 
```cpp
class Solution {
public:
    bool isHappy(int n) {
        unordered_set<int> sumSet;

        while(true){
            int sum = getSum(n);
            if (sum == 1){
                return true;
            }

            if (sumSet.find(sum) != sumSet.end()){
                return false;
            } else {
                sumSet.insert(sum);
            }

            n=sum;
        }
    }

    int getSum(int n){
        int sum=0;
        while (n){
            sum += (n%10) * (n%10);
            n/= 10; // get rid of the last number
        }
        return sum;
    }
};
```

### Problem 4: [1. Two Sum](https://leetcode.com/problems/two-sum/)

- **First Thought:**
	- Needs to know the position and the value of the numbers that have been traversed.
	- Need to save the information to find the paired number, fo rexample target = 9, position 5 num = 1, need to find if there is a position value of 8
	- Key : Value
- What do we want to find
	-  The **value** of each position
	- The **value** of each Position should be key
	- The position should be the **value of map**
	- Find the paired VALUE then retrive the position that's the **value of map**

- Note: learn how iterator works, how map.find, map.insert works
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::unordered_map<int, int> map;

        for(int i = 0; i < nums.size(); i++) {
            auto iter = map.find(target - nums[i]);
            if (iter != map.end()){
                return {iter->second, i};
            } 

            map.insert(pair<int, int>(nums[i], i)); 
        }

        return{};
        
    }
};
```