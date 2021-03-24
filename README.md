## babel-plugin-pure-calls-annotation

[![NPM](https://img.shields.io/npm/v/babel-plugin-pure-calls-annotation.svg?style=flat-square)](https://npmjs.org/package/babel-plugin-pure-calls-annotation)
[![Dependencies](https://img.shields.io/david/morlay/babel-plugin-pure-calls-annotation.svg?style=flat-square)](https://david-dm.org/morlay/babel-plugin-pure-calls-annotation)
[![License](https://img.shields.io/npm/l/babel-plugin-pure-calls-annotation.svg?style=flat-square)](https://npmjs.org/package/babel-plugin-pure-calls-annotation)

Automated annotate **`/*#__PURE__*/`** to call expression which in **variable declarator**, 
**assignment expression** and **arguments of call expression**

### Purpose

help to annotate **`/*#__PURE__*/`** to drop dead code in [Webpack](https://github.com/webpack/webpack) 
for uglyfiy and tree shaking


Will transform

```typescript
export const call = (s) => {
  return "call" + s
}

export const stringA = call("a")
export const stringB = (() => call("b"))()
```

to

```typescript
export const call = (s) => {
  return "call" + s
}

export const stringA = /*#__PURE__*/call("a")
export const stringB = /*#__PURE__*/(() => call("b"))()
```

Notice:

code like below will not be pure call

```typescript
const a = setInterval(() => { 
  console.log(a) 
}, 1000)
```
