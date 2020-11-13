My solutions for code katas on leetcode.com & codewars.com

# Leetcode

## Merge Sorted Array
```javascript
const merge = (nums1, m, nums2, n) => {
    let first = m - 1;
    let second = n  -1;
    
    for (let i = m + n - 1; i >= 0; i--) {
        if (second < 0) break;
        if (nums1[first] > nums2[second]) {
            nums1[i] = nums1[first];
            first--;
        } else {
            nums1[i] = nums2[second];
            second--;
        }
    }
};
```

## Duplicate Zeros
```javascript
const duplicateZeros = arr => {
    for (let i = 0; i < arr.length; i++) {
        if (!arr[i]) {
            arr.splice(i, 0, 0);
            i++
            arr.pop();
        }  
    }
};
```

# Code Katas

## Unique In Order
```javascript
var uniqueInOrder=function(iterable){
  const result = []
  let prevChar = ''
  
  for (const char of iterable) {
    if (prevChar !== char) {
      prevChar = char
      result.push(char)
    }
  }
  
  return result
}
```

## A Square of Squares
```javascript
const isSquare = num => {
  const rootNum = Math.sqrt(num)
  if(rootNum % 2 === 0 || rootNum % 2 === 1 && num >= 0) {
    return true
  } else {
    return false
  }
}
```

## Training on Dubstep
```javascript
const songDecoder = dubStepSong => {
    const splitArray = dubStepSong.split("WUB");
    const filteredArray = splitArray.filter(character => {
      if(character !== "") {
        return true;
      } else {
        return false;
      }
    })
    return filteredArray.join(" ")
}

console.log(songDecoder("WUBWEWUBAREWUBWUBTHEWUBCHAMPIONSWUBMYWUBFRIENDWUB"));
```

## Create Phone Number
```javascript
const createPhoneNumber = nums => {
  const phoneNumber = []
  const sectionOne = ["(", nums[0], nums[1], nums[2], ")"]
  const sectionTwo = [" ", nums[3], nums[4], nums[5], "-"]
  const sectionThree = [nums[6], nums[7], nums[8], nums[9]]
  return [...sectionOne, ...sectionTwo, ...sectionThree].join("")
}



console.log(createPhoneNumber([6,6,0,8,6,4,4,6,7,8]))
```
## Training on Roman Numerals
```javascript
const solution = (romanNum) => {
  const numerals = {
      M: 1000,
      D: 500,
      C: 100,
      L: 50,
      X: 10,
      V: 5,
      I: 1
    };
  const numbers = romanNum.split("");
  let solution = 0;
  let precedingNumeral;
  for (const ele of numbers) {
    if(precedingNumeral < numerals[ele]) {
        solution += numerals[ele] - 2
    } else {
      solution += numerals[ele]
    }
    precedingNumeral = numerals[ele]
  }
  return solution
}

solution("IX")
```

## Convert String to Camel Case
```javascript
const toCamelCase = str => {
  const splitStr = str.split("");
  const result = [];
  let underscorePresent = false;
  	for(const ele of splitStr) {
	    if(ele === "_" || ele === "-") {
		result.unshift()
		underscorePresent = true;
	    } else {
		if(underscorePresent) {
		    result.push(ele.toUpperCase())
		    underscorePresent = false;
		} else {
		    result.push(ele)
		  }
	      }
	    }
   return result.join("")
}

console.log(toCamelCase("the_camel_and_the_snake"))
```
### Convert Camel Case to Snake Case
- This is my own original challenge
```javascript
const toSnakeCase = str => {
  const splitStr = str.split("");
  const result = [];
  for(const ele of splitStr) {
      if(ele === ele.toUpperCase()) {
         result.push("_", ele.toLowerCase())
      } else {
	result.push(ele)
        }
      }
   return result.join("")
}

console.log(toSnakeCase("theCamelAndTheSnake"))
```

