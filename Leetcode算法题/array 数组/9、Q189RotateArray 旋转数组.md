**Q189RotateArray：旋转数组**

**题目类型：** 数组

**题目难度：** 中等

**题目地址：**https://leetcode-cn.com/problems/rotate-array/

给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

示例 1:

```
输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]
```

**思路：**

* 方法一：暴力法，两层循环，内循环为所有元素后移一位
* 方法二：使用额外的数组
* 方法三：环形替换
* 方法四：使用反转

**题解：**

方法一：暴力法，两层循环，内循环为所有元素后移一位

```java
public void rotate(int[] nums, int k) {
    int temp = 0;   // 备份值
    for (int i = 0; i < k; i++) {
        temp = nums[nums.length - 1];
        for (int j = nums.length - 1; j > 0; j--) {
            nums[j] = nums[j - 1];
        }
        nums[0] = temp;
    }
}
```

方法二：使用额外的数组

```java
public void rotate(int[] nums, int k) {
    //创建一个新的数组
    int[] arr = new int[nums.length];
    for (int i = 0; i < nums.length; i++) {
        arr[(i + k) % nums.length] = nums[i];
    }
    //再将新数组覆盖原数组
    for (int i = 0; i < arr.length; i++) {
        nums[i] = arr[i];
    }
}
```

方法三：环形替换

```java
public void rotate(int[] nums, int k) {
    //方法三：环形替换
    //取模是针对k可能大于数组长度的情况
    k = k % nums.length;
    int count = 0;  // 替换次数，每个元素都要替换一次
    // 这里需要注意的是判断条件为：count < nums.length
    for (int start = 0 ; count < nums.length; start++) {
        int cur = start;
        int pre = nums[cur];    // 当前元素值
        // 进行位置替换，直到一个元素最终的替换位置回到cur
        do {
            cur = (cur + k) % nums.length;
            int temp = nums[cur];
            nums[cur] = pre;
            pre = temp;
            count++;
        } while (cur != start);
    }
}
```

方法四：使用反转

```java
public void rotate(int[] nums, int k) {
    // 方法四：使用反转，先全部反转，再反转前k个数和后n-k个数
    k = k % nums.length;
    // 先将全部数进行反转
    reverse(nums, 0, nums.length - 1);
    // 反转前 k 个数
    reverse(nums, 0, k - 1);
    // 反转后 n-k 个数
    reverse(nums, k, nums.length - 1);
}

private void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
```

