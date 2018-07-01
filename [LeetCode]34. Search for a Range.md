# [34. Search for a Range](https://leetcode.com/problems/search-for-a-range/description/)

与上一题很相似，原理很清晰，两次二分搜索，一次找前边界一次找后边界，不必在找到target后直接break。但我真的是太讨厌二分搜索了，边界条件实在头疼。

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int l = 0, r = nums.size()-1;
        vector<int> res(2,-1);
        if (nums.empty()) return res;
        if (nums.size()==1 && nums[0] == target) return (vector<int>){0,0};  
        while (l < r){
            int mid = (l+r)/2;
            if (nums[mid]<target) l = mid+1;
            else r = mid; 
        }
        if (nums[r]!=target) return res;
        res[0] = r;
        r = nums.size();///!!!
        while (l < r){
            int mid = (l+r)/2;
            if (nums[mid]>target) r = mid;
            else l = mid+1;
        }
        res[1] = l-1;//!!!
        return res;
    }
};
```

## Reference

> <http://www.cnblogs.com/grandyang/p/4409379.html>





































































