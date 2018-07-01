# [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/description/)

与上一题几乎一模一样，代码也可以复用。问题在于这次不可以重复，自然就想到了把DFS函数中的start加1。然而由于candidates中存在同样的数字，所以重复不能完全避免。另一方面，重复的数字是有必要出现在combination中的。这又使我苦恼。参考大佬：<http://www.cnblogs.com/grandyang/p/4419386.html>解决方案是加入一个if判断。

这个让我重新思考了递归，应当从两个角度去理解递归，一个是横向的（同一级的递归的不同情况），而另一个是纵向的（不同级的递归）。这一题中，我们要避免的是横向的数字重复。所以在DFS这一级加入if判断。

---

```cpp
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<vector<int>> res;
        vector<int> out;
        sort(candidates.begin(), candidates.end());
        combinationSumDFS(candidates, target, 0, res, out);
        return res;
    }
    void combinationSumDFS(vector<int>& candidates, int target, int start, vector<vector<int>>& res, vector<int>& out) {
        if (target < 0) return;
        if (target == 0) {
            res.push_back(out);
            return;
        }
        for (int i = start; i < candidates.size(); i++){
            if (i>start && candidates[i]==candidates[i-1]) continue;
            out.push_back(candidates[i]);
            combinationSumDFS(candidates, target-candidates[i], i+1, res, out);
            out.pop_back();
        }
    }
};
```