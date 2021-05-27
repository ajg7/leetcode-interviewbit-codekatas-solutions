## Arrays

### 448. Find All Numbers Disappeared in an Array

```typescript
const findDisappearedNumbers = (nums: number[]): number[] => {
	const result: number[] = [];
	const numberSet = new Set(nums);

	for (let i = 1; i <= nums.length; i++) {
		if (!numberSet.has(i)) result.push(i);
	}

	return result;
};
```

### 217. Contains Duplicate

```javascript
const containsDuplicate = nums => {
	const numSet = new Set(nums);
	return numSet.size !== nums.length;
};
```

### Remove Element

```javascript
// Pointer Solution
const removeElement = (nums, val) => {
	let pointer = 0;
	for (let i = 0; i < nums.length; i++) {
		if (nums[i] !== val) {
			nums[pointer] = nums[i];
			pointer++;
		}
	}
	return pointer;
};

// Splice Solution
const removeElement = (nums, val) => {
	for (let i = nums.length - 1; i >= 0; i--) {
		if (nums[i] === val) nums.splice(i, 1);
	}
	return nums.length;
};
```

### Merge Sorted Array

```javascript
const merge = (nums1, m, nums2, n) => {
	let first = m - 1;
	let second = n - 1;

	for (let i = m + n - 1; i >= 0; i--) {
		if (second < 0) break;
		if (nums1[first] > nums2[second]) {
			nums1[i] = nums1[first];
			first--;
		} else {
			nums1[i] = nums2[second];
			second--;
		}
	}
};
```

### Duplicate Zeros

```javascript
const duplicateZeros = arr => {
	for (let i = 0; i < arr.length; i++) {
		if (!arr[i]) {
			arr.splice(i, 0, 0);
			i++;
			arr.pop();
		}
	}
};
```
