# [有效的括号](https://leetcode.cn/problems/valid-parentheses/)

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串 `s` ，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。
3. 每个右括号都有一个对应的相同类型的左括号。

**示例 1：**

```
输入：s = "()"
输出：true
```

**示例 2：**

```
输入：s = "()[]{}"
输出：true
```

**示例 3：**

```
输入：s = "(]"
输出：false
```

**提示：**

- `1 <= s.length <= 104`
- `s` 仅由括号 `'()[]{}'` 组成

## 题解

### 出入栈 O(n)

```typescript
function isValid(s: string): boolean {
  const hashMap = {
    "(": ")",
    "{": "}",
    "[": "]",
  };
  const stack = [];

  for (let i = 0; i < s.length; i++) {
    if (Object.keys(hashMap).includes(s[i])) {
      stack.push(s[i]);
    }

    if (Object.values(hashMap).includes(s[i])) {
      const top = stack.pop();

      if (hashMap[top] === s[i]) {
        continue;
      } else {
        return false;
      }
    }
  }

  return true;
}
```
