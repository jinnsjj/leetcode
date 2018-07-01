#33. [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

这道题的核心思想在于原数组是一个递增，即使旋转后，也具有这一性质，只不过递增的数组变成了两个。所以使用binary search即可。但要注意一些细节，比如`if`中的条件`if (nums[mid] >= nums[left])`等号比不可少，因为`mid`的计算会向下取整。

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0, right = nums.size()-1;
        if (right == 0) return nums[0]==target?0:-1;
        while (left <= right){
            int mid = (left+right)/2;
            if (nums[mid]==target) return mid;
            if (nums[mid] >= nums[left]){
                if (target >= nums[left] && target < nums[mid]) right = mid-1;
                else left = mid+1;
            } else {
                if (target > nums[mid] && target <= nums[right]) left = mid+1;
                else right = mid-1;
            }
        }
        return -1;
    }
};
```























































































































