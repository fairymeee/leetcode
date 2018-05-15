---
description: 
---

# 无重复字符的最长子串

## 题目描述
给定一个字符串，找出不含有重复字符的**最长子串**的长度。

**示例：**

给定 `"abcabcbb"` ，没有重复字符的最长子串是 `"abc"` ，那么长度就是3。

给定 `"bbbbb"` ，最长的子串就是 `"b"` ，长度是1。

给定 `"pwwkew" `，最长子串是 `"wke"` ，长度是3。请注意答案必须是一个**子串**，`"pwke" `是 *子序列*  而不是子串。

## 解题思路
1. 判断出已经遍历过的字符
2. 使用`startIndex`和`endIndex`来标识当前的**“无从重复子串“**，使用`while`循环比较合适，因为会重复遍历同一个字符
3. 如果当前字符为第一次遍历，则将其添加到集合中，并将`endIndex`值加1。
4. 如果当前字符不是第一次遍历，需要更新`maxLength`，并移除`startIndex`对应的数据，然后再更新`startIndex`值（从`startIndex`开始移除，直到不在包含当前字符）

## 实现代码
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int maxLength = 0;

        if (s == null || s.length() == 0) {
            return maxLength;
        }

        int startIndex = 0;
        int endIndex = 0;

        int length = s.length();
        Set<Character> set = new HashSet<>();
        while (startIndex < length && endIndex < length && startIndex <= endIndex) {
            char c = s.charAt(endIndex);
            if (!set.contains(c)) {
                set.add(c);
                endIndex++;
            } else {
                if (endIndex - startIndex > maxLength) {
                    maxLength = endIndex - startIndex;
                }
                set.remove(s.charAt(startIndex));
                startIndex++;
            }
        }
        if (endIndex - startIndex > maxLength) {
            maxLength = endIndex - startIndex;
        }
        return maxLength;
    }
}
```

## 总结
1. 使用`HashSet`来存放字符
 - 便于快速判断重复出现的字符
 - 便于移除旧子串

2. 使用`startIndex`和`endIndex`来标识当前的**“无从重复子串“**
3. 使用`while`循环
 - 不使用`for`循环，因为会重复遍历同一个字符