## Binary Search

### 852. Peak Index in a Mountain Array

```typescript
const peakIndexInMountainArray = (arr: number[]): number => {
	let low: number = 0;
	let high: number = arr.length - 1;

	while (low < high) {
		let mid: number = Math.floor(low + (high - low) / 2);

		if (arr[mid] < arr[mid + 1]) {
			low = mid + 1;
		} else {
			high = mid;
		}
	}
	return low;
};
```

### 33. Search in Rotated Sorted Array

```typescript
const search = (nums: number[], target: number): number => {
	let start: number = 0;
	let end: number = nums.length - 1;

	while (start <= end) {
		let mid = Math.floor(start + (end - start) / 2);

		if (nums[mid] === target) {
			return mid;
		} else if (nums[mid] >= nums[start]) {
			if (target >= nums[start] && target < nums[mid]) {
				end = mid - 1;
			} else {
				start = mid + 1;
			}
		} else {
			if (target <= nums[end] && target > nums[mid]) {
				start = mid + 1;
			} else {
				end = mid - 1;
			}
		}
	}
	return -1;
};
```

### 374. Guess Number Higher or Lower

```javascript
const guessNumber = n => {
	let left = 1;
	let right = n;
	while (left <= right) {
		const mid = Math.floor((right - left) / 2) + left;
		const result = guess(mid);

		if (result === 0) {
			return mid;
		} else if (result === 1) {
			left = mid + 1;
		} else {
			right = mid - 1;
		}
	}
};
```

### 69. Sqrt(x)

```typescript
const mySqrt = (x: number): number => {
	if (x < 2) return x;

	let left: number = 2;
	let right: number = Math.floor(x / 2);

	while (left <= right) {
		let pivot: number = Math.floor(left + (right - left) / 2);
		let num: number = pivot * pivot;

		if (num > x) {
			right = pivot - 1;
		} else if (num < x) {
			left = pivot + 1;
		} else {
			return pivot;
		}
	}

	return right;
};
```

### 744. Find Smallest Letter Greater Than Target

```typescript
const nextGreatestLetter = (letters: string[], target: string): string => {
	let left: number = 0;
	let right: number = letters.length - 1;

	while (left < right) {
		let mid: number = Math.floor((left + right) / 2);
		if (letters[mid] <= target) {
			left = mid + 1;
		} else {
			right = mid;
		}
	}

	return letters[left] <= target ? letters[0] : letters[left];
};
```

### 704. Binary Search

```typescript
// Time-Complexity: O(log n)
// Space-Complexity: O(1)
const search = (nums: number[], target: number): number => {
	let left: number = 0;
	let right: number = nums.length;

	while (left < right) {
		let mid: number = Math.floor((left + right) / 2);
		if (nums[mid] < target) {
			left = mid + 1;
		} else {
			right = mid;
		}
	}

	return nums[left] === target ? left : -1;
};
```

### 1351. Count Negative Numbers in a Sorted Matrix

```javascript
const countNegatives = grid => {
	let count = 0;
	for (let i = 0; i < grid.length; i++) {
		for (let j = 0; j < grid[i].length; j++) {
			if (Math.sign(grid[i][j]) === -1) count++;
		}
	}
	return count;
};
```
