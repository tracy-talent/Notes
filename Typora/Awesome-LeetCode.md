<h1>Awesome LeetCode</h1>
### LeetCode-10

<font color='red'>problem: </font>[Top100-LeetCode-10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

<font color='green'>tutorial: </font>动态规划。dp\[i\]\[j\]: bool表示从下标i开始字符串s是否与从下标j开始的正则式p匹配，dp\[n\]\[m\]=true

### LeetCode-11

<font color='red'>problem: </font>[Top100-LeetCode-11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

<font color='green'>tutorial:</font> 智商题。proof: We starts with the widest container, l = 0 and r = n - 1. Let's say the left one is shorter: h[l] < h[r]. Then, this is already the largest container the left one can possibly form. There's no need to consider it again. Therefore, we just throw it away and start again with l = 1 and r = n -1.

### LeetCode-22

<font color='red'>problem: </font>[Top100-LeetCode-22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)

<font color='red'>tutorial: </font>Catalan

### LeetCode-23

<font color='red'>problem:</font> [Top100-LeetCode-23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

<font color='green'>tutorial: </font>merge with bottom-up divide and conquer

### LeetCode-31

<font color='red'>problem: </font>[Top100-LeetCode-31. Next Permutation](https://leetcode.com/problems/next-permutation/)

<font color='green'>tutorila: </font>模拟题。题目要求in-place algorithm and constant extra memory，在脑海里模拟寻找次大序列，从右往左遍历找到第一对num[i] > num[i-1]的数，知nums[i,n)递减，从nums[i]往右遍历找到下标最大的大于nums[i-1]的数nums[j]，swap(nums[j], num[i-1])，那么nums[i,n)依然是递减的，reverse nums[i~n)

### LeetCode-33

<font color='red'>problem: </font>[Top100-LeetCode-33. Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/)

<font color='green'>tutorial: </font>

<font color='magenta'>solution1: </font>栈模拟，一开始想到要用栈去解决，但是没有想到具体的栈模拟方法，想得是用栈存储括号符，但正解是存储括符对应下标

<font color='magenta'>solution2: </font>智商压制简直，想到从左往右的方式去计数左右括符各自出现次数，相等时计算一次解，但是这种情况考虑不周全，就没接着往下想了，其实再加一个从右往左的计数就补全漏洞了。这真是交了智商税了

### LeetCode-42

<font color='red'>problem: </font>[Top100-LeetCode-33. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

<font color='green'>tutorial: </font>单调递减栈

### LeetCode-128

<font color='red'>problem: </font>[Top100-LeetCode-128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

<font color='green'>tutorial: </font> 哈希表查询(C++ unordered_map)

### LeetCode-139

<font color='red'>problem:</font> [Top-100-LeetCode-139. Word Break](https://leetcode.com/problems/word-break/)

<font color='green'>tutorial: </font>

<font color='magenta'>solution1: </font>哈希表(unordered_set)查询和动态规划，dp[i]表示s[0..i]是否可用字典中的word拼接出来方法

<font color='magenta'>solution2: </font>哈希表(unoedered_set)查询和队列bfs

### <font color='cyan'>LeetCode-146(cache LRU 模拟)</font>

<font color='red'>problem:</font> [Top-100-LeetCode-146. LRU Cache](https://leetcode.com/problems/lru-cache/)

<font color='green'>tutorial: </font>哈希表(onordered_map<int, ListNode*>)查询+双向链表+内存优化(只使用capacity个ListNode)