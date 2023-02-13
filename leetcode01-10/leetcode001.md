
# 简介
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。


# 解题思路

思路一：遍历数组，遍历元素nums[i]时，从i位置向后查找，找到target - nums[i]的值。时间复杂度O(n^2)，空间复杂度1.

思考后后发现，其实第一次查找是有效查找，我们可以通过HashMap保存结果避免冗余查找。

思路二：遍历数组，并将数组值为key，下标为value放入hashMap。只要后续元素能在Map中找到和为target的数，即得到结果。时间复杂度O(n),O(n)

# 代码

```java
class Solution {
public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i=0;i<nums.length;i++){
            if(map.get(target-nums[i])!=null){
                return {map.get(target-nums[i]),i};
            }else {
                map.put(nums[i],i);
            }
        }
        return [-1,-1];
    }
}
```
