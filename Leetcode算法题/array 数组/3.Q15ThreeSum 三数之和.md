**Q15ThreeSum：三数之和**

**题目类型：** 数组

**题目难度：** 中等

**题目地址：https://leetcode-cn.com/problems/3sum/**

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

示例：

给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]

****

**思路：**

* 方法一：暴力求解
* 方法二：hash表来记录，a + b = -c
* 方法三：左右推进，时间复杂度(O(n^2))

**题解：**

方法三：左右推进，时间复杂度(O(n^2))

```java
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    // 将数组从小到大排序
    Arrays.sort(nums);
    // i < nums.length - 2 保证其右边至少有两个数和其组成一个三元组
    for (int i = 0; i < nums.length - 2; i++) {
        // 防止出现重复值
        if (i > 0 && nums[i] != nums[i - 1] || i == 0) {
            int target = -nums[i], left = i + 1, right = nums.length - 1;
            while (left < right) {
                if (nums[left] + nums[right] == target) {
                    res.add(new ArrayList<>(Arrays.asList(nums[i],nums[left],nums[right])));
                    // 防止出现重复值
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    left++;
                    right--;
                } else if (nums[left] + nums[right] < target) {
                    // 和值太小，left左移
                    left++;
                } else {
                    // 和值太太，right右移
                    right--;
                }
            }
        }
    }
    return res;
```

