# 简介

给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。


# 解题思路

一开始没看懂，后面发现这个就是加法运算。需要注意的问题：注意进位以及空指针。

注意点：

(1)使用递归来扩展链表，终止扩展条件为进位为0并且相加节点位置均为null。


# 代码

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode result = recursion(0, l1, l2);
        return result;
    }

    private ListNode recursion(int addFlag, ListNode l1, ListNode l2) {
        //先进行终止条件判断
        boolean l1IsNull = l1 == null;
        int l1Num = l1IsNull ? 0 : l1.val;
        boolean l2IsNull = l2 == null ;
        int l2Num = l2IsNull ? 0 : l2.val;
        if (l1IsNull && l2IsNull && addFlag == 0) {
            return null;
        }
        //进行加法运算
        int res = addFlag + l1Num + l2Num;
        if (res >= 10) {
            addFlag = 1;
            res = res - 10;
        } else {
            addFlag = 0;
        }
        //递归扩展结果链表
        ListNode listNode = new ListNode();
        listNode.val = res;
        listNode.next = recursion(addFlag,l1IsNull?null:l1.next,l2IsNull?null:l2.next);
        return listNode;
    }
}
```