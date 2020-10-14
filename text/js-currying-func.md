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
