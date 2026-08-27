Tags: [[_JavaScript]] [[__Programming_languages]]
#JavaScript #ProgrammingLanguages 

# Introduction
Some runtimes, e.g. Node.js, allows for caching modules, that means that when we import objects from the same module in multiple scripts, each script gets the same object.
# Examples
## Counter
For example:
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

`b.js`
```javascript
const counter = require('./counter')

counter.value++

console.log(counter.value)
```

`main.js`
```javascript
require('./a')
require('./b')
```

The output of the `main.js` is:
```
1
2
```

So in both modules `a.js` and `b.js` we work with the same `counter` object, not with two separate `coutner` objects.
## Connecting to a database
We can also connect to a database in one module and use this connection in other modules:
`module1.js`
```javascript
const mongoose = require('mongoose')

async function load_data(...):
	data = await collection.find(...)
	return data
```

`main.js`
```javascript
const mongoose = require('mongoose')
await mongoose.connect(`mongodb://${MONGO_DNS}/${MONGO_DATABASE}`)

const module = require('./modules/module1')
const data = module.load_data()
```

It is enough to connect to MongoDB in the `main.js`, we don't need to do this in the `module1.js` as well.