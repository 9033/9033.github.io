---
title: js-currying-func
---
<meta name="keywords" content="JavaScript, Nodejs">
<link rel="stylesheet" href="/global.css">

# 자바스크립트 커링 함수 활용
## 기본 형식
```js
const a = [1,3,8];
a.forEach((val,idx) => { console.log(val,idx) });
a.forEach((val,idx) => { console.error(val,idx) });

const log = logger => (val,idx) => { logger(val,idx) };
a.forEach(log(console.log))
a.forEach(log(console.error))
```
## express 라우터에 응용
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
  if( !Array.isArray(able_options) || (req.query.option && able_options.includes(req.query.option)) ){
    return options[req.query.option]
  }
  return false
}
// currying function
const curry_func = (able_options) =>{
  if( !Array.isArray(able_options) || !able_options.every(option=>Object.keys(options).includes(option)) ){
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
  const ret = func(req, ['R','SSR'])
  console.log(ret);
  res.end()
});
// another express router
const fn = curry_func(['R','SSR']) // run at starting server
router.get('/value2',
async (req, res, next)=>{
  const ret = fn(req)
  console.log(ret);
  res.end()
});
```
커링함수는 함수를 리턴한다. 라우터에서는 리턴한 함수를 실행한다.  
다시 보면 커링 함수는 함수를 리턴하는 함수가 실행된다. 언제? 바로 서버가 실행될때 실행된다.  
그래서 커링 함수가 실행이 시작한 후 함수를 리턴하기 전에 유용한 코드를 집어 넣었다.  
바로 `able_options`을 확인하는 코드를 넣어서 서버가 실행될때 오류가 있으면 오류 메시지를 출력하고 실행을 멈추게 했다.  
만일 커링함수를 사용하지 않으면 `able_options`에 대한 오류는 라우터가 호출했을때 나온다.  
그러면 편안히 있다가 급하게 서버에 오류를 찾어서 수정할 것이다.  
하지만 커링함수를 이용하면 실행할때 오류를 발견하기 위한 용도로도 쓸 수 있다.  
