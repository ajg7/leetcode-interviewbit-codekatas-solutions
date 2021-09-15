## 690. Employee Importance

```javascript
const GetImportance = (employees, id) => {
	const subordinatesMap = new Map();
	const importanceMap = new Map();
	const visited = new Set();
	let res = 0;

	for (const employee of employees) {
		subordinatesMap.set(employee.id, employee.subordinates);
		importanceMap.set(employee.id, employee.importance);
	}

	const queue = [];
	queue.push(id);
	res += importanceMap.get(id);

	while (queue.length !== 0) {
		const val = queue.shift();
		for (const subordinate of subordinatesMap.get(val)) {
			if (!visited.has(subordinate)) {
				queue.push(subordinate);
				visited.add(subordinate);
				res += importanceMap.get(subordinate);
			}
		}
	}

	return res;
};
```

## 1971. Find if Path Exists in Graph

```javascript
const validPath = (n, edges, start, end) => {
	const visited = new Set([start]);
	const queue = [start];
	const adjacencyList = {};

	for (const [u, v] of edges) {
		if (adjacencyList[u] === undefined) {
			adjacencyList[u] = [];
		}

		if (adjacencyList[v] === undefined) {
			adjacencyList[v] = [];
		}

		adjacencyList[u].push(v);
		adjacencyList[v].push(u);
	}

	while (queue.length !== 0) {
		const node = queue.shift();

		if (node === end) {
			return true;
		}

		const neighbors = adjacencyList[node];
		if (neighbors === undefined) {
			continue;
		}

		for (const neighbor of neighbors) {
			if (visited.has(neighbor)) {
				continue;
			}

			visited.add(neighbor);
			queue.push(neighbor);
		}
	}

	return false;
};
```

## 733. Flood Fill

```javascript
const floodFill = (image, sr, sc, newColor) => {
	const queue = [[sr, sc]];
	const m = image.length;
	const n = image[0].length;
	const dirs = [
		[-1, 0],
		[1, 0],
		[0, -1],
		[0, 1],
	];
	const startColor = image[sr][sc];

	if (startColor === newColor) {
		return image;
	}

	while (queue.length !== 0) {
		const [row, col] = queue.shift();
		image[row][col] = newColor;

		for (const [deltaRow, deltaCol] of dirs) {
			const nextRow = row + deltaRow;
			const nextCol = col + deltaCol;

			if (nextRow >= m || nextRow < 0 || nextCol >= n || nextCol < 0) {
				continue;
			}

			if (image[nextRow][nextCol] === startColor) {
				queue.push([nextRow, nextCol]);
			}
		}
	}

	return image;
};
```

## 1469. Find All The Lonely Nodes

```javascript
const getLonelyNodes = root => {
	const lonelyNodes = [];
	const queue = [root];

	while (queue.length) {
		const currNode = queue.shift();
		if (!currNode.left && currNode.right) {
			lonelyNodes.push(currNode.right.val);
		} else if (!currNode.right && currNode.left) {
			lonelyNodes.push(currNode.left.val);
		}

		if (currNode.left) {
			queue.push(currNode.left);
		}

		if (currNode.right) {
			queue.push(currNode.right);
		}
	}

	return lonelyNodes;
};
```

## 559. Maximum Depth of N-ary Tree

```javascript
const maxDepth = root => {
	if (!root) {
		return 0;
	}

	let level = 0;
	const queue = [root];

	while (queue.length) {
		const size = queue.length;

		for (let i = 0; i < size; i++) {
			const curr = queue.shift();
			for (const child of curr.children) {
				queue.push(child);
			}
		}

		level++;
	}

	return level;
};
```

## 104. Maximum Depth of Binary Tree

```javascript
const maxDepth = root => {
	if (!root) return 0;
	const queue = [root];
	let level = 0;

	while (queue.length) {
		const size = queue.length;
		for (let i = 0; i < size; i++) {
			const curr = queue.shift();
			if (curr?.left) queue.push(curr.left);
			if (curr?.right) queue.push(curr.right);
		}

		level++;
	}

	return level;
};
```

## 226. Invert Binary Tree

```javascript
const invertTree = root => {
	if (!root) return null;
	const queue = [root];

	while (queue.length) {
		const size = queue.length;

		for (let i = 0; i < size; i++) {
			const curr = queue.shift();
			if (curr) {
				[curr.left, curr.right] = [curr.right, curr.left];
				queue.push(curr.left, curr.right);
			}
		}
	}

	return root;
};
```

## 965. Univalued Binary Tree

```javascript
const isUnivalTree = root => {
	const queue = [root];
	const val = root.val;

	while (queue.length) {
		const size = queue.length;

		for (let i = 0; i < size; i++) {
			const curr = queue.shift();
			if (curr.val !== val) return false;
			if (curr.left) queue.push(curr.left);
			if (curr.right) queue.push(curr.right);
		}
	}

	return true;
};
```

## 200. Number of Islands

```javascript
const numIslands = grid => {
	let island = 0;
	for (let row = 0; row < grid.length; row++) {
		for (let col = 0; col < grid[row].length; col++) {
			if (grid[row][col] == 1) {
				island++;
				floodFill(row, col, grid);
			}
		}
	}

	return island;
};

const floodFill = (row, col, grid) => {
	const directions = [
		[0, -1],
		[0, 1],
		[-1, 0],
		[1, 0],
	];

	grid[row][col] = "0";

	const queue = [[row, col]];

	while (queue.length) {
		const [currRow, currCol] = queue.shift();

		for (const [deltaRow, deltaCol] of directions) {
			const nextRow = currRow + deltaRow;
			const nextCol = currCol + deltaCol;

			if (
				nextRow < 0 ||
				nextRow >= grid.length ||
				nextCol < 0 ||
				nextCol >= grid[row].length
			) {
				continue;
			}

			if (grid[nextRow][nextCol] == 1) {
				grid[nextRow][nextCol] = "0";
				queue.push([nextRow, nextCol]);
			}
		}
	}
};
```

## 463. Island Perimeter

```javascript
const islandPerimeter = grid => {
	const directions = [
		[0, -1],
		[-1, 0],
		[1, 0],
		[0, 1],
	];
	const queue = [];
	let perimeter = 0;
	const visited = new Set();
	outer: for (let row = 0; row < grid.length; row++) {
		for (let col = 0; col < grid[row].length; col++) {
			if (grid[row][col] === 1) {
				queue.push([row, col]);
				visited.add(`${row}-${col}`);
				break outer;
			}
		}
	}

	while (queue.length) {
		const [currRow, currCol] = queue.shift();
		perimeter += 4;
		for (const [deltaRow, deltaCol] of directions) {
			const nextRow = currRow + deltaRow;
			const nextCol = currCol + deltaCol;

			if (nextRow < 0 || nextRow >= grid.length || nextCol < 0 || nextCol >= grid[currRow]) {
				continue;
			}

			if (grid[nextRow][nextCol] === 1) {
				if (!visited.has(`${nextRow}-${nextCol}`)) {
					queue.push([nextRow, nextCol]);
					visited.add(`${nextRow}-${nextCol}`);
				}
				perimeter -= 1;
			}
		}
	}
	return perimeter;
};
```

## 637. Average of Levels in Binary Tree

```javascript
const averageOfLevels = root => {
	const queue = [root];
	const averages = [];
	while (queue.length) {
		const size = queue.length;
		let val = 0;
		for (let i = 0; i < size; i++) {
			const curr = queue.shift();
			if (curr.left) {
				queue.push(curr.left);
			}

			if (curr.right) {
				queue.push(curr.right);
			}

			val += curr.val;
		}

		averages.push(val / size);
	}

	return averages;
};
```

## 323. Number of Connected Components in an Undirected Graph

```javascript
const countComponents = (n, edges) => {
	let components = 0;
	const visited = new Array(n).fill(false);
	const adjacencyList = buildGraph(edges);

	for (let node = 0; node < n; node++) {
		if (visited[node] === false) {
			visited[node] = true;
			components++;
			bfs(visited, adjacencyList, node);
		}
	}

	return components;
};

const buildGraph = edges => {
	const adjacencyList = {};
	for (const [a, b] of edges) {
		if (adjacencyList[a] === undefined) {
			adjacencyList[a] = [];
		}

		if (adjacencyList[b] === undefined) {
			adjacencyList[b] = [];
		}

		adjacencyList[a].push(b);
		adjacencyList[b].push(a);
	}

	return adjacencyList;
};

const bfs = (visited, adjacencyList, node) => {
	const queue = [node];

	while (queue.length) {
		const curr = queue.shift();

		if (adjacencyList[curr] === undefined) {
			continue;
		}

		for (const neighbor of adjacencyList[curr]) {
			if (visited[neighbor] === false) {
				visited[neighbor] = true;
				queue.push(neighbor);
			}
		}
	}
};
```

## 690. Employee Importance

```javascript
const GetImportance = (employees, id) => {
	const adjacencyList = {};
	const importanceMap = {};

	for (const { id, importance, subordinates } of employees) {
		adjacencyList[id] = subordinates;
		importanceMap[id] = importance;
	}

	const queue = [id];
	let totalImportance = 0;

	while (queue.length) {
		const curr = queue.shift();
		const importance = importanceMap[curr];
		totalImportance += importance;

		const neighbors = adjacencyList[curr];
		queue.push(...neighbors);
	}

	return totalImportance;
};
```

## 783. Minimum Distance Between BST Nodes

```javascript
const minDiffInBST = root => {
	if (root === null) return 0;
	const queue = [root];
	let prev = [];
	let result = Infinity;

	while (queue.length) {
		const curr = queue.shift();
		for (const prevNums of prev) {
			result = Math.min(result, Math.abs(curr.val - prevNums));
		}
		prev.push(curr.val);
		if (prev.length) {
			if (curr.left) queue.push(curr.left);
			if (curr.right) queue.push(curr.right);
		}
	}

	return result;
};
```
