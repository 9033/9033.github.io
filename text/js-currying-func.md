---
title: js-currying-func
---
<style >body {background-color:lightblue;}</style>

# 자바스크립트 커링 함수 활용

```js
const a = [1,3,8];
a.forEach((val,idx) => { console.log(val,idx) });
a.forEach((val,idx) => { console.error(val,idx) });

const log = logger => (val,idx) => { logger(val,idx) };
a.forEach(log(console.log))
a.forEach(log(console.error))
```

```js
// preseted values
const options = {
     R:   10,
    SR:  100,
   SSR: 1000,
  USSR:10000,
};
// function
const func = (req, able_options) => {
  if( Array.isarray(able_options) && req.query.option && able_options.includes(req.query.option) ){
    return options[req.query.option]
  }
  return false
}
// currying function
const curry_func = (able_options) =>{
  // able_options.every(option=>!!options[option])
  if( Array.isarray(able_options) && able_options.every(option=>Object.keys(options).includes(option)) ){
    throw Error('error')
  }
  return (req) => {
    if( req.query.option && able_options.includes(req.query.option) ){
      return options[req.query.option]
    }
    return false
  }
}
// a express router
router.get('/value',
async (req, res, next)=>{
  const ret = func(req, ['SR','SSR'])
  res.end()
}
// another express router
router.get('/value2',
async (req, res, next)=>{
  const ret = func(['SR','SSR'])(req)
  res.end()
}
```
