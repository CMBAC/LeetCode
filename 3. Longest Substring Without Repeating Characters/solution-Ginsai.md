给定一个字符串，找出不含有重复字符的最长子串的长度。

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 无重复字符的最长子串是 "abc"，其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 无重复字符的最长子串是 "b"，其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 无重复字符的最长子串是 "wke"，其长度为 3。
     请注意，答案必须是一个子串，"pwke" 是一个子序列 而不是子串。




#### 思路
- 使用数组作为哈希表，以当前字符的大小作为数组arr中的索引位置，数组中存储的值为当前字符所在位置+1
- 遍历字符串，以当前遍历的字符为索引，查找在数组arr中的值,分为两种情况：
  1. 如果值为0，说明之前没有出现过，则将当前字符大小作为索引，将当前字符所在的位置+1后存入数组，最大长度maxLen更新
  2. 如果值不为0，说明这个字符可能出现过，又分为两种情况：
     1. 如果arr中当前字符对应的值（即当前字符上一次出现的位置）-1小于当前子字符串开始的位置start，则不重复，子字符串继续向后添加，最大长度maxLen更新
     2. 如果arr中当前字符对应的值（即当前字符上一次出现的位置）-1大于当前子字符串开始的位置start，则重复，子字符串重新需重新开始添加，开始的位置start为当前字符串上一次出现的位置+1（即数组中当前字符对应的值）
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] arr=new int[128];
        int maxLen=0;
        int start=0;//当前不重复子串开始的位置
        for(int i=0;i<s.length();i++){
            if(arr[s.charAt(i)]==0){//当前字符第一次出现
                maxLen=Math.max(maxLen,i+1-start);
            }else{//当前字符重复出现
                if(arr[s.charAt(i)]-1<start){//当前字符重复出现，但是在字符串中第一次出现，则继续添加
                    maxLen=Math.max(maxLen,i+1-start);
                    arr[s.charAt(i)]=i+1;
                    continue;
                }
                start=arr[s.charAt(i)];
            }
            arr[s.charAt(i)]=i+1;
        }
        return maxLen;
    }
}
```
