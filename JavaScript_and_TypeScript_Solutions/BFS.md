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
    
    while(queue.length !== 0) {
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