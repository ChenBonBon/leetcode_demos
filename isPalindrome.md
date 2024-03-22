# [回文数](https://leetcode.cn/problems/palindrome-number/)

给你一个整数 `x` ，如果 `x` 是一个回文整数，返回 `true` ；否则，返回 `false` 。

回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

- 例如，`121` 是回文，而 `123` 不是。

**示例 1：**

```
输入：x = 121
输出：true
```

**示例 2：**

```
输入：x = -121
输出：false
解释：从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

**示例 3：**

```
输入：x = 10
输出：false
解释：从右向左读, 为 01 。因此它不是一个回文数。
```

**提示：**

`-231 <= x <= 231 - 1`

**进阶：** 你能不将整数转为字符串来解决这个问题吗？

## 题解

### 转为字符串 O(n)

```typescript
function isPalindrome(x: number): boolean {
  const str = x.toString();
  let i = 0;
  let j = str.length - i - 1;

  for (i, j; i < j; i++, j--) {
    if (str[i] !== str[j]) {
      return false;
    }
  }

  return true;
}
```

### 反转一半数字 O(log n)

```typescript
function isPalindrome(x: number): boolean {
  // 负数一定不是回文数
  if (x < 0) {
    return false;
  }

  // 个位数一定是回文数
  if (x >= 0 && x < 10) {
    return true;
  }

  //   尾数为 0 的非个位数一定不是回文数
  if (x % 10 === 0) {
    return false;
  }

  let reversedNum = 0;

  // 当没有反转一半时
  while (x > reversedNum) {
    // 已经反转的乘以 10 加上 x 的最后一位
    reversedNum = reversedNum * 10 + Math.floor(x % 10);
    // x 舍去最后一位
    x = Math.floor(x / 10);
  }

  // 反转完成时，若正好对半，则判断是否相等，否则判断反转后的舍去末位是否相等
  return x === reversedNum || x === Math.floor(reversedNum / 10);
}
```
