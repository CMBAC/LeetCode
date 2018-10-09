给定一个没有重复数字的序列，返回其所有可能的全排列。

示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]

思路：参考<a href="https://leetcode.com/problems/permutations/discuss/18239/
A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning)"/> 大佬的解法
回溯，[1]==》[1,2]进行递归，在[1,2,3]的时候将集合中值存入结果集合中，回溯到[1]，再由[1]==>[1,3]，再进行递归
```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> retList=new ArrayList<>();
        List<Integer> tmpList=new ArrayList<>();
        backTracking(retList,tmpList,nums);
        return retList;
    }
    private void backTracking(List<List<Integer>> list,List<Integer> tmpList,int nums[]){
        if (tmpList.size()==nums.length){
             list.add(new ArrayList<Integer>(tmpList));//回溯到最后tmpList会清空，所以需要每次在tmpList满了之后新建一个集合进行存储
        }
        for (int i = 0; i < nums.length; i++) {
            if (tmpList.contains(nums[i])){//重复则跳过
                continue;
            }
            tmpList.add(nums[i]);
            backTracking(list,tmpList,nums);//添加当前值之后递归
            tmpList.remove(tmpList.size()-1);//回溯，跳到下一个循环
        }
    }
}
```
