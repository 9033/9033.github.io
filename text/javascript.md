---
title: javascript
---
<style >body {background-color:lightblue;}</style>
# javascript

func1, func2, func3은 같은 역할을 가진 함수.
```js
func1=function (i){
    if(i)
        return true;
    return false;
};

func2=i=>{ return i?true:false;};

func3=i=>i?true:false;
```

다음과 같은 코드가 있을때
```js
var a=[1,2];
for(let i=0;i<a.length;i++)console.log(a[i]);
for(let k in a)console.log(a[k]);
[].forEach.call(a, v=>{ console.log(v)})
a.map(v=>{ console.log(v)});//return results in a array
a.forEach(v=>{ console.log(v)});
```
수행결과
```console
1
2
1
2
1
2
1
2
1
2
```
추가적으로 여기서 `a.map(v=>{ return v+1});`의 리턴값은 `[2,3]`이다. 함수의 리턴값을 배열로 모아서 리턴함.