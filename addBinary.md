# [二进制求和](https://leetcode.cn/problems/add-binary/)

给你两个二进制字符串 `a` 和 `b` ，以二进制字符串的形式返回它们的和。

 

**示例 1：**

```
输入:a = "11", b = "1"
输出："100"
```

**示例 2：**

```
输入：a = "1010", b = "1011"
输出："10101"
```

 

**提示：**

- `1 <= a.length, b.length <= 104`
- `a` 和 `b` 仅由字符 `'0'` 或 `'1'` 组成
- 字符串如果不是 `"0"` ，就不含前导零



## 题解

- 位运算

```typescript
function addBinary(a: string, b: string): string {
  if (a.length > b.length) {
    b = new Array(a.length - b.length).fill(0).join("") + b;
  } else {
    a = new Array(b.length - a.length).fill(0).join("") + a;
  }
  
  let add = 0;
  let result = [];
  
  for (let i = a.length - 1; i >= 0; i--) {
    result.unshift(Number(a[i]) ^ Number(b[i]) ^ add);
    
    if (Number(a[i]) + Number(b[i]) + add > 1) {
			add = 1;
    } else {
			add = 0;
    }
  }
  
  if (add > 0) {
		result.unshift(1);
  }
  
  return result.join("");
}
```

