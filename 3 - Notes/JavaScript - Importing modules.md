Tags: [[_JavaScript]] [[__Programming_languages]]
#JavaScript #ProgrammingLanguages 

# Introduction
In JavaScript, when we import a module, we execute its entire code and return the exported objects, for example:
`counter.js`
```javascript
const counter = {
    value: 0
}

module.exports = counter
```

`a.js`
```javascript
const counter = require('./counter')

counter.value++

console.log(counter.value)
```

`main.js`
```javascript
require('./a')
```

The output of the `main.js` is:
```
1
```
# Related topics
1. [[JavaScript - Caching modules]]