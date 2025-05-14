# 1. Two Sum（两数之和）
给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** 的那 **两个整数**，并返回它们的数组下标。

- 每种输入只对应一个答案。
- 不可以重复使用同一个元素。
- 可以按任意顺序返回答案。

### 示例 1：
输入：`nums = [2,7,11,15]`, `target = 9`  
输出：`[0,1]`  

### 示例 2：
输入：`nums = [3,2,4]`, `target = 6`  
输出：`[1,2]`  

### 示例 3：
输入：nums = [3,3], target = 6
输出：[0,1]
---

## 💡 Java 解法
暴力法：
最直接的做法就是对数组中的每一对元素都尝试一下，看看它们的和是否等于 target。
外层循环选定第一个元素 i，
内层循环选定第二个元素 j（j > i），
判断 nums[i] + nums[j] == target 就返回 [i, j]

示例：
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int n = nums.length;
        for(int i = 0; i < n; i++){
            for(int j = i +1; j < n; j++){
                if(nums[i]+nums[j]==target){
                    return new int[]{i,j};
                }
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}

哈希法：
