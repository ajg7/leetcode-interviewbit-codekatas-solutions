## Binary Search Trees

### 226. Invert Binary Tree

```javascript
const invertTree = root => {
	if (!root) return null;

	let right = invertTree(root.right);
	let left = invertTree(root.left);
	root.right = left;
	root.left = right;
	return root;
};
```

### 572. Subtree of Another Tree

```javascript
const isSubtree = (s, t) => {
	const set = new Set();

	const preorder = (t, left) => {
		if (!t) {
			if (left) {
				return "lnull";
			} else {
				return "rnull";
			}
		}
		return `#${t.val} ${preorder(t.left, true)} ${preorder(t.right, false)}`;
	};

	let tree1 = preorder(s, true);
	let tree2 = preorder(t, true);
	return tree1.indexOf(tree2) >= 0;
};
```

### 235. Lowest Common Ancestor of a Binary Search Tree

```javascript
const lowestCommonAncestor = (root, p, q) => {
	let parent = root.val;
	let pVal = p.val;
	let qVal = q.val;

	if (pVal > parent && qVal > parent) {
		return lowestCommonAncestor(root.right, p, q);
	} else if (pVal < parent && qVal < parent) {
		return lowestCommonAncestor(root.left, p, q);
	} else {
		return root;
	}
};
```

### 543. Diameter of Binary Tree

```javascript
const diameterOfBinaryTree = root => {
	let diameter = 0;

	const longestPath = node => {
		if (!node) return 0;
		let left = longestPath(node.left);
		let right = longestPath(node.right);

		diameter = Math.max(diameter, left + right);

		return Math.max(left, right) + 1;
	};

	longestPath(root);
	return diameter;
};
```

### 617. Merge Two Binary Trees

```javascript
const mergeTrees = (root1, root2) => {
	if (!root1) return root2;
	if (!root2) return root1;
	root1.val += root2.val;
	root1.left = mergeTrees(root1.left, root2.left);
	root1.right = mergeTrees(root1.right, root2.right);
	return root1;
};
```

### 112. Path Sum

```javascript
const hasPathSum = (root, targetSum) => {
	if (!root) return false;
	targetSum -= root.val;
	if (!root.left && !root.right) return targetSum === 0;
	return hasPathSum(root.left, targetSum) || hasPathSum(root.right, targetSum);
};
```

### 100. Same Tree

```javascript
const isSameTree = (p, q) => {
	if (!p && !q) return true;
	if (!p || !q) return false;
	if (p.val !== q.val) return false;
	return isSameTree(p.right, q.right) && isSameTree(p.left, q.left);
};
```

### 637. Average of Levels in Binary Tree

```javascript
const averageOfLevels = root => {
	const numbers = [];
	const queue = [];
	if (root) queue.push(root);
	while (queue.length !== 0) {
		let sum = 0;
		let queueLength = queue.length;
		for (let i = 0; i < queueLength; i++) {
			let currentNode = queue.shift();
			sum += currentNode.val;
			if (currentNode.left !== null) queue.push(currentNode.left);
			if (currentNode.right !== null) queue.push(currentNode.right);
		}
		numbers.push(sum / queueLength);
	}
	return numbers;
};
```

### 98. Validate Binary Search Trees

```typescript
const isValidBST = (root: TreeNode | null): boolean => {
	const validate = (root: TreeNode | null, low: number, high: number): boolean => {
		if (!root) return true;
		if ((low !== null && root.val <= low) || (high !== null && root.val >= high)) return false;

		return validate(root.right, root.val, high) && validate(root.left, low, root.val);
	};

	return validate(root, null, null);
};
```

### 111. Minimum Depth of Binary Tree (BFS)

```javascript
const minDepth = root => {
	if (!root) return 0;
	if (!root.left) return minDepth(root.right) + 1;
	if (!root.right) return minDepth(root.left) + 1;
	return Math.min(minDepth(root.left), minDepth(root.right)) + 1;
};
```

### 104. Maximum Depth of Binary Tree (DFS)

```javascript
const maxDepth = root => {
	const checkDepth = (node, depth) => {
		if (node === null) return depth;
		depth++;
		const leftSide = checkDepth(node.left, depth);
		const rightSide = checkDepth(node.right, depth);
		return Math.max(leftSide, rightSide);
	};
	return checkDepth(root, 0);
};
```

#### Shorter Version

```javascript
const maxDepth = root => {
	if (!root) return 0;
	const left = maxDepth(root.left);
	const right = maxDepth(root.right);
	return Math.max(left, right) + 1;
};
```

### 700. Search in a Binary Search Tree

```javascript
const searchBST = (root, val) => {
	if (!root) return null;
	if (root.val === val) return root;
	if (root.val > val) return searchBST(root.left, val);
	if (root.val < val) return searchBST(root.right, val);
};
```

### 617. Merge Two Binary Trees

```javascript
const mergeTrees = (t1, t2) => {
	if (!t1 || !t2) return t1 || t2;
	t1.val += t2.val;
	t1.left = mergeTrees(t1.left, t2.left);
	t1.right = mergeTrees(t1.right, t2.right);
	return t1;
};
```

### 938. Range Sum of BST

```javascript
const rangeSumBST = (root, low, high) => {
	if (!root) return 0;
	if (root.val < low) return rangeSumBST(root.right, low, high);
	if (root.val > high) return rangeSumBST(root.left, low, high);
	return root.val + rangeSumBST(root.left, low, high) + rangeSumBST(root.right, low, high);
};
```
