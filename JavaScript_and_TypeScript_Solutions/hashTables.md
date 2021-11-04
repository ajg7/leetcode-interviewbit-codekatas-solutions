## Hash Tables

### 1. Two Sum

```javascript
const twoSum = (nums, target) => {
	const map = new Map();
	for (let i = 0; i < nums.length; i++) {
		let complement = target - nums[i];
		if (map.has(complement)) {
			return new Array(map.get(complement), i);
		}
		map.set(nums[i], i);
	}
	return -1;
};

const twoSum = (nums, target) => {
	const dict = {};

	for (let i = 0; i < nums.length; i++) {
		const candidate = target - nums[i];

		if (dict[candidate] !== undefined) {
			return [dict[candidate], i];
		}

		dict[nums[i]] = i;
	}

	return [];
};
```

### 1512. Number of Good Pairs

```javascript
const numIdenticalPairs = nums => {
	const map = {};
	let count = 0;

	for (const num of nums) {
		if (map[num]) {
			count += map[num];
			map[num] += 1;
		} else {
			map[num] = 1;
		}
	}

	return count;
};
```

### 771. Jewels and Stones

```javascript
const numJewelsInStones = (jewels, stones) => {
	const jewelSet = new Set(jewels);
	let count = 0;

	for (const stone of stones) {
		if (jewelSet.has(stone)) {
			count++;
		}
	}
	return count;
};
```

#### Alternative Way of doing 771. Jewels and Stones

```javascript
const numJewelsInStones = (jewels, stones) => {
	const jewelSet = new Set(jewels);
	return stones.split("").reduce((count, stone) => count + jewels.has(stone), 0);
};
```

### 1656. Design an Ordered Stream

```javascript
class OrderedStream {
  // Define a construction function and set some values as object properties to keep our data persistent between invocations
  constructor(n) {
    this.pointer = 0
    // this will create an array of length (n) and set all values to 'undefined'
    this.list = []
  }

  insert(id, value) {
    // will be used to store values that pass the condition and to be returned
    let chunk = []
    // since array indices start from zero and id in this problem from 1 we need to decrement it
    this.list[id - 1] = value
    // every time we insert a value we have to look if there is a value at the index (pointer) that should be returned
    // if there is any we copy it and then iterate to the next element until the condition is no longer true
    while(this.list[this.pointer]) {
      chunk.push(this.list[this.pointer])
      this.pointer++
    }
    return chunk
  }
}
```
