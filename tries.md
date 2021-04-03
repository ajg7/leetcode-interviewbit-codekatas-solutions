## Tries

### 208. Implement Trie (Prefix Tree)

```javascript
class TrieNode {
	constructor(key) {
		this.key = key;
		this.children = {};
		this.isEnd = false;
	}
}

class Trie {
	constructor(words) {
		this.root = new TrieNode();
	}

	insert(word) {
		let node = this.root;
		for (const char of word) {
			if (!node.children[char]) {
				node.children[char] = new TrieNode(char);
			}
			node = node.children[char];
		}
		node.isEnd = true;
	}

	search(word) {
		let currentNode = this.root;
		for (const char of word) {
			if (!currentNode.children[char]) return false;
			currentNode = currentNode.children[char];
		}

		return currentNode.isEnd;
	}

	startsWith(prefix) {
		let currentNode = this.root;
		for (const char of prefix) {
			if (!currentNode.children[char]) return false;
			currentNode = currentNode.children[char];
		}
		return true;
	}
}
```

### 720. Longest Word in the Dictionary

```javascript
class TrieNode {
	constructor(key) {
		this.key = key;
		this.children = {};
		this.word = null;
	}
}

class Trie {
	constructor(words) {
		this.root = new TrieNode();

		for (const word of words) {
			this.insert(word);
		}
	}

	insert(word) {
		let node = this.root;
		for (const char of word) {
			if (node.children[char] === undefined) {
				node.children[char] = new TrieNode(char);
			}

			node = node.children[char];
		}

		node.word = word;
	}

	longestWord() {
		const dfs = node => {
			for (const child of Object.values(node.children)) {
				if (child.word === null) continue;
				dfs(child);
			}

			if (node.word === null) return;

			if (result.length < node.word.length) {
				result = node.word;
			} else if (result.length === node.word.length && result > node.word) {
				result = node.word;
			}

			return true;
		};

		let result = "";
		dfs(this.root);
		return result;
	}
}

const longestWord = words => {
	const trie = new Trie(words);
	return trie.longestWord();
};
```
