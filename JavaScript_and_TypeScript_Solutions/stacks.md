## Stacks

### 1614. Maximum Nesting Depth of the Parentheses

```javascript
// Time Complexity: O(n)
// Space-Complexity: O(n)

const maxDepth = s => {
	const stack = [];
	let max = 0;

	for (const char of s) {
		if (char === "(") {
			stack.push(char);
		}

		max = Math.max(max, stack.length);

		if (char === ")") {
			stack.pop();
		}
	}

	return max;
};
```
