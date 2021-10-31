# ACMLog
## 10.31

### 下午
1. Educational Codeforces Round 116 (Rated for Div. 2) C. Banknotes

&ensp;&ensp;补题之前打比赛的时候没做出来的题。大概意思就是，给你n种面额为$10^{0-9}$的钞票，然后对于固定的数量k，求不能用至少k张钞票凑出来的最小的数S。
&ensp;&ensp;先考虑对于一个数S，如何用最小的钞票张数凑出来,简单贪心可以发现并证明有一种策略的取法可以用最少的数量凑出S。然后用这种策略对于一定的k,来填满S，小于S的数值一定可以用小于等于k的钞票凑出。用反证法可以证明这种策略是对的.

2. Codeforces Round #752 (Div. 2) B. XOR Specia-LIS-t 

&ensp;&ensp;水题,这场昨天晚上打得很烂。B也能想偏,后面一直没想回来,可能应该把电脑抱到床上打，室友在耳朵旁边吵得一匹，360度杜比音效环绕,太搞心态了。
&ensp;&ensp;题目大意就是需要把一段序列分成若干部分，使得每个部分的最长严格递增子序列的长度异或和为0。
序列长度偶数的情况,一定可以，就一个数分一个序列就行。

如果为奇数长度，那么需要找到满足$a[i+1] \eaq a[i]$的i，然后把他们分出一段,可以证明,这样种情况是充分必要条件。

### 晚上

下午看了几个小时昨天晚上比赛的C题官方题解，越看越迷,最后问了下小朱，发现自己题目看错了。准备后面再补，先把这周3要做的人工智能pre弄了。找了篇讲神经网络的文章，一晚上看了一半，后面接着看。