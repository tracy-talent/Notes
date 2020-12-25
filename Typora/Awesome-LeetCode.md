<h1>Awesome LeetCode</h1>
### LeetCode-4

<font color='red'>problem: </font>[Top100-LeetCode-4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

<font color='green'>tutorial: </font>设数组A元素m个，数组B元素n个，将两个数组分别划分为左右两部分A\[0\~i-1\]和B\[0\~j-1]，使得两个数组左部分元素数目之和i + j = (n + m + 1) / 2，又因为j = (n + m + 1) / 2 - i > 0，而0 < i < m，所以有(n + m + 1) / 2 > m，因此n + 1 > m即n >= m，这一限制条件要求数组A长度不超过数组B。然后对数组A划分点二分，初始l=0,r=m,满足条件的划分点i=(l+r)/2必满足A\[i-1\]<=B\[j\]，B\[j-1\]<=A\[i\]，若A\[i-1]>B\[j]则更新r=i-1，若B\[j-1\]>A\[i\]则更新l=i+1，总体时间复杂度log(min(m, n))，参考[csdn](https://blog.csdn.net/hit1110310422/article/details/80865539)

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

<font color='green'>tutorial: </font>哈希表(unordered_map<int, ListNode*>)查询+双向链表+内存优化(只使用capacity个ListNode)，也可以使用STL中的list\<pii\>，但是就没有了内存优化

### <font color='cyan'>LeetCode-460(cache LFU 模拟)</font>

<font color='red'>problem: </font>[LeetCode-460. LFU Cache](https://leetcode.com/problems/lfu-cache/)

<font color='green'>tutorial: </font>与LRU相比，LFU多了一个限制条件就是频率，只有频率相同的元素才使用LRU的原则，其实这就相当于让每个频率对应一个LRU使用的数据结构即可实现LFU。使用unordered_map\<int, list\<int\>\> freq2key存储freq到key的映射，unordered_map<int, list\<int\>::iterator> itermap存储key到freq2key中值list的元素迭代器，以便实现O(1)的更新删除操作，unordered_map\<int, pair\<int, int\>\> kvf存储key到(value, freq)的映射。使用一个变量minfreq记录当前cache中所有元素的最小使用频率，以便在cache容量超出限制的时候剔除频率为minfreq的LRU元素。

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

<font color='green'>tutorial: </font>这一题与[LeetCode-121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)很相似，但是更复杂一点，121只允许一次交易，122允许多次交易，需要想明白怎么多次交易才能使得利益最大化就很好模拟出这个过程了。维护买入的最便宜股票的索引minpos，如果前一天股票价格比今天贵则在前一天抛售股票，并更新minpos到今天的索引。解释：假设当前第i天比第i-1天股票便宜，i后面的第j天股价比第i天贵，那么(prices[i-1]-prices[minpos]) + (prices[j] - prices[i]) = prices[j] - prices[minpos] + (prices[i-1]-prices[i]) > prices[j] - prices[minpos]，因此如果第i-1天的股票更贵，则应该在第i-1天抛售并且更新minpos到第i天。

### LeetCode-123

<font color='red'>problem: </font>[Hard-123. Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/submissions/)

<font color='green'>tutorial: </font>这一题与[LeetCode-121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)相似，121只允许交易一次，123允许交易2次，很自然的一个想法是遍历交易日，求左右两边一次交易的最大收益相加即可。分别预处理得到从左到右和从右到左一次交易得到的最大收益，一次交易最大收益求法同121，程序时间复杂度为$O(n)$

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

### LeetCode-47

<font color='red'>problem: </font>[medium-LeetCode-47. Permutations II](https://leetcode.com/problems/permutations-ii/submissions/)

<font color='green'>tutorial: </font>2种方法。

<font color='magenta'>solution1: </font>先排序，对每一个位置从头开始遍历数组，used数组维护元素是否已被使用过，没有使用过的元素可以放到当前位置，然后used标记该元素使用过，迭代执行下一个位置从头开始遍历数组，用一个额外的数组存储遍历过程中的中间排列。

<font color='magenta'>solution2: </font>先排序，从左往右dfs每一个位置idx，然后从左往右每次将idx之后的每一个元素i与idx置换，效果相当于将下标区间[idx, i)之间的元素右挪一个位置，i被置换到idx上，这样idx之后的所有元素依然保持有序，然后进入下一轮dfs(注意nums数组要非引用传入，不让后面的dfs影响当前这一轮dfs的nums数组位置)，知道最后一个位置dfs结束后的nums数组即为一种排列结果。

方法1时间复杂度为$O(n^n)$，方法2时间复杂度为O(n!)，而且方法2的空间复杂度更低，无须额外数组储存排列中间结果，而是直接对输入数组nums进行swap，代码量更小也更高效。

### LeetCode-240

<font color='red'>problem: </font>[medium-LeetCode-240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

<font color='green'>tutorial: </font>矩阵从左到右、从上到下有序，要求查找一个数。一开始想法是从第一行第一列开始二分查找，然后不断缩小矩阵大小，复杂度为$O(nlogn)$.后来发现只要从左下角或者右上角开始查找，每次用顶角的元素进行比较，根据比较的结果将这一顶角对应的行或者列从查找范围中排除，这样每次比较都可以缩小一行或者一列，只需比较m+n-1次即可得到结果，根据adversary argument(对手理论)可证明n*n矩阵使用斜对角线以及次斜对角线上的数与查找目标进行比较是最优的​，至少要比较2\*n-1次，这个算法课上有讲过。

### LeetCode-935

<font color='red'>problem: </font> [medium-LeetCode-935. Knight Dialer](https://leetcode.com/problems/knight-dialer/)

<font color='green'>tutorial: </font>在电话号码盘上只能走"马"，问走N步可以拨出多少种不同的号码。动态规划的思想，基于前一步每个号码的计数来计算下一步每个号码的计数，提前存好从每一个号码可以通过走"马"跨越到的号码。

### LeetCode-93

<font color='red'>problem: </font>[medium-LeetCode-93. Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/)

<font color='green'>tutorial: </font>给出一段数字字符串，输出所有可能的用"."分割的IP地址。先说我的做法是一个一个字符的判断处理，实际更高效更清晰的做法是将字符串分段处理，段的大小为1\~3，然后记录分割段的数目，等于4就不再递归分段而是判断是否已处理完所有的字符。分段的好处在于可以直接判断一个段的合理性，而不像单个字符处理那样还需要从生成的候选IP字符串中从最后一个"."后进行截取。

### LeetCode-95

<font color='red'>problem: </font>[medium-LeetCode-95. Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

<font color='green'>tutorial: </font>求数字1\~n的所有可能二叉搜索树。bst总数就是卡特兰数: $h(n)=\sum_{i=1}^{n}h(i-1)h(n-i)$，因此可由递归构造。

### LeetCode-109

<font color='red'>problem: </font>[medium-LeetCode-109. Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)

<font color='green'>tutorial: </font>将有序链表转换成二叉搜索树。使用快慢指针递归求解，快指针到头时，慢指针所指向位置即为当前序列对应bst的根节点。可以只提供链表头结点的但函数实现，那么需要获取序列对应bst根节点的前一个位置，且对长度为0,1,2的链表序列要单独处理。

### LeetCode-117

<font color='red'>problem: </font>[medium-LeetCode-117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

<font color='green'>tutorial: </font>将每一层二叉树节点从左指向右。一开始我bfs层次遍历实现的，更优雅的解法是递归实现，用父节点root的next节点找下一层的root->right节点后的第一个非空节点。

### LeetCode-440

<font color='red'>problem: </font>[hard-LeetCode-440. K-th Smallest in Lexicographical Order](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/)

<font color='green'>tutorial: </font>计算某个前缀prefix开始的数有多少个，$[prefix, prefix+1), [prefix*10, (prefix+1)*10), [prefix*100, (prefix+1)*100)...$，假设prefix开始的数有cnt个，如果k小于cnt，那么prefix\*\=10，k--，如果k大于等于cnt，那么prefix++，k-=cnt.

### LeetCode-494

<font color='red'>problem: </font>[medium-LeetCode-494. Target Sum](https://leetcode.com/problems/target-sum/)

<font color='green'>tutorial: </font>数组nums，设P表示添加正号的数集合，设N表示添加负号的数集合，那么sum(P)-sum(N)=target，sum(P)+sum(N)+sum(P)-sum(N)=target+sum(nums) 可推出sum(P)=(target+sum(nums))/2，其中target和sum(nums)必须同奇同偶，这样就将问题转换成0-1背包问题

```c++
dp[i][s]:0~i个数正数和为s的计数个数
优化成一维背包
w = (target + sum(nums))/2
dp[0]=1
for (int i = 0; i < n; i++) 
    for (int s = w; s>=nums[i]; s--)
        dp[s] = dp[s] + dp[s - nums[i]];
```

### LeetCode-1375

<font color='red'>problem: </font>[medium-LeetCode-1375. Bulb Switcher III](https://leetcode.com/problems/bulb-switcher-iii/)

<font color='green'>tutorial: </font>这题还挺有意思的，要求以O(1)的空间复杂度解决，遍历打开顺序，维护当前打开的最大灯序号，如果该灯序号等于当前遍历位置+1，那么结果+1

### LeetCode-672

<font color='red'>problem: </font>[medium-LeetCode-672. Bulb Switcher II](https://leetcode.com/problems/bulb-switcher-ii/)

<font color='green'>tutorial: </font>智商题。考虑到前3种操作任取2种等价于剩下的一种，3种操作同时使用等价于无操作，所以最终的操作状态归为\[无操作,1,2,3,4,(1,2),(1,3),(1,4)\]，分情况讨论n<=2和m<=2的情况，当m>=3且n>=3时返回8

### LeetCode-319

<font color='red'>problem: </font>[medium-LeetCode-319. Bulb Switcher](https://leetcode.com/problems/bulb-switcher/)

<font color='green'>tutorial: </font>智商题。只有被操作奇数次的灯才会亮，对于第k个灯，它会被操作k的因子个数的次数，而一个数的因子都是成对出现的，只有完全平方数有一对重合因子，所以最终只有完全平方数编号的灯亮着。返回floor(sqrt(n))

### LeetCode-678

<font color='red'>problem: </font>[medium-LeetCode-678. Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/)

<font color='green'>tutorial: </font>暴搜超时，dfs+记忆化搜索过了，也可以用dp来做，dp\[i]\[j]表示从i到j的字符串是否合理，复杂度O(n^3)，比记忆化搜索耗时长。看题解之后可以O(N)的贪心来做，想不到太精秒了。贪心：假想所有'*'是'('，从左往右遍历保证左括号个数比右括号多，然后把'\*'看做是')'，只要此时左括号个数不比右括号多即合理，否则不合理

### LeetCode-55

<font color='red'>problem: </font>[medium-LeetCode-55. Jump Game](https://leetcode.com/problems/jump-game/)

<font color='green'>tutorial: </font>从右往左贪心，更新可达位置

### LeetCode-45

<font color='red'>problem: </font>[hard-LeetCode-45.Jump Game II](https://leetcode.com/problems/jump-game-ii/)

<font color='green'>tutorial: </font>贪心，把某个位置上能跳的步数看作梯子，步数即为梯长，走完一个梯子才跳，跳的时候选择当前最长梯子作为下一步的梯子。详细解释[YouTube](https://www.youtube.com/watch?v=vBdo7wtwlXs)

### LeetCode-629

<font color='red'>problem: </font>[hard-LeetCode-629.K Inverse Pairs Array](https://leetcode.com/problems/k-inverse-pairs-array/)

<font color='green'>tutorial: </font>动态规划。dp\[i]\[j]表示前i个元素有j个逆序的可能数。$dp[i][j]=\sum_{t=0}^{i-1}{dp[i-1][j-t]}$

### LeetCode-855

<font color='red'>problem: </font>[medium-LeetCode-855.Exam Room](https://leetcode.com/problems/exam-room/)

<font color='green'>tutorial: </font>自定义区间比较的set维护区间使得seat实现O(logN)复杂度，字典unordered_map维护点左右区间边界使得leave实现O(logN)复杂度

### LeetCode-600

<font color='red'>problem: </font>[hard-LeetCode-600.Non-negative Integers without Consecutive Ones](https://leetcode.com/problems/non-negative-integers-without-consecutive-ones/)

<font color='green'>tutorial: </font>斐波拉契数列求n位二进制数不含2个连续1的个数，然后减去大于给定数且满足条件的个数

### LeetCode-974

<font color='red'>problem: </font>[medium-LeetCode-974. Subarray Sums Divisible by K](https://leetcode.com/problems/subarray-sums-divisible-by-k/)

<font color='green'>tutorial: </font>连续子数组和为K的整数倍的个数，考虑2<=K<=10000，可以用数组存储前缀取余和，然后在求总和

### LeetCode-801

<font color='red'>problem: </font>[medium-LeetCode-801. Minimum Swaps To Make Sequences Increasing](https://leetcode.com/problems/minimum-swaps-to-make-sequences-increasing/)

<font color='green'>tutorial: </font>dp.维护n长序列在第n个元素交换和不交换的情况保持有序所需要的最小交换次数n1,s1。

### LeetCode-792

<font color='red'>problem: </font>[medium-792. Number of Matching Subsequences](https://leetcode.com/problems/number-of-matching-subsequences/)

<font color='green'>tutorial: </font>遍历主串S，更新待匹配子序列匹配位置

$$ dp(K, N) = \min_{0 <= i <= N}{\max{dp(K - 1, i - 1), dp(K, N - i)} + 1}$$