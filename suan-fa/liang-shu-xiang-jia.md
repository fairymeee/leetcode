---
description: null
---

# 两数相加

## 题目描述

给定两个**非空**链表来表示两个非负整数。位数按照**逆序**方式存储，它们的每个节点只存储单个数字。将两数相加返回一个新的链表。

> 你可以假设除了数字 0 之外，这两个数字都不会以零开头。

**示例：**

```text
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

## 解题思路

1. 遍历链表取出链表的值相加插入新节点中
2. 区分头节点与非头节点的插入
3. 考虑**进位**操作

## 实现代码

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */

class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode result = null;
        int next = 0;
        while (null != l1 || null != l2 || next != 0) {
            int sum = (null == l1 ? 0 : l1.val) + (null == l2 ? 0 : l2.val) + next;
            if (null == result) {
                result = new ListNode(sum % 10);
            } else {
                ListNode temp = result;
                while (null != temp.next) {
                    temp = temp.next;
                }
                temp.next = new ListNode(sum % 10);
            }
            next = sum / 10;
            l1 = null == l1 ? l1 : l1.next;
            l2 = null == l2 ? l2 : l2.next;
        }
        return result;
    }
}
```

## 总结

1. 遍历链表

   ```java
   while (null != listNode) {
      listNode = listNode.next;
   }
   ```

2. 插入链表
   * 插入头节点

     ```java
     if (null == listNode) {
        listNode = new ListNode(val);
     }
     ```

   * 插入下一节点

     ```java
     if (null != listNode) {
        ListNode temp = listNode;
        while (temp.next != null) {
            temp = temp.next;
        }
        temp.next = new ListNode(val);
     }
     ```

     > 新建一个ListNode对象得到源链表的内存地址，再将新链表对象读取到链尾，把需要插入的节点赋值到链尾节点，完成源链表的插入操作。
3. 遍历条件加上`next != 0`

   > 当两个链尾节点都为`null`了，但上一节点的两个值相加大于`10`，这时便需要**进位**操作。

4. 获取链表内的`val`值或读取下一个`next`节点需要判断当前节点是否为`null`

   > 当前节点为`null`时，`val`和`next`是不存在的，这时会报**空指针异常**错误。

