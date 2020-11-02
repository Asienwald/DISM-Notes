

02 Core NodeJS
===




## Table of Contents
- [02 Core NodeJS](#02-core-nodejs)
  * [Table of Contents](#table-of-contents)
  * [Nodejs File-Based Module System](#nodejs-file-based-module-system)
  * [Node Paradigms](#node-paradigms)
    + [Notes](#notes)



Nodejs File-Based Module System
---
- nodejs follows commonjs module specification
    - ea file is own module
    - to export current module, use `module.exports`
    - to import module, use `require()`
        - file referenced with relative path

```javascript=
// in formula.js
multiplyFunct = (x, y) => x * y;
module.exports=multiplyFunct

// in another file
var mulFn = require('./formula');
console.log(mulFn(2,3));

// export multiple files
module.exports = {
    funcName: func,
    funcName2: func2
}

// import specific modules from export
const {funcName, funcName2} from './formula';
```

Node Paradigms
---
- npm - huge collection of libs and modules
- `npm init` to create new `package.json` file
    - `package.json` keeps track of the packages node projs use
    - allows us to avoid checking in node_modules into our version control system (Eg. git) if used
    - run `npm install` if `node_modules` folder missing/corrupted to reinstall required packages
- `require()` to import packages
- export packages - `module.exports`

```javascript=
const john = {
  name: 'john',
  age: 65,
};

module.exports = john;
```

### Notes
- general rule of thumb to use async ver of func if it exists
    - because sync funcs that perform async operations prevent nodejs from performing other tasks while it waits for op to complete



###### tags: `BED` `DISM` `School` `Notes`