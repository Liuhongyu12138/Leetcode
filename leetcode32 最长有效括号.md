给定一个只包含 '(' 和 ')' 的字符串，找出最长的包含有效括号的子串的长度。

示例 1:

~~~
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
~~~

示例2

~~~
输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
~~~

题解1

~~~python
"""
简单有效的做法：
从左往右，从右往左分别扫一遍，left和right分别记录左括号和右括号数量：
从右往左扫：
	如果left<right,说明右括号多了，匹配肯定失败。left right 清0
	如果left==right，说明肯定是之前左括号更多，之前没失败过，所以现在是完美匹配。更新res
	反之类似。反过来扫是为了解决"((()"的情况，如果只从右往左扫，res=0。
	时间o(n), 空间o(1)
"""
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        left, right = 0, 0
        res = 0
        for i in s:
            if i == '(':
                left += 1
            elif i == ')':
                right += 1
            if left == right:
                res = max(res, right*2)
            
            if right > left:
                left, right = 0, 0
                
        left, right = 0, 0
        for i in reversed(s):
            if i == '(':
                left += 1
            elif i == ')':
                right += 1
            if left == right:
                res = max(res, right*2)
            
            if left > right:
                left, right = 0, 0
        
        return res
        
            
~~~

题解2

~~~python
"""
	括号匹配惯用做法，用栈。如果是（ 进栈，如果是）出栈，用当前下标减去栈顶value就是当前匹配的长度。
	栈初始化的时候放一个-1，如果上来就是），栈还可以弹，如果发现栈空，就把当前的index放入栈中。
"""
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        stack = [-1]
        res = 0
        
        for i in range(len(s)):
            if s[i]== '(':
                stack.append(i)
            elif s[i] == ')':
                stack.pop()
                if stack:
                    res = max(res, i-stack[-1])
                else:
                    stack.append(i)
        
        return res
~~~

题解3

~~~python
"""
动态规划大法好！
状态表示：dp[i]等于以s[i]结尾的最长有效子字符串长度。
dp[0] 肯定是不匹配的
dp[i]: 如果s[i] == '(' ==> 0 	肯定无效
       如果s[i] == ')' 且 s[i-1] == '(', 他俩直接凑对了。dp[i] = dp[i-2] + 2
       如果s[i] == ')' 且 s[i-1] == ')',那就再往前看看，看看前一个）匹配的（的前一个是不是（，
            如果是的话那就是((.....))。dp[i] = dp[i-1] + 2 + dp[i-1-dp[i-1]-1]
"""
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        dp = [0] * len(s)
        res = 0
        for i in range(1, len(s)):
            if s[i] == ')':
                if s[i-1] == '(':
                    dp[i] = dp[i-2] + 2
                elif s[i-1] == ')' and i-1-dp[i-1] >= 0 and s[i-1-dp[i-1]] == '(':
                    dp[i] = dp[i-1] + 2 + dp[i-2-dp[i-1]]
            
            if dp[i] > res:
                res = dp[i]
        
        return res
~~~

