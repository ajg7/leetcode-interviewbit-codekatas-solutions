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

const twoSum = (nums, target) => {
	const dict = {};

	for (let i = 0; i < nums.length; i++) {
		const candidate = target - nums[i];

		if (dict[candidate] !== undefined) {
			return [dict[candidate], i];
		}

		dict[nums[i]] = i;
	}

	return [];
};
```
