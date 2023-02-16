# 简介

给定两个大小分别为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的 中位数 。

算法的时间复杂度应该为 O(log (m+n)) 。


# 解题思路

思路一：最简单的先排序，后面找中位数。时间复杂度O(nlogn)。简单但是不满足时间要求。排序优化，因为两个数组都是有序数组，所以时间复杂度O(nlogn)降为O(n)

思路二：因为算法时间复杂度要求O(log (m+n))，所以只能使用二分查找解决。中位数分两种情况，m+n为奇数只需找到一个中位数，为偶数需要找到两个中位数。

关键问题：如何缩小二分区间？

发现很难，果断放弃看答题解析，发现有一个题目有非常有趣的解法，通过求第k小的数来得出中位数。

思路三：要寻找第k小的数，首先选取两个数组中前k/2向下取整，比较大小，直接淘汰小的之前的元素。然后剩下的数组求第k-淘汰元素个数小的数，重复直到有数组被全部淘汰或者k=0或者1。O(log (m+n))



# 代码

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        //解法一：先排序后求中位数
        int[] sumNums = new int[nums1.length+nums2.length];
        int i = 0;
        int j = 0;
        int temp = 0;
        while(i>=nums1.length&&j>=nums2.length){
            if(i>=nums1.length){
                sumNums[temp++] = nums2[j++];
            }else if(j>=nums2.length){
                sumNums[temp++] = nums1[i++];
            }else{
                if(nums1[i]<nums2[j]){
                    sumNums[temp++] = nums1[i++];
                }else{
                    sumNums[temp++] = nums2[j++];
                }
            }
        }
        return sumNums.length%2==1?sumNums(sumNums.length/2):(sumNums[sumNums.length/2]+sumNums[sumNums.length/2-1]);
    }
}
```

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        //解法二：求第k小
        int k = (nums1.length + nums2.length + 1) / 2;
        if ((nums1.length + nums2.length) % 2 == 1) {
            return getLessNumK(nums1,nums2,k);
        } else {
            return (getLessNumK(nums1,nums2,k)+getLessNumK(nums1,nums2,k+1))/2.0;
        }
    }

    private int getLessNumK(int[] nums1, int[] nums2,int k){
        int s1Start = 0;
        int s2Start = 0;
        while (k > 1) {
            int offCount = k / 2;
            int s1Num = 0;
            int out = 0;
            if (s1Start >= nums1.length) {
                s1Num = Integer.MAX_VALUE;
            } else {
                s1Num = (s1Start + offCount - 1) >= nums1.length ? nums1[nums1.length - 1] : nums1[s1Start + offCount-1];
            }
            int s2Num = 0;
            if (s2Start >= nums2.length) {
                s2Num = Integer.MAX_VALUE;
            } else {
                s2Num = (s2Start + offCount -1) >= nums2.length ? nums2[nums2.length - 1] : nums2[s2Start + offCount-1];
            }
            if (s1Num < s2Num) {
                s1Start = s1Start + offCount;
                if(s1Start>nums1.length){
                    out = offCount-s1Start+nums1.length;
                }else{
                    out = offCount;
                }
            } else {
                s2Start = s2Start + offCount;
                if(s2Start>nums2.length){
                    out = offCount-s2Start+nums2.length;
                }else{
                    out = offCount;
                }
            }
            k = k - out;
        }
        if (s1Start >= nums1.length) {
            return nums2[s2Start];
        }
        if (s2Start >= nums2.length) {
            return  nums1[s1Start];
        }
        return Math.min(nums2[s2Start],nums1[s1Start]);
    }
}
```