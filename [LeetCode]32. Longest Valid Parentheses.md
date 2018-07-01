# [Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/description/)

括号的题目自然就想到了使用stack，然而自己最开始的想法还沿用之前的思路，用一个`stack<char> stk`来记录括号，这导致了括号位置信息的丢失，思考起来很麻烦，于是参考了别人的解答。
启发我的地方是栈 `stack<int> stk` 用来记录开括号的位置。

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        
        stack<int> stk;
        int res = 0;
        int start = 0;
        
        for (int i = 0; i<s.size(); i++)
        {
            if (s[i]=='(') stk.push(i);// 遇到'('则入栈
            else if (stk.empty()) start = i+1;// 当栈中所有的'('都被匹配了，又遇到闭括号，表示此处需要断开
            else {
                stk.pop();
                // 当栈为空，说明前方所有开括号均被匹配，可以和前一串相连，若不为空则不相连
                res = stk.empty() ? max(res, i-start+1) : max(res, i-stk.top());
            }
        }
        return res;
    }
};
```
DP的解法我还不太熟悉，今后学习了DP后再来研究。

## Reference
> [stack 解法](http://www.cnblogs.com/grandyang/p/4424731.html)
> [DP 解法](http://bangbingsyb.blogspot.com/2014/11/leetcode-longest-valid-parentheses.html)




















































































































































































































































