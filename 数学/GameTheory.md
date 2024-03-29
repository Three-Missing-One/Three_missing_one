---
documentclass:
    - ctexart
---

[TOC]

## 巴什博弈
### 原型
> 有$n$个物品,两个人轮流从这堆物品中取物,规定每次至少取一个,最多取$m$个。最后取光者得胜。
### 结论
> 若 $n\%(m+1)$不等于0,则先手必胜


## 斐波那契博弈
### 原型
> 有一堆个数为n的石子,游戏双方轮流取石子,满足：
> 1. 先手不能在第一次把所有的石子取完；
> 2. 之后每次可以取的石子数介于1到对手刚取的石子数的2倍之间   
>  （包含1和对手刚取的石子数的2倍）。  
> 约定取走最后一个石子的人为赢家,求必败态。
### 结论
> 先手胜当且仅当$n$不是斐波那契数（$n$为物品总数）
### 例题
[2019徐州网络赛-A. Who's Better](https://nanti.jisuanke.com/t/41383)(拓展中国剩余定理+斐波那契博弈)

## 威佐夫博弈
### 原型
> 有两堆各若干个物品,两个人轮流从某一堆或同时从两堆中取同样多的物品,规定每次至少取一个,多者不限,最后取光者得胜。
### 结论
> 必败状态：
> $(a_k,b_k):a_k = \lfloor \frac{1+\sqrt5}{2}*k\rfloor,\,\, b_k=a_k + k$

## 尼姆博弈
### 原型
> 有3堆物品,每堆个数若干,两个人轮流从某一堆取任意多的
物品,规定每次至少取一个,多者不限,最后取光者得胜。
### 结论
> 每堆物品数全部异或,如果得到的值为0,那么先手必败,否则先手必胜。

## SG函数和SG定理
### 引理
> $sg(x,y)=mex(Sx∪Sy)$。
### 内容
> SG定理：组合游戏和（整个游戏）的SG函数等于各个游戏SG函数的Nim和。
> SG值为零时一方胜,反之另一方胜。

### 使用
> 摘自xyw师哥PPT
> 解题模型：
> 1. 把原游戏分解成多个独立的子游戏,则原游戏的SG函数值是它的所有子游戏的SG函数值的Nim和,即$SG(G)=SG(G_1)$ ^ $SG(G_2)$^...^$SG(G_n)$
> 2. 分别考虑每一个子游戏,计算其$SG$值。
>对每一个子游戏求SG值时,一般可以选择打表找规律,实在找不到规律再老老实实用定义求SG值的方法。
一些对时间复杂度要求较高的题,无法通过定义求SG值,这时只能选择找规律。

一般用于博弈打表找规律
高级的目前现在太菜不会。。。
### 实例
* [1-2-K Game](https://vjudge.net/problem/CodeForces-1194D)

> $n$颗石子,每次可以选择拿$1$、$2$或者$k$个,最后取光者胜。

* [Fibonacci again and again](http://acm.hdu.edu.cn/showproblem.php?pid=1848) (多堆博弈取异或和)
### 实现
```cpp
// 渣渣写的自用SG函数,复杂度较高
// 作用：Nim博弈打表,sg值为零时一方胜,多堆博弈取异或和
// 1-2-K Game SG函数打表
#include <bits/stdc++.h>
using namespace std;
const int maxn = 1e5 + 5;

int sg[maxn];
int f[] = { 1,2,4 }; //单次可以取的数
set<int> s;

int mex() //返回不在集合中的最小非负整数
{
	for (int i = 0; ; i++) {
		if (s.count(i) == 0) {
			s.clear();
			return i;
		}
	}
	s.clear();
}

void getSG(int n)
{
	memset(sg, 0, sizeof(sg));
	for(int i = 1; i <= n; i++) {
		for(int j = 0; f[j] <= i; j++) {
			if (f[j] == 0) break;
			s.insert(sg[i - f[j]]);
		}
//		printf("set[%d] = ", i); //用于查看当前set中的值
//		for(set<int> :: iterator it = s.begin(); it != s.end(); it++) printf("%d ", *it); printf("\n");
		sg[i] = mex();
	}
}

int main()
{
	getSG(10);
	for(int i = 0; i < 10; i++)
		cout << sg[i] << " ";
}
```
