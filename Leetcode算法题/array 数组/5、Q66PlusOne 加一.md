**Q66PlusOne：加一**

**题目类型：** 数组

**题目难度：** 简单

**题目地址：**https://leetcode-cn.com/problems/plus-one/

给定一个由 **整数** 组成的 **非空** 数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储**单个**数字。

你可以假设除了整数 0 之外，这个整数不会以零开头

示例 1：

```
输入：digits = [1,2,3]
输出：[1,2,4]
解释：输入数组表示数字 123。
```

**思路：**

* 方法一：取余判断
* 方法二：直接判断是否小于9，小于则直接返回

**题解：**

方法一：取余判断

```java
public int[] plusOne(int[] digits) {
    //方法一：取余判断
    for (int i = digits.length - 1; i >= 0; i--) {
        digits[i]++;
        digits[i] = digits[i] % 10;
        if (digits[i] != 0) {
            // 没有进位，直接返回
            return digits;
        }
    }
    digits = new int[digits.length + 1];
    digits[0] = 1;
    return digits;
}
```

方法二：直接判断是否小于9，小于则直接返回

```java
public int[] plusOne(int[] digits) {
    //方法二：判断是否小于9
    for (int i = digits.length - 1; i >= 0; i--) {
        // 直接判断是否小于9，小于则直接返回
        if (digits[i] < 9) {
            digits[i]++;
            return digits;
        }
        digits[i] = 0;
    }
    // 如果成功退出循环，则表示除了最高位，其他位都为0，无需赋值
    // 只用将最高位即数组下标为0的位置设为1即可，例如：999 + 1 => 1000
    digits = new int[digits.length + 1];
    digits[0] = 1;
    return digits;
}
```

