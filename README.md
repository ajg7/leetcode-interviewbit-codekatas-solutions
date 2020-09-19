# code_katas
My solutions for code katas on codewars.com

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
  const numTest = Math.sqrt(num)
  if(numTest % 2 === 0 || numTest % 2 === 1 && num >= 0) {
    return true
  } else {
    return false
  }
}

isSquare(36);
```
