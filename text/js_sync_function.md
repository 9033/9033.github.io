---
title: js_sync_function
---
<link rel="stylesheet" href="/global.css">

# 자바스크립트에서 프로미스, 동기함수의 사용.
ok변수의 값을 변경해서 어느 부분이 실행이 되는지 볼수 있다. true일 경우에는 resolve부분이, false일 경우에는 reject부분이 실행된다.  
프로미스와 프로미스 함수의 차이. `async, await`를 사용할때는 프로미스 함수를 사용해야 한다.  
`.then(resolved,rejected)`와 `.then(resolved).catch(rejected)`는 동작이 같다.  
어떻게 동작하는지 알았으면 ctrl+c, ctrl+v를 이용하여 복붇해서 쓰면된다.  
```js
var ok=true;

let promise = new Promise((resolve,reject)=>{
    console.log('promise construction');
    (ok)?resolve('ok'):reject('fail');
});

promise.then((value)=>{
    //resolve
    console.log(value);
},(reason)=>{
    //reject
    console.log(reason);
});

promise.then((value)=>{
    //resolve
    console.log(value);
}).catch((reason)=>{
    //reject
    console.log(reason);
});

let promiseFunction = ()=>promise;
async function af(){
    try{
        //resolve
        console.log(await promiseFunction());
    }catch(e){
        //reject
        console.error(e);
    }    
};
af();
```
## promise function를 async 함수에서 사용.
프로미스를 생성해서 리턴하는 함수를 이용한다.  
동작은 위와 같다.  
```js
function promiseFunction(){
    return new Promise((resolve,reject)=>{
        console.log('promise construction');
        (true)?resolve('ok'):reject('fail');
    });
}
async function af(){
    try{
        //resolve
        var r=await promiseFunction();
        console.log(r);
    }catch(e){
        //reject
        console.error(e);
    }    
};
af();
```