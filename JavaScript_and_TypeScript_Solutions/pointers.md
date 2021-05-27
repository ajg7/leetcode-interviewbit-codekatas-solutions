## Pointers

### 844. Backspace String Compare

```javascript
const backspaceCompare = (S, T) => {
	const check = string => {
		const stack = [];
		for (const s of string) {
			if (s !== "#") stack.push(s);
			else if (stack.length !== 0) stack.pop();
		}
		return stack.join("");
	};
	return check(S) === check(T);
};
```

### 977. Squares of a Sorted Array

```javascript
const sortedSquares = nums => {
	let length = nums.length;
	let result = new Array(length);
	let left = 0;
	let right = length - 1;

	for (let i = length - 1; i >= 0; i--) {
		let square;
		if (Math.abs(nums[left]) < Math.abs(nums[right])) {
			square = nums[right];
			right--;
		} else {
			square = nums[left];
			left++;
		}
		result[i] = square * square;
	}
	return result;
};
```
