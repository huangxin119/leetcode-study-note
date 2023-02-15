# 简介

给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串 的长度。

# 解题思路

非常典型的双指针题目，左指针表示不重复字符串起始位置，右指针表示不重复字符串结束位置。每次右指针向右前进一步，如果新加入字符已存在，左指针需要向前移动，直到和右指针组成的字符串为不重复字符串。直到右指针前进结束。

小优化：可以使用Map存储当前子串，方便判断字符是否重复。

时间复杂度O(n)，空间复杂度O(n)

# 代码

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int left = 0;
        int right = 0;
        int maxLen = 0;
        HashMap<Character,Integer> nowStr = new HashMap<>();
        //注意，这里是[left,right]表示当前字符串，所以字符串长度是right+1-left
        for(right=0;right<s.length();right++){
            if(nowStr.get(s.charAt(right))==null){
                maxLen = Math.max(maxLen,right+1-left);
            }else{
                //如果存在重复字符，将左边界缩小到无重复元素
                int newLeft = nowStr.get(s.charAt(right));
                for(int j=left;j<=newLeft;j++){
                    nowStr.remove(s.charAt(j));
                }
                left = newLeft+1;//这里一开始没注意到左开右闭，纠结了好久
            }
            nowStr.put(s.charAt(right),right);
        }
        return maxLen;
    }
}
```
