**Q1Two Sum：两数之和**

**题目类型：** 数组

**题目难度：** 简单

**题目地址**：https://leetcode-cn.com/problems/two-sum/

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]

**思路：**

* 暴力法：遍历
* 使用hashmap，降低时间、空间复杂度

**题解：**

暴力法：

```java
public int[] twoSum(int[] nums, int target) {
    int[] results = new int[2];
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target && i != j) {
                results[0] = i;
                results[1] = j;
                break;
            }
        }
    }
    return results;
}
```

使用hashmap，降低时间、空间复杂度（推荐）：

```java
public int[] twoSum(int[] nums, int target) {
    HashMap<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        if (map.containsKey(target - nums[i])) {
            return new int[]{map.get(target - nums[i]), i};
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

