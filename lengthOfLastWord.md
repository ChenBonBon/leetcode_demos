# [最后一个单词的长度](https://leetcode.cn/problems/length-of-last-word/)

给你一个字符串 `s`，由若干单词组成，单词前后用一些空格字符隔开。返回字符串中 **最后一个** 单词的长度。

**单词** 是指仅由字母组成、不包含任何空格字符的最大

子字符串

。



 

**示例 1：**

```
输入：s = "Hello World"
输出：5
解释：最后一个单词是“World”，长度为5。
```

**示例 2：**

```
输入：s = "   fly me   to   the moon  "
输出：4
解释：最后一个单词是“moon”，长度为4。
```

**示例 3：**

```
输入：s = "luffy is still joyboy"
输出：6
解释：最后一个单词是长度为6的“joyboy”。
```

 

**提示：**

- `1 <= s.length <= 104`
- `s` 仅有英文字母和空格 `' '` 组成
- `s` 中至少存在一个单词

## 题解

### 正向查找 O(n)

```typescript
function lengthOfLastWord(s: string): number {
  let slow = 0;
  let fast = 0;
  let result = 0;
  
  while (fast < s.length) {
		if (s[fast] === " ") {
      if (fast - slow > 0) {
        result = fast - slow;
      }
      slow = fast + 1;
    }
    
    fast++;
  }
  
  return fast - slow > 0 ? fast - slow : result;
}
```



### 反向查找 O(n)

```typescript
function lengthOfLastWord(s: string): number {
  let i = s.length - 1;
  
  for (i; i >= 0; i--) {
    if (s[i] !== " ") {
      break;
    }
  }
  
  for (let j = i; j >= 0; j--) {
    if (s[j] === " ") {
      return i - j;
    }
  }
}
```

