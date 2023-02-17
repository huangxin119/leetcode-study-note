# 简介

给你一个字符串 s，找到 s 中最长的回文子串。

如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。

# 解题思路

回文子串去掉首尾字符仍然是回文字符串，所以可以使用动态规划，保存开始为i，结尾为j的最长回文字符串长度。

# 代码

//todo动态规划不熟练，需要专题练习
```java
class Solution {
    public String longestPalindrome(String s) {
        int maxLen = 1;
        int[][] dp = new int[s.length()][s.length];
        for(int i=0;i<s.length();i++){
            for(j=i;j<s.length();j++){
                if(i==j){
                    dp[i][j] = 1;
                }else{
                    if(dp[i][j-1]==1&&s.charAt(j)==s.charAt(i)){
                        dp[i][j] = 2;
                    }else if()
                }
            }
        }
    }

}

```