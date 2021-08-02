[TOC]



# Nowcoder 多校联合第四场

## C.LCS

**题解：**

题意为，我们给出三个等长字符串$s_1$,$s_2$,$s_3$，定义$a = LCS(s_1,s_2)$，$b = LCS(s_2,s_3)$，$c = LCS(s_1,s_3)$。要求构造出满足条件的三个字符串，如果不存在输出$NO$。

先构造公共前缀，取$a$,$b$,$c$中最小的，记为$min$作为三个字符串公共前缀，为了便于分析我们把公共前缀写为：$aaa....a$

此后我们令$a - min;b - min;c- min$，这样得到的三个数中必定至少有一个是$0$，剩余的数我们可以认为是从他对应的字符串身上继承下来的。比如$a = 0$，那就相当于是$s_1 = a ... a$，$s_2 = a .. a b...b$除了前缀外都不一样，$s_3$的后缀来源于两方面：一方面是根据$b$的值，从$s_2$中后的非公共部分拿出$b$个，另一方面是根据$c$的值，从$s_3$后的非公共部分拿出$c$个，最后补充到要求长度即可。

**AC代码：**

```cpp
#include <bits/stdc++.h>

#define ill __int128
#define ll long long
#define PII pair <ll,ll>
#define ull unsigned long long
#define me(a,b) memset (a,b,sizeof(a))
#define rep(i,a,b) for (int i = a;i <= b;i ++)
#define req(i,a,b) for (int i = a;i >= b;i --)
#define ios std :: ios :: sync_with_stdio(false)

const double Exp = 1e-9;
const int INF = 0x3f3f3f3f;
const int inf = -0x3f3f3f3f;
const ll mode = 1000000007;
const double pi = 3.141592653589793;

using namespace std;
string A,B,C;
int a,b,c,n;

int main()
{
    ios;
    cin >> a >> b >> c >> n;
    int minn = min(min(a,b),c);
    a -= minn;b -= minn;c -= minn;
    char t = 'a';
    for (int i = 1;i <= minn;i ++) {
        A += t;
        B += t;
        C += t;
    }
    if (a == 0) {
        if (minn + b + c > n) {
            cout << "NO" << endl;
            return 0;
        }
        for (int i = 1;i <= n - minn;i ++) A += (t);
        for (int i = 1;i <= n - minn;i ++) B += (t + 1);
        for (int i = 1;i <= b;i ++) C += (t + 1);
        for (int i = 1;i <= c;i ++) C += t;
        for (int i = 1;i <= n - minn - b - c;i ++) C += (t + 2);
        cout << A << endl << B << endl << C << endl;
    }
    else if (b == 0) {
        if (minn + a + c > n) {
            cout << "NO" << endl;
            return 0;
        }
        for (int i = 1;i <= n - minn;i ++) C += (t);
        for (int i = 1;i <= n - minn;i ++) B += (t + 1);
        for (int i = 1;i <= a;i ++) A += (t + 1);
        for (int i = 1;i <= c;i ++) A += t;
        for (int i = 1;i <= n - minn - a - c;i ++) A += (t + 2);
        cout << A << endl << B << endl << C << endl;
    }
    else {
        if (minn + a + b > n) {
            cout << "NO" << endl;
            return 0;
        }
        for (int i = 1;i <= n - minn;i ++) C += (t);
        for (int i = 1;i <= n - minn;i ++) A += (t + 1);
        for (int i = 1;i <= a;i ++) B += (t + 1);
        for (int i = 1;i <= b;i ++) B += t;
        for (int i = 1;i <= n - minn - a - b;i ++) B += (t + 2);
        cout << A << endl << B << endl << C << endl;
    }
    return 0;
}
```

## F.Just a Joke

**题解：**

每一次有两种选择的删除方法，第一种是我们直接删除一整个连通分量（**不能含有环**），第二种是只能删一条边，但是注意，**删除这个边后还是有点存在的！**这个点也是需要单独删除的。我们其实可以直接统计点和边的个数，不用考虑连边的问题，因为不管执行哪一种操作，最后得到的一定是边点和为奇数时`Alice`胜，否则`Bob`胜。

**AC代码：**

```cpp
#include <bits/stdc++.h>
 
#define ill __int128
#define ll long long
#define PII pair <ll,ll>
#define ull unsigned long long
#define me(a,b) memset (a,b,sizeof(a))
#define rep(i,a,b) for (int i = a;i <= b;i ++)
#define req(i,a,b) for (int i = a;i >= b;i --)
#define ios std :: ios :: sync_with_stdio(false)
 
const double Exp = 1e-9;
const int INF = 0x3f3f3f3f;
const int inf = -0x3f3f3f3f;
const ll mode = 1000000007;
const double pi = 3.141592653589793;
 
using namespace std;

int main()
{
    int n,m;
    cin >> n >> m;
    int x,y;
    for(int i = 0;i < m;i++) cin >> x >> y;
    if ((n + m) & 1) puts("Alice");
    else puts("Bob");
    return 0;
}
```

## I.Inverse Pair

**题解：**

其实很水的一个题，算出逆序对，然后因为本身序列是一个排列，所以我们可以扫描序列，假设当前的值为$P$，则我们只需要判断$P -1$是否在$P$的前面就可以了。如果在前面就直接加一，逆序对就少了一对。

**AC代码：**

```cpp
#include <bits/stdc++.h>
 
#define ill __int128
#define ll long long
#define PII pair <ll,ll>
#define ull unsigned long long
#define me(a,b) memset (a,b,sizeof(a))
#define rep(i,a,b) for (int i = a;i <= b;i ++)
#define req(i,a,b) for (int i = a;i >= b;i --)
#define ios std :: ios :: sync_with_stdio(false)
 
const double Exp = 1e-9;
const int INF = 0x3f3f3f3f;
const int inf = -0x3f3f3f3f;
const ll mode = 1000000007;
const double pi = 3.141592653589793;
 
using namespace std;
 
const int maxn = 2e5 + 10;
int s1[maxn] = {},n,s2[maxn] = {},flag[maxn] = {},a[maxn] = {};
ll cnt = 0;
map<int,int > mp;
 
void merge(int L, int R, int Mid)
{
    int i = L;int j = Mid + 1;int k = L;
    while(i <= Mid && j <= R){
        if(s1[i] <= s1[j])s2[k ++] = s1[i ++];
        else{
            cnt += Mid - i + 1;
            s2[k ++] = s1[j ++];
        }
    }
    while(i <= Mid) s2[k ++] = s1[i ++];
    while(j <= R) s2[k ++] = s1[j ++];
    for(i = L; i <= R; i ++) s1[i] = s2[i];
}
 
void mergesort(int L, int R)
{
    if(L < R){
        int Mid = (L + R) / 2;
        mergesort(L, Mid),mergesort(Mid + 1, R);
        merge(L, R, Mid);
    }
}
 
int main()
{
    scanf ("%d", &n);
    for (int i = 1; i <= n; i ++) {
        scanf ("%d",&s1[i]);
        a[i] = s1[i];
        mp[a[i]] = i;
    }
    mergesort (1,n);
    for (int i = 1;i <= n;i ++) {
        int now = mp[a[i]];
        if (flag[mp[a[i]]] == 1) continue;
        if (a[i] == 1) continue;
        else {
            int last = mp[a[i] - 1];
            if (last > now) {
                cnt --;
                flag[mp[a[i] - 1]] = 1;
            }
        }
    }
    cout << cnt << endl;
    return 0;
}
```

## J.Average

**题解：**

二分+尺取

核心思想就是把一个二维数组的求和优化到两个一维数组上，这样我们就把问题转换成了，对于两个一维数组，分别求出他们的子数组最大平均值即可，这就用到了尺取和二分的思想。

**AC代码：**

```cpp
#include <bits/stdc++.h>
using namespace std;
const int MAXN = 1e5;
int arr[MAXN + 5];
double sum[MAXN + 5];
int arr2[MAXN + 5];
double sum2[MAXN + 5];
int n, m;
int x,y;
bool check(double avg)
{
    for(int i = 1; i <= n; ++i) sum[i] = sum[i - 1] + arr[i] - avg;
    double minv = 0;
    for(int i = x; i <= n; ++i) {
        minv = min(minv, sum[i - x]);
        if(sum[i] >= minv) return true;
    }
    return false;
}
bool check2(double avg)
{
    for(int i = 1; i <= m; ++i) sum[i] = sum[i - 1] + arr2[i] - avg;
    double minv = 0;
    for(int i = y; i <= m; ++i) {
        minv = min(minv, sum[i - y]);
        if(sum[i] >= minv) return true;
    }
    return false;
}
int main()
{
    
    scanf("%d%d%d%d", &n,&m,&x,&y);  // cin  cout
    double l = 0, r = 0;
    for(int i = 1; i <= n; ++i) {
        scanf("%d", arr + i);
        r = max(r, double(arr[i]));
    }
    double r2 = 0;
    double l2 = 0 ;
    for(int i = 1; i <= m; ++i) {
        scanf("%d", arr2 + i);
        r2 = max(r2, double(arr2[i]));
    }
    while(r - l > 1e-7) {//二分法
        double mid = (l + r) / 2;
        if(check(mid)) l = mid;
        else r = mid;
    }
    while(r2 - l2 > 1e-7) {//二分法
        double mid = (l2 + r2) / 2;
        if(check2(mid)) l2 = mid;
        else r2 = mid;
    }

    printf("%.7lf\n",r2+r);
    return 0;
}
```

# Nowcoder 多校联合第五场

## H.Holding Two

**题解：**

具体要求就是：同一行、一列、一对角线上的元素不能有三个相同的。要求构造这样的$n \times m$的矩阵。

我们发现：$1001$和$0110$恰好是一对符合要求的串，那就按照他们为模板串根据长度构造即可。

**AC代码：**

```cpp
#include <bits/stdc++.h>

#define ill __int128
#define ll long long
#define PII pair <ll,ll>
#define ull unsigned long long
#define me(a,b) memset (a,b,sizeof(a))
#define rep(i,a,b) for (int i = a;i <= b;i ++)
#define req(i,a,b) for (int i = a;i >= b;i --)
#define ios std :: ios :: sync_with_stdio(false)

const double Exp = 1e-9;
const int INF = 0x3f3f3f3f;
const int inf = -0x3f3f3f3f;
const ll mode = 1000000007;
const double pi = 3.141592653589793;

using namespace std;

string a = "1001", b = "0110";

int main()
{
    int n, m;
    cin >> n >> m;
    for (int i = 0;i < n;i ++) {
        if (i % 2 == 0) {
            for (int j = 0;j < m;j ++) {
                cout << a[j % 4];
            }
            cout << endl;
        }
        else {
            for (int j = 0;j < m;j ++) {
                cout << b[j % 4];
            }
            cout << endl;
        }
    }
    return 0;
}
```

## K.King of Range

**题解：**

这个题要做的就是维护一个区间最值的问题，问题的规模和要求可以绕过线段树直接$ST$表，但是这里使用了单调队列的做法，速度更快而且代码更简洁。

首先构造两个队列$Q_1$​​和$Q_2$​​，分别保存区间最大值和区间最小值，每一次查询我们只需要看两个队的队头即可，之后我们开始枚举区间，这里如果暴力扫描的话，复杂度会达到$O(n^2)$​​，所以肯定是不可取的。于是这里我们考虑用尺取法优化：先限定左端点在$l = 1$​​的位置，我们从$1$​​到$n$​​遍历一遍数组，每次遍历更新$Q_1$​​和$Q_2$​，同时比较队头元素差是否满足$Q_1 - Q_2 > k$​，如果符合，那从当前区间就是满足题意的最短​区间，大于右端点的位置肯定也符合条件，所以我们可以每次更新答案$ans += (n - i + 1)$​，然后尝试着缩小左端点，如果左端点是$Q_1$​或$Q_2$​的队头元素，那么就让对应的队头出队（**这里保证了每一次我们得到的队头元素都是对应区间上的！**），扫描完即可。

**AC代码：**

```cpp
#include <bits/stdc++.h>

#define ill __int128
#define ll long long
#define PII pair <ll,ll>
#define ull unsigned long long
#define me(a,b) memset (a,b,sizeof(a))
#define rep(i,a,b) for (int i = a;i <= b;i ++)
#define req(i,a,b) for (int i = a;i >= b;i --)
#define ios std :: ios :: sync_with_stdio(false)

const double Exp = 1e-9;
const int INF = 0x3f3f3f3f;
const int inf = -0x3f3f3f3f;
const ll mode = 1000000007;
const double pi = 3.141592653589793;

using namespace std;

const int maxn = 1e5 + 10;
ll a[maxn] = {}, k;
ll Q1[maxn], Q2[maxn];
int head1, head2, point1, point2, l;
int n ,m;

void init()
{
    me(Q1, 0);me(Q2, 0);
    head1 = head2 = 0;
    point1 = point2 = -1;
    l = 1;
}

void solve()
{
    ll ans = 0;
    scanf ("%lld", &k);
    for (int i = 1;i <= n;i ++) {
        while (head1 <= point1 && a[Q1[point1]] <= a[i]) point1 --;
        Q1[++ point1] = i;
        while (head2 <= point2 && a[Q2[point2]] >= a[i]) point2 --;
        Q2[++ point2] = i;
        while (l <= i && a[Q1[head1]] - a[Q2[head2]] > k) {
            ans += (n - i + 1);
            l ++;
            if (l > Q1[head1]) head1 ++;
            if (l > Q2[head2]) head2 ++;
        }
    }
    printf ("%lld\n", ans);
    return ;
}

int main()
{
    scanf ("%d%d", &n, &m);
    for (int i = 1;i <= n;i ++) scanf ("%lld", &a[i]);
    while ( m -- ) {
        init();
        solve();
    }
    return 0;
}
```

## B.Boxes

**题解：**

数学 + 思维

这个问题的策略无非两种：一种是我们不用提醒开全部箱子，这样的花费就是$\sum^{n}_{i = 1}w_i$​​​，第二种就是我们使用提醒的最小花费，这里要用一点贪心的思想：**一开始就使用提醒的花费一定比中间某一次使用提醒的花费小**，所以我们第一次使用提醒，花费$C$​​，然后我们假设我们开到第$i$​个箱子的时候我们就不用再开了，换言之，当开到第$i$​个箱子后，后$n - i$​个箱子内小球的颜色一定是确定的（**同为黑或者同为白**），所以我们可以倒推一下：从后往前开的情况，后面$n - i$个球的颜色都是相同的，所以概率就是$\frac{1}{2^{n - i}}$，花费的期望就是开的箱子的花费乘概率，为了花费最小我们需要对$w$数组升序排序。

所以策略就是：两种开法做比较取最小即可，即：$ans = min(\sum^n_{i = 1}w_i,\sum^n_{i = 1}\frac{1}{2 ^ {n - i}}\sum^i_{j = 1}w_j)$

**AC代码：**

```cpp
#include <bits/stdc++.h>

#define ill __int128
#define ll long long
#define PII pair <ll,ll>
#define ull unsigned long long
#define me(a,b) memset (a,b,sizeof(a))
#define rep(i,a,b) for (int i = a;i <= b;i ++)
#define req(i,a,b) for (int i = a;i >= b;i --)
#define ios std :: ios :: sync_with_stdio(false)

const double Exp = 1e-6;
const int INF = 0x3f3f3f3f;
const int inf = -0x3f3f3f3f;
const ll mode = 1000000007;
const double pi = 3.141592653589793;

using namespace std;

const int maxn = 1e5 + 10;
int n;
double C, w[maxn], sum[maxn], cnt[maxn];

int main()
{
    scanf ("%d%lf",&n, &C);
    sum[0] = 0;
    for (int i = 1;i <= n;i ++) scanf ("%lf", &w[i]);
    sort(w + 1, w + 1 + n);
    for (int i = 1;i <= n;i ++) sum[i] = sum[i - 1] + w[i]; 
    double ans1 = sum[n];
    double ans2 = C;
    for (int i = 1;i < n;i ++) ans2 += (pow(0.5, n - i) * sum[i]);
    printf ("%.6lf\n", min(ans2, ans1));
    return 0;
}
```

## D.Double Strings

**题解：**

2019秦皇岛站$C$的翻版。

$dp$ + 组合数 + $Lucas$定理

比较综合的一道题目，首先看一下要求：

- 选出的子序列长度一致
- 前$[1,i - 1]$为公共子序列
- $A[i] < B[i]$
- 后面的随意

这个题的数据也比较小，我们先求解一下$dp[i][j]$，他的意义是：当$A$串扫描到$A_i$，$B$串扫描到$B_j$时，他们的公共前缀数目，如果此时$A[i] = B[j]$，那就有$dp[i][j] += dp[i - 1][j - 1] + 1$，这里的$1$表示的是前面没有前缀，是空字符串。然后我们对每一对$i,j$，如果此时$A[i] < B[j]$，我们从$A$和$B$中剩下的字符里面选相同数量个字符组成合法字串。这里的选取方法数有：$\sum^{min(lenA - i,lenB - j)}_{i = 0}C^{i}_{lenA}C^i_{lenB} = C^{min(lenA - i,lenB - j)}_{len_A - i + lenB - j}$。这里的式子是一个组合数的性质，具体推导参见蓝书。所以最后的答案就是$ans = (dp[i - 1][j - 1] + 1) * C^{min(lenA - i,lenB - j)}_{len_A - i + lenB - j}$。

但是还没完！

$lenA - i + lenB - j$的最大值可以达到$10000$的大小，$min(lenA- i,lenB-j)$也有$5000$的规模，对组合数预处理的时候，根本无法开到$10000 \times 5000$的大小的数组！所以我们只能另寻方案：我们打出$9500 \times 5000$的表，预处理组合数，剩下的使用$Lucas$定理暴力求解。$Lucas$定理参考[OI.wiki_Lucas]([卢卡斯定理 - OI Wiki (oi-wiki.org)](https://oi-wiki.org/math/lucas/))

```cpp
#include <bits/stdc++.h>

#define ill __int128
#define ll long long
#define PII pair <ll,ll>
#define ull unsigned long long
#define me(a,b) memset (a,b,sizeof(a))
#define rep(i,a,b) for (int i = a;i <= b;i ++)
#define req(i,a,b) for (int i = a;i >= b;i --)
#define ios std :: ios :: sync_with_stdio(false)

const double Exp = 1e-9;
const int INF = 0x3f3f3f3f;
const int inf = -0x3f3f3f3f;
const ll mode = 1000000007;
const double pi = 3.141592653589793;

using namespace std;

const int maxn = 5e3 + 10;

char A[maxn], B[maxn];
int dp[maxn][maxn] = {};
int c[9505][5005] = {};

void init()
{
    c[0][0] = 1;
    for (int i = 1;i <= 9500;i ++) {
        c[i][0] = 1;
        for (int j = 1;j <= min(i, 5000);j ++) c[i][j] = (c[i - 1][j] + c[i - 1][j - 1] + mode) % mode;
    }
    return ;
}

ll qpow(ll a, ll b)
{
    ll ans = 1;
    a = a % mode;
    while (b) {
        if (b & 1) ans = ans * a % mode;
        a = a * a % mode;
        b >>= 1;
    }
    return ans % mode;
}

ll C(ll n, ll m)
{
    if (m > n) return 0;
    ll a = 1, b = 1;
    for (int i = 1;i <= m;i ++) {
        a = a * (n + i - m) % mode;
        b = b * i % mode;
    }   
    return a * qpow(b, mode - 2) % mode;
}

ll Lucas(ll n, ll m)
{
    if (m == 0) return 1ll;
    return C(n % mode, m % mode) * Lucas(n / mode, m / mode) % mode;
}

int main()
{
    init();
    scanf ("%s%s",A + 1, B + 1);
    int len_A = strlen(A + 1), len_B = strlen(B + 1);
    for (int i = 1;i <= len_A;i ++) {
        for (int j = 1;j <= len_B;j ++) {
            dp[i][j] = (dp[i - 1][j] + dp[i][j - 1] - dp[i - 1][j - 1] + mode) % mode;
            if (A[i] == B[j]) dp[i][j] = (mode + dp[i][j] + dp[i - 1][j - 1] + 1) % mode;
        }
    }
    ll ans = 0;
    for (int i = 1;i <= len_A;i ++) {
        for (int j = 1;j <= len_B;j ++) {
            if (A[i] < B[j]) {
                int l = len_A - i, r = len_B - j;
                if (l + r > 9500) ans = (ans + (dp[i - 1][j - 1] + 1) * Lucas(l + r, min(l, r)) + mode) % mode;
                else ans = (ans + (dp    [i - 1][j - 1] + 1) * c[l + r][min(l, r)] + mode) % mode;
            }
        }
    }
    printf ("%lld\n",ans);
    return 0;
}
```
