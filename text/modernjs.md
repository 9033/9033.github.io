# Symbol
같은 명칭을 쓰면서도 안겹치게 하는 효과를 가짐.  
```js
var k=[];
k.haha=function(){
    console.log('haha');
}
k.haha();
k.haha=function(){//overwrite
    console.log('haha 2');
}
k.haha();

var f1=Symbol('haha');
k[f1]=function(){
    console.log('Symbol haha');
}
k[f1]();
var f2=Symbol('haha');
k[f2]=function(){
    console.log('Symbol haha 2');
}
k[f2]();
k[f1]();
k.haha();
```

# label
중첩된 루프를 한번에 나올 수 있다.  
```js
loops : for(let i=0;i<10;i++){
    for(let j=0;j<10;j++){
        console.log(i,j);
        if(j==5)break loops;
    }
}
```

# ... arg
인자들을 넘길수 있다.  
```js
( (a,...x) => console.log(a,...x) )("a","b","c");
```
# iterator
```js
let l=[1,2,3];
let i=l[Symbol.iterator]();
while(!0){
    let t=i.next();
    console.log(t);
    if( t.done )break;//끝인가?
}
```

# for/of
for/in과 비교해보면 값을 바로 조회가능.  
```js
let object=[1,2,3];
for(let value of object)console.log(value);
for(let index in object)console.log(object[index]);
```

# generator
```js
function *g(){
    yield 1;
    yield 2;
    yield 3;    
}
let i=g();
console.log(i.next());
console.log(i.next());
console.log(i.next());
console.log(i.next());//done == true
for(let v of g())console.log(v);
```
