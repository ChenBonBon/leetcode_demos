# [最长公共前缀](https://leetcode.cn/problems/longest-common-prefix/)

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

**示例 1：**

```
输入：strs = ["flower","flow","flight"]
输出："fl"
```

**示例 2：**

```
输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
```

**提示：**

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` 仅由小写英文字母组成

## 题解

### 双循环 O(mn)

```typescript
function longestCommonPrefix(strs: string[]): string {
  let prefix = strs[0];

  for (let i = 1; i < strs.length; i++) {
    while (prefix.length) {
      if (strs[i].indexOf(head) === 0) {
        prefix = prefix.slice(0, prefix.length - 1);
      } else {
        prefix = "";
        break;
      }
    }
  }

  return prefix;
}
```

### 分治 O(mn)

```typescript
function longestCommonPrefix(strs: string[]): string {
  let prefix = strs[0];

  for (let i = 1; i < strs.length; i++) {
    prefix = getCommonPrefix(prefix, strs[i]);

    if (prefix.length === 0) {
      break;
    }
  }

  return prefix;
}

function getCommonPrefix(str1: string, str2: string): string {
  let i = 0;
  let prefix = "";

  while (i < str1.length && i < str2.length) {
    if (str1[i] === str2[i]) {
      prefix += str1[i];
      i++;
    } else {
      break;
    }
  }

  return prefix;
}
```
