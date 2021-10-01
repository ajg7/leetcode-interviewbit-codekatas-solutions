## 530. Minimum Absolute Difference in BST

```javascript
const getMinimumDifference = root => {
	const inorder = root => {
		if (root === null) {
			return;
		}

		inorder(root.left);

		if (prev !== null) {
			const diff = Math.abs(prev - root.val);
			minDiff = Math.min(minDiff, diff);
		}

		prev = root.val;

		inorder(root.right);
	};

	let prev = null;
	let minDiff = Infinity;

	inorder(root);

	return minDiff;
};
```
## 938. Range Sum of BST
```javascript
const rangeSumBST = (root, low, high) => {
    const dfs = node => {
        if (!node) return;
        if (low <= node.val && node.val <= high) {
            sum += node.val;
            dfs(node.left);
            dfs(node.right);
        } else if (node.val < low) {
            dfs(node.right);
        } else if (node.val > high) {
            dfs(node.left);
        }
    }
    
    let sum = 0;
    dfs(root);
    return sum; 
};
```

```javascript
const rangeSumBST = (root, low, high) => {
    if (!root) return 0;
    if (low <= root.val && root.val <= high) {
        return root.val + rangeSumBST(root.left, low, high) + rangeSumBST(root.right, low, high);
    } else if (root.val < low) {
        return rangeSumBST(root.right, low, high);
    } else if (root.val > high) {
        return rangeSumBST(root.left, low, high);
    }
    return 0;
};
```