---
description: 
---

# 回文数

## 题目描述
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:**
```
输入: 121
输出: true
```
**示例 2:**
```
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```
**示例 3:**
```
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```
**进阶:**
你能不将整数转为字符串来解决这个问题吗？
## 解题思路
1. 负数一定不是，个位数一定是
2. 使用log10函数得到位数
3. 使用除和幂级数得到每位数上的数值并反过来组合（比如三位数：百位当个位）

## 实现代码
```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        } else if (x >= 0 && x < 10) {
            return true;
        } else {
            int y = 0;
            int z = x;
            int length = (int) Math.log10(x);
            for (int i = length; i >= 0; i--) {
                y += (z / (int) Math.pow(10, i)) * (int) Math.pow(10, length - i);
                z -= (z / (int) Math.pow(10, i)) * (int) Math.pow(10, i);
            }
            return x == y;
        }
    }
}
```

## 总结
1. 利用`Math`函数计算
 - `Math.log10(x)` 即 `logx/log10`
 - `Math.pow(10, i)` 即 `10^i`