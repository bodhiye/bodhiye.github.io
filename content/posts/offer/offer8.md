---
title: "剑指offer8——跳台阶"
date: 2019-03-06T19:19:30+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

#### 题解

```c++
#include <iostream>

using namespace std;

int dp[101];

int jumpFloor(int number)
{
	if (number == 1 || number == 2)return number;
	if (dp[number])return dp[number];
	else
		return dp[number] = jumpFloor(number - 1) + jumpFloor(number - 2);
}

int main()
{
	ios::sync_with_stdio(false);
	int n;
	cin >> n;
	cout << jumpFloor(n) << endl;
	return 0;
}
```
