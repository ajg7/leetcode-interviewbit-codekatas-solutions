## Graphs

### 997. Find the Town Judge

```javascript
const findJudge = (N, trust) => {
	const map = {};

	for (const [person1, person2] of trust) {
		if (!map[person1]) map[person1] = { in: 0, out: 0 };
		if (!map[person2]) map[person2] = { in: 0, out: 0 };

		map[person1].out++;
		map[person2].in++;
	}

	for (const [person, degrees] of Object.entries(map)) {
		if (degrees.in === N - 1 && degrees.out === 0) {
			return +person;
		}
	}

	return -1;
};
```

## 463. Island Perimeter

```javascript
const islandPerimeter = grid => {
	const directions = [
		[0, -1],
		[0, 1],
		[-1, 0],
		[1, 0],
	];
	let perimeter = 0;
	for (let row = 0; row < grid.length; row++) {
		for (let col = 0; col < grid[row].length; col++) {
			if (grid[row][col] === 1) {
				perimeter += 4;

				for ([deltaRow, deltaCol] of directions) {
					const nextRow = row + deltaRow;
					const nextCol = col + deltaCol;

					if (
						nextRow < 0 ||
						nextRow >= grid.length ||
						nextCol < 0 ||
						nextCol >= grid[row].length
					) {
						continue;
					}

					if (grid[nextRow][nextCol] === 1) {
						perimeter -= 1;
					}
				}
			}
		}
	}
	return perimeter;
};
```
