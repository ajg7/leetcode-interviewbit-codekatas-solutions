## Sorting

### 169. Majority Element

#### Boyer-Moore Voting Algorithm

```javascript
const majorityElement = nums => {
	let count = 0;
	let candidate = null;

	for (const num of nums) {
		if (count === 0) {
			candidate = num;
		}

		count += num === candidate ? 1 : -1;
	}
	return candidate;
};
```
