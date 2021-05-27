## Intervals

### 252. Meeting Rooms

```typescript
const canAttendMeetings = (intervals: number[][]): boolean => {
	const arr = intervals.sort((a, b) => a[0] - b[0]);

	for (let i = 1; i < arr.length; i++) {
		if (arr[i][0] < arr[i - 1][1]) return false;
	}
	return true;
};
```
