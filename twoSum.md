# [两数之和](https://leetcode.cn/problems/two-sum/)

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

 

**提示：**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **只会存在一个有效答案**

 

**进阶：** 你可以想出一个时间复杂度小于 `O(n2)` 的算法吗？

## 题解

### 暴力破解法 O(n<sup>2</sup>)

```typescript
function twoSum(nums: number[], target: number): number[] {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }
}
```

### 完整遍历哈希表 O(n)

```typescript
function twoSum(nums: number[], target: number): number[] {
  const hashMap = {};
  
  for (let i = 0; i < nums.length; i++) {
    const num = nums[i];
    if (typeof hashMap[num] === "undefined") {
      hashMap[num] = i;
    } else {
			hashMap[num] = [hashMap[num], i]
    }
  }
  
  const keys = Object.keys(hashMap);
  
  for (let i = 0; i < keys.length; i++) {
    const key = Number(keys[i]);
    const targetKey = target - key;
    
    if (typeof hashMap[targetKey] === "undefined") {
      continue;
    }
    
    if (Array.isArray(hashMap[targetKey])) {
      return hashMap[targetKey];
    }
    
    return [i, hashMap[targetKey]];
  }
}
```



### 非完整遍历哈希表 O(n)

```typescript
function twoSum(nums: number[], target: number): number[] {
  const hashMap = {};
  
  for (let i = 0; i < nums.length; i++) {
    const num = nums[i];
    const targetKey = target - num;
    
    if (typeof hashMap[targetKey] !== "undefined") {
      return [hashMap[targetKey], i];
    } else {
			if (typeof hashMap[num] === "undefined") {
        hashMap[num] = i;
      } else {
        hashMap[num] = [hashMap[num], i];
      }
    }
  }
}
```

