# [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/description/)

这道题是一道比较简单的二分搜索题，最近的这几道题都是用二分搜索，这题的讨论要简单一点，正好适合看看二分的条件。

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int l = 0, r = nums.size()-1;
        if (nums.empty() || target < nums[0]) return 0;
        if (target > nums[r]) return r+1;
        
        /*
         * 此处用到<=，这样在只有一个元素的时候也可以进入这个循环，
         * 但于此同时，在后来mid的赋值中，l=mid+1而不是mid，r同理，
         * 这样才能保证可以顺利退出循环
         */
        while (l <= r) {
            int mid = (l+r)/2;

            // 找到target或者其所在的区间，则返回index，
            if (nums[mid] == target) return mid;
            if (nums[mid] < target && target <nums[mid+1]) return mid+1;
            
            if (nums[mid] < target) l = mid+1;
            else if (target < nums[mid]) r = mid-1;
        }
    }
};
```