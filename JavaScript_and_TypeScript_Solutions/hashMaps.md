## Hash Maps

### 1. Two Sum

```javascript
const twoSum = (nums, target) => {
	const map = new Map();
	for (let i = 0; i < nums.length; i++) {
		let complement = target - nums[i];
		if (map.has(complement)) {
			return new Array(map.get(complement), i);
		}
		map.set(nums[i], i);
	}
	return -1;
};
```
