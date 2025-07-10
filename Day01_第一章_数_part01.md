###  Problem 1: [704. Binary Search](https://leetcode.com/problems/binary-search/)
- Be careful about the boundary change when moving the boundary 
	- `mid = (left + right) / 2`  could be out of boundary
	- `mid = left + (right - left) / 2` is a better way
- Different Boundary Problem
	- `[left, right]`
		- right = length - 1;
		- `left <= right` since right is included 
		- `right = mid - 1` or `left = mid + 1`
	- `[left, right)`
		- right = length
		- left < right
		- `right = mid` or `left = mid + 1

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int len = nums.size();
        int left = 0;
        int right = len- 1;
 
        while(left <= right) {
            int mid = left + ((right - left)/2);

            if (nums[mid] > target){
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                return mid;
            }
        }
        return -1 ;  
    }
};

```

### Problem 2: [27. Remove Element](https://leetcode.com/problems/remove-element/)
- Fast and slow pointers is reducing the time complexity from O(n^2) to O(n). 
- Don't forget to move the slow pointer when `nums[fast] != val`, else all the replacement will be done to the same posion.

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {

        int length = nums.size();
        int slow = 0;
        
        for (int fast = 0; fast < length; fast++){
            if (nums[fast] != val){
                nums[slow] = nums[fast];
                slow++;
            }
        }
        return slow;

    }
};
```

### Problem 3: [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)
- Idea: since it's non descending, the square of the first number or the last number will be the largest. 
	- Insert into a new array from back to front, a sort won't be necessary anymore. 
	- how to insert into array from back to front. 
	- have 2 pointers, one in front, one in back -> comes to the mid and compare the squares

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        
        int left = 0;
        int len = nums.size();
        int right = len - 1;

        vector<int> result(len); //create a new array with size of curr length
        int index = len - 1;

        while(left <= right){
            int leftSquare = nums[left] * nums[left];
            int rightSquare = nums[right] * nums[right];

            if (leftSquare > rightSquare){
                result[index] = leftSquare;
                left ++;
            } else {
                result[index] = rightSquare;
                right --;
            }
            index --;
        }
        return result;
    }
};
```