
### Problem 1: [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

- Sliding Window
- The initial result needs to be set to infinity instead of set to 0
	- Since we are looking for the smallest length possible, we want a smaller than prior result
	- If initial Set to 0, the first compare needs to be: `subLength > result` 
	- Later comparason needs to be `subLength < result`  which brings a problem.
- Initial Result needs to be `INT32_MAX` 
- Remember to delete from sum first then move pointer.

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int left = 0;
        int length = nums.size();

        int sum = 0;
        int subLength = 0;
        int result = INT32_MAX;

        for(int right = 0; right < length; right ++){
            sum += nums[right];
            while(sum >= target){
                subLength = (right - left) + 1;
                if (subLength < result){
                    result = subLength;
                }
                sum -= nums[left];
                left++;
            }
        }

        if(result != INT32_MAX){
            return result;
        } else {
            return 0;
        } 
		// return result != INT32_MAX ? result : 0;
    }
};
```

### Problem 2: [59. Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/)
- When approach this question when length = n, 
	- the square ` Top length = n`, left to right
	- `right = n - 1` since there is an overlap
	- `bottom length = n - 1`
	- `left = n - 2`
	- repeat to go inside  until the last number, 
- How to stop the repeat, if length = n 
	- total number of squares = n^2
- Top = 0, bottom = n-1
- left = 0, right  = n-1

```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> matrix(n, vector<int>(n));
        int num = 1;
        int top = 0, bottom = n - 1, left = 0, right = n - 1;
        while (num <= n * n) {
            for (int i = left; i <= right; i++) {
                matrix[top][i] = num++;
            }
            top++;

            for (int i = top; i <= bottom; i++) {
                matrix[i][right] = num++;
            }
            right--;

            for (int i = right; i >= left; i--) {
                matrix[bottom][i] = num++;
            }
            bottom--;

            for (int i = bottom; i >= top; i--) {
                matrix[i][left] = num++;
            }
            left++;
        }

        return matrix;
    }
};
```