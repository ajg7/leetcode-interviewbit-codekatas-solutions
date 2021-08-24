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

```csharp
public class Solution {
    public int IslandPerimeter(int[][] grid) {
        int perimeter = 0;
        int[,] directions = { { 0, -1 }, { 0, 1 }, { -1, 0 }, { 1, 0 } };

        for (int row = 0; row < grid.Length; row++) {
            for (int col = 0; col < grid[row].Length; col++) {
                if (grid[row][col] == 1) {
                    perimeter += 4;

                    for (int i = 0; i < directions.GetLength(0); i++) {
                        int deltaRow = directions[i, 0];
                        int deltaCol = directions[i, 1];

                        int nextRow = row + deltaRow;
                        int nextCol = col + deltaCol;

                        if (nextRow < 0 || nextRow >= grid.Length || nextCol < 0 || nextCol >= grid[row].Length) {
                            continue;
                        }

                        if (grid[nextRow][nextCol] == 1) {
                            perimeter -= 1;
                        }
                    }
                }
            }
        }

        return perimeter;
    }
}
```
