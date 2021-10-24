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
	};

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

## 1469. Find All The Lonely Nodes

```javascript
const getLonelyNodes = root => {
	const dfs = node => {
		if (!node) return;
		if (node.left && !node.right) {
			result.push(node.left.val);
		} else if (!node.left && node.right) {
			result.push(node.right.val);
		}
		dfs(node.left);
		dfs(node.right);
	};

	const result = [];
	dfs(root);
	return result;
};
```

## 617. Merge Two Binary Trees

```javascript
const mergeTrees = (root1, root2) => {
	if (!root1 && !root2) {
		return null;
	}
	const root = new TreeNode((root1 ? root1.val : 0) + (root2 ? root2.val : 0));
	root.left = mergeTrees(root1 ? root1.left : null, root2 ? root2.left : null);
	root.right = mergeTrees(root1 ? root1.right : null, root2 ? root2.right : null);
	return root;
};
```

## 897. Increasing Order Search Tree

```javascript
const increasingBST = root => {
	const dfs = node => {
		if (!node) return;
		dfs(node.left);
		currTree.right = new TreeNode(node.val);
		currTree = currTree.right;
		dfs(node.right);
	};
	let dummyTree = new TreeNode();
	let currTree = dummyTree;
	dfs(root);
	return dummyTree.right;
};
```

## 589. N-ary Tree Preorder Traversal

```javascript
const preorder = root => {
	const dfs = node => {
		if (!node) {
			return;
		}

		result.push(node.val);
		for (const child of node.children) {
			dfs(child);
		}
	};

	if (!root) return [];
	const result = [];
	dfs(root);
	return result;
};
```

## 590. N-ary Tree Postorder Traversal

```javascript
const postorder = root => {
	const dfs = node => {
		if (!node) return;

		for (const child of node.children) {
			dfs(child);
		}
		result.push(node.val);
	};

	if (!root) return [];
	const result = [];
	dfs(root);
	return result;
};
```

## 1022. Sum of Root To Leaf Binary Numbers

```javascript
const sumRootToLeaf = root => {
	const dfs = node => {
		if (!node) return;

		path <<= 1;
		path |= node.val;
		if (!node.left && !node.right) {
			console.log(path);
			sum += path;
		}
		dfs(node.left);
		dfs(node.right);
		path >>= 1;
	};

	let path = 0;
	let sum = 0;
	dfs(root);
	return sum;
};
```

## 559. Maximum Depth of N-ary Tree

```javascript
const maxDepth = root => {
	if (!root) {
		return 0;
	}

	let childMaxDepth = 0;

	for (const child of root.children) {
		childMaxDepth = Math.max(childMaxDepth, maxDepth(child));
	}

	return 1 + childMaxDepth;
};
```

## 94. Binary Tree Inorder Traversal

```javascript
const inorderTraversal = root => {
	const dfs = node => {
		if (!node) {
			return;
		}

		dfs(node.left);

		result.push(node.val);

		dfs(node.right);
	};

	const result = [];
	dfs(root);
	return result;
};
```

## 965. Univalued Binary Tree

```javascript
const isUnivalTree = root => {
	const dfs = node => {
		if (!node) {
			return true;
		}

		if (node.val !== value) {
			return false;
		}

		const leftValue = dfs(node.left);
		const rightValue = dfs(node.right);

		return leftValue && rightValue;
	};

	const value = root.val;

	return dfs(root);
};
```
