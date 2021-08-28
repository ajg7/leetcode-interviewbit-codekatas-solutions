## Dynamic Programming

### 303. Range Sum Query - Immutable

```javascript
class NumArray {
	constructor(nums) {
		this.nums = nums;
		this.prefix = nums.reduce((accumulator, num) => {
			let last = accumulator[accumulator.length - 1] || 0;
			accumulator.push(last + num);
			return accumulator;
		}, []);
	}

	sumRange(i, j) {
		if (i === 0) return this.prefix[j];
		return this.prefix[j] - this.prefix[i - 1];
	}
}
```

### 53. Maximum Subarray

#### Kadane's Alogrithm

```javascript
const maxSubArray = nums => {
	let currSubArraySum = -Infinity;
	let maxSubArraySum = -Infinity;

	for (const num of nums) {
		currSubArraySum = Math.max(num, currSubArraySum + num);
		maxSubArraySum = Math.max(maxSubArraySum, currSubArraySum);
	}

	return maxSubArraySum;
};
```

### 121. Best Time to Buy and Sell Stock

```typescript
const maxProfit = (prices: number[]): number => {
	if (prices.length < 2) return 0;

	let maxProfit: number = -Infinity;
	let minPrice: number = prices[0];
	for (const price of prices) {
		maxProfit = Math.max(maxProfit, price - minPrice);
		minPrice = Math.min(minPrice, price);
	}
	return maxProfit;
};
```

### 70. Climbing Stairs

```typescript
const climbStairs = (n: number): number => {
	if (n === 1) return 1;

	const memo: number[] = [n + 1];

	memo[1] = 1;
	memo[2] = 2;

	for (let i = 3; i <= n; i++) {
		memo[i] = memo[i - 1] + memo[i - 2];
	}

	return memo[n];
};
```
