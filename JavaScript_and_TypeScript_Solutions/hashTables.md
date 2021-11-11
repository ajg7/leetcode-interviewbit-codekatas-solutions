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

```typescript
const numJewelsInStones = (jewels: string, stones: string): number => {
	const jewelSet: Set<string> = new Set(jewels);
	let count: number = 0;

	for (const stone of stones) {
		if (jewelSet.has(stone)) count++;
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
	// Define a constructor function and set some values as object properties to keep our data persistent between invocations
	constructor(n) {
		this.pointer = 0;
		// this will create an array of length (n) and set all values to 'undefined'
		this.list = [];
	}

	insert(id, value) {
		// will be used to store values that pass the condition and to be returned
		let chunk = [];
		// since array indices start from zero and id in this problem from 1 we need to decrement it
		this.list[id - 1] = value;
		// every time we insert a value we have to look if there is a value at the index (pointer) that should be returned
		// if there is any we copy it and then iterate to the next element until the condition is no longer true
		while (this.list[this.pointer]) {
			chunk.push(this.list[this.pointer]);
			this.pointer++;
		}
		return chunk;
	}
}
```

### 1365. How Many Numbers Are Smaller Than the Current Number

```javascript
const smallerNumbersThanCurrent = nums => {
	let result = [];

	for (let i = 0; i < nums.length; i++) {
		let count = 0;
		let j = 0;

		while (j < nums.length) {
			if (nums[i] > nums[j]) {
				count++;
				j++;
			} else {
				j++;
			}
		}
		result.push(count);
	}

	return result;
};
```

### 1165. Single-Row Keyboard

```javascript
const calculateTime = (keyboard, word) => {
	const map = new Map(keyboard.split("").map((letter, index) => [letter, index]));
	let count = 0;
	let curr = 0;

	for (const letter of word) {
		const temp = map.get(letter);
		count += Math.abs(curr - temp);
		curr = temp;
	}

	return count;
};
```

### 760. Find Anagram Mappings

```javascript
const anagramMappings = (nums1, nums2) => {
	const map = new Map();
	let result = [];

	for (let i = 0; i < nums2.length; i++) {
		map.set(nums2[i], i);
	}

	for (const num of nums1) {
		const anagramIndex = map.get(num);
		result.push(anagramIndex);
	}

	return result;
};
```

### 1832. Check if the Sentence Is Pangram

```javascript
const checkIfPangram = sentence => {
	return new Set(sentence.split("")).size === 26;
};
```

### 1684. Count the Number of Consistent Strings

```javascript
const countConsistentStrings = (allowed, words) => {
	const chars = new Set(allowed);
	return words.filter(word => {
		return [...word].every(char => {
			return chars.has(char);
		});
	}).length;
};
```

### 1941. Check if All Characters Have Equal Number of Occurrences

```javascript
const areOccurrencesEqual = s => {
	const map = {};

	for (const letter of s) {
		if (map[letter]) {
			map[letter] += 1;
		} else {
			map[letter] = 1;
		}
	}

	const set = new Set(Object.values(map));
	return set.size === 1;
};
```

### 1748. Sum of Unique Elements

```javascript
const sumOfUnique = nums => {
	const map = {};
	let result = 0;

	for (const num of nums) {
		if (map[num]) {
			map[num] += 1;
		} else {
			map[num] = 1;
		}
	}

	for (const [key, value] of Object.entries(map)) {
		if (value === 1) {
			result += +key;
		}
	}

	return result;
};
```

### 1207. Unique Number of Occurrences

```javascript
const uniqueOccurrences = arr => {
	const map = new Map();

	for (const num of arr) {
		if (map.has(num)) {
			const count = map.get(num) + 1;
			map.set(num, count);
		} else {
			map.set(num, 1);
		}
	}

	return new Set(map.values()).size === map.size;
};
```

### 242. Valid Anagrams

```javascript
const isAnagram = (s, t) => {
	const map = {};

	for (const letter of s) {
		map[letter] = 1 + (map[letter] || 0);
	}

	for (const letter of t) {
		map[letter] = (map[letter] || 0) - 1;
	}

	for (const value of Object.values(map)) {
		if (value !== 0) {
			return false;
		}
	}

	return true;
};
```

```javascript
const isAnagram = (s, t) => {
	const counts = new Array(26).fill(0);

	for (const letter of s) {
		const index = letter.charCodeAt(0) - "a".charCodeAt(0);
		counts[index]++;
	}

	for (const letter of t) {
		const index = letter.charCodeAt(0) - "a".charCodeAt(0);
		counts[index]--;
	}

	for (const count of counts) {
		if (count !== 0) {
			return false;
		}
	}

	return true;
};
```

### 804. Unique Morse Code Words

```javascript
const uniqueMorseRepresentations = words => {
	const dict = [
		".-",
		"-...",
		"-.-.",
		"-..",
		".",
		"..-.",
		"--.",
		"....",
		"..",
		".---",
		"-.-",
		".-..",
		"--",
		"-.",
		"---",
		".--.",
		"--.-",
		".-.",
		"...",
		"-",
		"..-",
		"...-",
		".--",
		"-..-",
		"-.--",
		"--..",
	];

	const translatedWords = words.map(word => {
		return translate(word, dict);
	});

	return countUniqueElements(translatedWords);
};

const translate = (word, dict) => {
	const result = [];
	for (const letter of word) {
		const lowerCaseLetter = letter.toLowerCase();
		const index = indexForChar(lowerCaseLetter);
		const morseCode = dict[index];
		result.push(morseCode);
	}
	return result.join("");
};

const countUniqueElements = values => {
	const set = new Set();

	for (const value of values) {
		set.add(value);
	}
	return set.size;
};

const indexForChar = letter => letter.charCodeAt(0) - "a".charCodeAt(0);
```

### 1436. Destination City

```javascript
// Time-Complexity: O(n)
// Space-Complexity: O(n)
const destCity = paths => {
	const map = new Map();

	for (const [startCity, endCity] of paths) {
		map.set(startCity, endCity);
	}

	for (const [key, value] of map.entries()) {
		if (!map.has(value)) return value;
	}
};
```

### 2032. Two Out of Three

```javascript
// Time-Complexity: O(n)
// Space-Complexity: O(1)
const twoOutOfThree = (nums1, nums2, nums3) => {
	const arr1 = new Array(101).fill(false);
	const arr2 = new Array(101).fill(false);
	const arr3 = new Array(101).fill(false);

	for (const num of nums1) {
		arr1[num] = true;
	}

	for (const num of nums2) {
		arr2[num] = true;
	}

	for (const num of nums3) {
		arr3[num] = true;
	}

	const map = new Array(101).fill(0);
	const result = [];

	for (let num = 1; num <= 100; num++) {
		if (arr1[num]) {
			map[num]++;
		}

		if (arr2[num]) {
			map[num]++;
		}

		if (arr3[num]) {
			map[num]++;
		}
	}

	for (let num = 0; num < map.length; num++) {
		if (map[num] > 1) {
			result.push(num);
		}
	}

	return result;
};
```

### 1394. Find Lucky Integer in an Array

```javascript
// Time-Complexity: O(n)
// Space-Complexity: O(1)
const findLucky = arr => {
	const map = new Array(501).fill(0);
	let luckyNum = 0;

	for (const num of arr) {
		map[num]++;
	}

	for (let num = 1; num <= 500; num++) {
		if (map[num] == num) {
			luckyNum = Math.max(luckyNum, num);
		}
	}

	return luckyNum || -1;
};
```

### 575. Distribute Candies

```javascript
// Time-Complexity: O(n)
// Space-Complexity: O(n)
const distributeCandies = candyType => {
	const candies = new Set(candyType);
	const maxAmount = candyType.length / 2;

	return Math.min(candies.size, maxAmount);
};
```

### 13. Roman to Integer

```javascript
// Time-Complexity: O(n)
// Space-Complexity: O(1)
const romanToInt = s => {
	const legend = {
		I: 1,
		V: 5,
		X: 10,
		L: 50,
		C: 100,
		D: 500,
		M: 1000,
	};

	let sum = 0;

	for (let i = 0; i < s.length; i++) {
		if (legend[s[i]] < legend[s[i + 1]]) {
			sum -= legend[s[i]];
		} else {
			sum += legend[s[i]];
		}
	}

	return sum;
};
```
