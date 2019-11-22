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

<font color='magenta'>solution2: </font>哈希表(unordered_set)查询和队列bfs

### LeetCode-140

<font color='red'>problem: </font>[Top-interview-LeetCode-140.Word Break II](https://leetcode.com/problems/word-break-ii/)

<font color='green'>tutorial: </font>这一题跟139非常相似，要求输出所有可能的构造，使用dp+dfs，match[j]表示s[0...j]是否可以被拼接，dp[i]\[j]表示s.substr(i, j - i + 1)是否可作为拼接词来拼接s。优化：维护wordDict中最长词长度maxlen用于优化

### <font color='cyan'>LeetCode-146(cache LRU 模拟)</font>

<font color='red'>problem:</font> [Top-100-LeetCode-146. LRU Cache](https://leetcode.com/problems/lru-cache/)

<font color='green'>tutorial: </font>哈希表(onordered_map<int, ListNode*>)查询+双向链表+内存优化(只使用capacity个ListNode)

### LeetCode-236

<font color='red'>problem: </font>[Top-100-236. LeetCode-Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

<font color='green'>tutorial: </font>LCA求解，使用dfs或者使用stack+map迭代记忆两个节点的所有父节点，找到公共的两个节点即为LCA。

### <font color='CYAN'>LeetCode-301</font>

<font color='red'>problem: </font>[Top-100-301. LeetCode-Remove Invalid Parentheses](https://leetcode.com/problems/remove-invalid-parentheses/)

<font color='green'>tutorial: </font>dfs递归 + 栈计数

### LeetCode-49

<font color='red'>problem: </font>[Top-100-49. LeetCode-Group Anagrams](https://leetcode.com/problems/group-anagrams/)

<font color='green'>tutorial: </font>anagrams是指颠倒字母构成的词(含有相同的字母但是顺序可能不同)，有三种解法：1、哈希。每个字母対应一个质数，字符串的哈希值是是其字符对应质数相乘取模1e+7，这种方法可能会存在哈希冲突，但是对于给出的数据集一般都能过。2、对字符串排序后查找哈希表得到索引，插入到对应索引的列表中。3、计数后将计数数组构成"#".join(cnt)字符串然后在查找哈希表得到索引，插入到对应索引的列表中。

### LeetCode-416

<font color='red'>problem: </font>[Top-100-416. LeetCode-Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

<font color='green'>tutorial: </font>dfs寻找可行确定和，降序优化：将数组降序排序，先取最大的数到sum中(最大的数必在某一可行解中)然后再搜索

### LeetCode-437

<font color='red'>problem: </font>[Top-100-437. LeetCode-Path Sum III](https://leetcode.com/problems/path-sum-iii/)

<font color='green'>tutorial: </font>dfs搜索，unordered_set存储前缀和

### LeetCode-438

<font color='red'>problem: </font>[Top-100-438. LeetCode-Find All Anagrams in a String](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

<font color='green'>tutorial: </font>

<font color='magenta'>solution1: </font>哈希

<font color='magenta'>solution2: </font>计数使用尺取法匹配验证

两种方案的时间复杂度都是O(n)，但是solution2鲁棒性更好，solution1如果哈希空间可能会冲突

### LeetCode-621

<font color='red'>problem: </font>[Top-100-621. LeetCode-Task Scheduler](https://leetcode.com/problems/task-scheduler/)

<font color='green'>tutorial: </font>智商题(又交了智商税)，以构造法模拟的方式来讲解这道题的做法：把最频繁的chars(最频繁的字符可能有多个)都找出来，假设出现频次为f，然后划分出f个chunk，chunk的初始容量为n+1，每个chunk的开头是频繁chars的任意序的字符串(假设最频繁chars是A、E，那么组成任意序字符串可以是AE)，然后后续非最频繁的剩余chars，顺序循环依次append到每个chunk后面，伪代码例:

```python
f = 最频繁char频次
pos = 0 # 当前所在chunk
notfreqchars = {'E':23, 'Q':18, 'Z': 13}
for key, value in notfeqchars.items():
    for i in range(value):
   		chunk[pos % (f - 1)].append(key) # 取余(f - 1)，后面字符频次都小于f，足以填充
```

填充结果有两种情况：

1. 有chunk未被填充满
2. 所有chunk被填充满，并且还有剩余字符未填充进去

对于情况一很好理解，结果为(f - 1) \* (n  + 1) + len(最频繁chars)，关键是想明白情况二，一开始自己建模方式不对，不能理解后续未填充字符该如何处理，现在中间的f-1个chunk都被填充满了，同一字符之间区间距离不小于n，这时候无论后续剩余字符填充在什么位置都不会减少原来字符之间的区间距离，所以只要保证后续插入字符之间区间距离不小于n即可，这时候每个chunk末尾位置之间的距离恰为n，且剩余字符的频次都小于f，所以可以直接把剩余字符(相同字符)顺序循环依次append到chunk末尾(不包括最后一个chunk)来保证插入的同样字符之间不会有冲突，最终填充完之后的区间大小即为输入字符集的大小。

### LeetCode-29

<font color='red'>problem: </font>[Top-Interview-LeetCode-29. Divide Two Integers](https://leetcode.com/problems/divide-two-integers/)

<font color='green'>tutorial: </font>循环divisor <<= 1与dividend对比，直到(divisor << d) > dividend，ans += 1 << (d - 1)，然后dividend- divisor << (d - 1)重复上面的操作。

### LeetCode-44

<font color='red'>problem: </font>[Top-interview-LeetCode-44. Wildcard Matching](https://leetcode.com/problems/wildcard-matching/)

<font color='green'>tutorial: </font>这一题与[Top100-LeetCode-10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)几乎一样，可以使用一样的二维dp方法来做，但也可以使用一维dp来做。n为字符串长度，m为模式串长度

<font color='magenta'>solution1:</font>二维dp。dp\[i\]\[j\]: bool表示从下标i开始字符串s是否与从下标j开始的正则式p匹配，dp\[n\]\[m\]=true，返回dp\[0\]\[0]

<font color='magenta'>solution2:</font>一维dp。dp[j]: bool表示模式串p[0\~i]可以匹配s[0\~j]，选择适当的遍历方式即可使用一维dp实现想法，从左到右依次遍历模式串p，然后从左到右遍历s判断s当前位置的前缀是否可以匹配模式串p当前位置的前缀，dp[0]=true，返回dp[n]

### LeetCode-54

<font color='red'>problem: </font>[Top-interview-LeetCode-54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

<font color='green'>tutorial: </font>模拟题，注意边界细节

### LeetCode-73

<font color='red'>problem: </font>[Top-interview-LeetCode-73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)

<font color='green'>tutorial: </font>题目的难点在于要求使用常数级别的空间复杂度实现，想到了方法也可能败在细节处(我羞耻地直接看了答案。。。逃~)。可以将出现0的行向左映射到第一列，在第一列对应行位置置1，将出现0的列向上映射到第一行，在第一行对应位置置1。但是matrix[0\][0]这个位置元素既属于第一行也属于第一列，这是个要特别注意的冲突细节，在处理时可以不将第一列向上映射到第一行，第一列的元素是否出现过0使用额外的标志变量进行标记。最后matrix[i\][j\](除了第一列元素)是否置0根据matrix[i\][0]和matrix[0\][j]是否为0来决定，第一列元素根据标志变量来决定是否置0，还有一个细节就是matrix的置0判断操作一定要从下往上一行一行处理，因为第一行含列标记位，不能在下面行未处理之前覆盖掉。

### LeetCode-127

<font color='red'>problem: </font>[Top-interview-LeetCode-127. Word Ladder](https://leetcode.com/problems/word-ladder/)

<font color='green'>tutorial: </font>这一题给人的直觉就是bfs一层一层的搜索，知道找到目标词汇。但是令人惊诧的是还有很多优化的技巧可用到。

<font color='magenta'>solution1: </font>单向bfs，可以使用list维护词列表(每个待扩展词遍历词列表寻找相差一个字符的扩展词)，也可以使用unordered_set维护词列表(对于每个待扩展词，构造所有只与其相差一个字符的扩展词，然后查询是否在词列表中存在)。假设词列表大小为n，使用list的时间复杂度O(n^2)，使用unordered_set的时间复杂度为O(n*len(单个词长度)\*26)，如果词列表不长使用list更高效，而如果词列表很大则使用unordered_set效率更高。

<font color='magenta'>solution2: </font>双向bfs，先判断终结词是否在词列表中，如果在则从起始词和终结词同时向中间bfs(扩展出来的词都用unordered_set维护)，每次选择含有较少待扩展词的一边进行bfs扩展，这样就可以避免单向bfs在深层次遍历大量待扩展词。

### LeetCode-122

<font color='red'>problem: </font>[Top-interview-LeetCode-122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

<font color='green'>tutorial: </font>这一题与[LeetCode-121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)很相似，但是更复杂一点，121只允许一次交易，122允许多次交易，需要想明白怎么多次交易才能使得利益最大化就很好模拟出这个过程了。维护minpos和maxpos(初始位置为0)，如果后面的股票比前面的股票便宜则更新maxpos=minpos=该股票位置，如果后面股票比maxpos位置股票贵，则更新maxpos到当前位置，并继续探索后一天股价是否有比当前maxpos股价更贵，如果更贵则将maspos继续后移，否则将maxpos和minpos两个位置的股价差累加到收益中，并更新minpos=maxpos=maxpos+1。

### LeetCode-212

<font color='red'>problem: </font>[Top-interview-LeetCode-212. Word Search II](https://leetcode.com/problems/word-search-ii/)

<font color='green'>tutorial: </font>trie树搜索，将字符串字典中所有字符串建立成trie树，然后遍历字符矩阵从trie树的root节点开始dfs搜索，如果当前trie节点isword标记为true则将对应字符串添加到结果中，并将该节点的isword标记为false。空间优化：搜索过程中字符矩阵中访问过的字符不要开辟额外空间去标记了，直接在原字符矩阵基础上修改为'\0'，dfs回溯到当前节点后再将原字符还原回去。

### <font color='cyan'>LeetCode-218</font>

<font color='red'>problem: </font>[Top-interview-LeetCode-218. The Skyline Problem](https://leetcode.com/problems/the-skyline-problem/)

<font color='green'>tutorial: </font>对输入的单个数据[l,r,h]分割处理为[l,-h]和[r,h]存储到列表中，按照x坐标从小到大，高度h从小到大排列，这里将左边界坐标高度存为负数有两点作用：1. 辨别是左边界节点还是右边界节点，左边界节点则插入高度到维护最大值的容器中，右边界节点则从维护最大高度的容器中删除该高度。至于什么时候存入结果，迭代前面排好序的列表，如果当前维护最大值容器中的最大高度值与前一次存入到返回结果中的坐标高度不相同则组合当前这一次迭代元素的x坐标和最大高度存入返回到结果中，否则迭代列表下一个值。其中维护最大值的容器可以使用priority_queue(配合unordered_map计数需要被删除的高度，如果当前队顶值在unordered_map中计数不为0则弹出)，也可以使用multiset(删除元素的时候不要直接删除值即erase(h)，这样会删除所有等值h的数，但实际上只需要删除一个h，所有应该删除对应h的一个迭代器即erase(multiset.find(h)))

### LeetCode-227

<font color='red'>problem: </font>[Top-interview-LeetCode-227. Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/)

<font color='green'>tutorial: </font>题目中的中缀表达式只包含空格和不带正负号的正整数，由于没有括号和正负号的干扰，可以只是用一个数字栈而不用运算符栈即可实现中缀表达式计算。具体过程：记录前一个运算符，遍历到一个元素符或者最后一个字符时，判断前一个运算符，如果为\*或者/则弹出数字栈中一个数与当前转化过来的一个数进行计算并将结果压入栈中，如果为+则直接转化过来的数入栈，如果为-则取负再入栈。遍历完表达式，最终直接将数字栈中的所有数相加即为结果。

### LeetCode-237

<font color='red'>problem: </font>[Top-interview-LeetCode-237. Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/)

<font color='green'>tutorial: </font>这题看似只是一个简单的链表节点删除操作，实际上却非常考察我们对指针的理解，指针取\*时的意义。只给出你一个节点，要如何删除这个节点使链表前后相通呢？将后一个节点的内容复制到当前节点即可。两种做法：

```
*node = *node->next;  //方法1.
ListNode* next = node->next;  *node = *next; delete next;  //方法2. 回收了内存
```

### LeetCode-315

<font color='red'>problem: </font>[Top-interview-LeetCode-315. Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)

<font color='green'>tutorial: </font>树状数组。可以按照数组长度建立树状数组(我采用此方法)，也可以采用数组中最大最小值范围建立树状索引，前者需要按值从小到大排序，然后在n-数的原索引位置处更新树状数组，后者无须排序，直接从在后往前遍历的值减去最小值的位置处更新树状数组。如果最小值最大值相差不大则使用后者效率更高，否则前者更佳。

### <font color='CYAN'>LeetCode-324</font>

<font color='red'>problem: </font>[Top-interview-LeetCode-324. Wiggle Sort II](https://leetcode.com/problems/wiggle-sort-ii/)

<font color='green'>tutorial: </font>这一题难度要求O(n)时间复杂度O(1)空间复杂度实现难度很大，想到细节繁多的索引就头疼，看了讨论里一位大神的题解都理解很费劲。首先重定义索引`#define idx(i) (1 + 2*i)%(n|1)`，此处索引的定义太关键了，极简了程序中繁杂的索引处理，平时没用过这种索引方式的话根本想不到，该索引重写会先索引完所有奇数位置的数，然后重头遍历索引所有偶数位置的数。借用该索引方式，将较midv小的数放靠后面偶数索引位置，较midv大的数放靠前面奇数索引位置，等于midv所有值集中放在较中间的位置。核心代码

```c++
auto midptr = nums.begin() + n / 2;
nth_element(nums.begin(), midptr, nums.end()); // 分块算法找nth复杂度O(n)
int midv = *midptr;
int i = 0, j = 0, k = n - 1;
// 把较midv小的数放最后，较midv大的数放最后，等于midv的放中间
while (j <= k) {
    if (nums[idx(j)] > midv) swap(nums[idx(i++)], nums[idx(j++)]);  // 把更大的数放到靠前的奇数索引位置，与等于midv的索引位置的第一个置换
    else if (nums[idx(j)] < midv) swap(nums[idx(j)], nums[idx(k--)]); //  把更小的数放到靠后的偶数索引位置
    else j++; // idx([i,j))存储midv相等的值
}
```

### LeetCode-329

<font color='red'>problem: </font>[Top-interview-LeetCode-329. Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)

<font color='green'>tutorial: </font>dfs记忆化搜索

### LeetCode-30

<font color='red'>problem: </font>[hard-LeetCode-30. Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)

<font color='green'>tutorial: </font>哈希查找。使用hash\<string\>()(word)求出words列表中每个word的哈希值进行累加得到目标哈希值，然后再遍历字符串s，以前len(word)个下标为起始点，步长len(word)进行哈希值叠加与匹配。

### LeetCode-378

<font color='red'>problem: </font>[Top-interview-LeetCode-378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)

<font color='green'>tutorial: </font>二分查找。取matrix的左上角最小值和右下角最大值为其实上下界进行二分查找。从右往左遍历每行得到每行小于等于mid的值并累加，与k对比小于k则lv = mid + 1，否则rv = mid。

### LeetCode-371

<font color='red'>problem: </font>[Top-interview-LeetCode-371. Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/)

<font color='green'>tutorial: </font>不用到'+'或者'-'求两个数的和，猜到要用位操作但就是难想。

```c++
int getSum(int a, int b) {
    return b == 0 ? a : getSum(a ^ b, (1u * (a & b)) << 1);
}
```

### LeetCode-380

<font color='red'>problem: </font>[Top-interview-LeetCode-380. Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1/)

<font color='green'>tutorial: </font>插入、删除用哈希表即可实现O(1)，关键在于以O(1)复杂度随机获取值。只使用哈希表还不行，O(1)随机获取值必须基于一个连续的数组。那么删除数组中间的值使得数组不连续怎么解决？可以将数组最后一个值置换到删除位置(这并不影响随机获取值)，并更新数组最后这个值的哈希索引为删除位置，接着从哈希表中和数组中删除值。

### LeetCode-395

<font color='red'>problem: </font>[Top-interview-LeetCode-395. Longest Substring with At Least K Repeating Characters](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/)

<font color='green'>tutorial: </font>这一题写的时候找到了bug问题所在，但是没想到要缩小区间去重新计数(总想着只遍历一次。。。)。有两种解决方案：方案1，暴力，二次遍历区间(i, j)，使用26位的位计算(<k置1，>=k置0)，如果位存储单元mask等于0则意味着当前区间(i,j)满足，更新ans，则下一次遍历起始位置必大于j，不必再重新计算(i,j)，最坏时间复杂度O(n^2)。方案2，使用递归区间的方式，找到满足计数>=k的连续区间(i,j)并递归(i,j)，重新计数(i,j)区间内的字符，如果i~j的每一字符的新计数都>=k则直接返回j-i+1作为结果，否则缩小区间继续递归。