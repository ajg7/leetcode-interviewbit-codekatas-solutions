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
