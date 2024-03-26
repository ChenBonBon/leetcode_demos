# [搜索插入位置](https://leetcode.cn/problems/search-insert-position/)

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 `O(log n)` 的算法。

 

**示例 1:**

```
输入: nums = [1,3,5,6], target = 5
输出: 2
```

**示例 2:**

```
输入: nums = [1,3,5,6], target = 2
输出: 1
```

**示例 3:**

```
输入: nums = [1,3,5,6], target = 7
输出: 4
```

 

**提示:**

- `1 <= nums.length <= 104`
- `-104 <= nums[i] <= 104`
- `nums` 为 **无重复元素** 的 **升序** 排列数组
- `-104 <= target <= 104`

## 题解

### 暴力搜索 O(n)

```typescript
function searchInsert(nums: number[], target: number): number {
  let i = 0;
  
  while (i < nums.length) {
    if (nums[i] >= target) {
			return i;
    } else if (nums[i] < target) {
      i++;
    }
  }
  
  return nums.length;
}
```

### 递归二分法 O(log n)

```typescript
function searchInsert(nums: number[], target: number): number {
  return binaraySearch(nums, target, 0, nums.length - 1);
}

function binaraySearch(nums: number[], target: number, low: number, high: number): number {
  if (low > high) {
		return low;
  }
  
  const mid = low + Math.floor((high - low) / 2);
  
  if (nums[mid] === target) {
		return mid;
  } else if (nums[mid] < target) {
    return binaraySearch(nums, target, mid + 1, high);
  } else {
    return binaraySearch(nums, target, low, high - 1);
  }
}
```



### 迭代二分法 O(log n)

```typescript
function searchInsert(nums: number[], target: number): number {
  let low = 0;
  let high = nums.length - 1;
  
  while (low <= high) {
		let mid = low + Math.floor((high - low) / 2);
    
    if (nums[mid] === target) {
      return mid;
    } else if (nums[mid] < target) {
			low = mid + 1;
    } else {
			high = mid - 1;
    }
  }
  
  return low;
}
```

