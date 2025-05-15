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

---

### 🚩 暴力法（Brute Force）

最直接的做法就是对数组中的每一对元素都尝试一下，看看它们的和是否等于 `target`。

- 外层循环选定第一个元素 `i`  
- 内层循环选定第二个元素 `j`（`j > i`）  
- 判断 `nums[i] + nums[j] == target` 就返回 `[i, j]`

#### 示例代码：

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int n = nums.length;
        for(int i = 0; i < n; i++){
            for(int j = i + 1; j < n; j++){
                if(nums[i] + nums[j] == target){
                    return new int[]{i, j};
                }
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}

## ⚡ 哈希法（Hash Map 法）

利用哈希表（`Map<值, 下标>`）将查找操作的时间复杂度从 **O(n²)** 降到 **O(n)**。

---

### 🧠 解题思路：

1. 遍历数组 `nums`，对每个元素 `nums[i]` 计算其“补数”：  
   `remain = target - nums[i]`

2. 在哈希表中查找 `remain` 是否存在：
   - ✅ **存在**：说明之前遇到过那个数，与当前数之和等于 `target`，直接返回两个下标。
   - ❌ **不存在**：将当前数 `nums[i]` 和其下标 `i` 存入哈希表中，继续遍历。

---

### 📌 示例代码：

```java
public int[] twoSumHashMap(int[] nums, int target) {
    // key：数组中的元素值；value：该元素的下标
    Map<Integer, Integer> map = new HashMap<>();
    
    for (int i = 0; i < nums.length; i++) {
        int remain = target - nums[i];
        // 如果补数已在 map 中，直接返回结果
        if (map.containsKey(remain)) {
            return new int[]{ map.get(remain), i };
        }
        // 否则将当前数及其下标加入 map
        map.put(nums[i], i);
    }
    
    // 题目保证一定有解
    throw new IllegalArgumentException("No two sum solution");
}

