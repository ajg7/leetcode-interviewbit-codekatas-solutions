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
## 1469. Find All The Lonely Nodes
```javascript
const getLonelyNodes = (root) => {
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