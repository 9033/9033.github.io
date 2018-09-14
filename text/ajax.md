---
title: ajax
---
<style >body {background-color:lightblue;}</style>
# ajax
* XMLHttpRequest
    ```js
    function mxhr(method,url,send,headers={}){
        let xhr=new XMLHttpRequest();
        xhr.open(method,url);        
        for(let v in headers){            
            xhr.setRequestHeader(v,headers[v]);
        }
        xhr.send(send);
    }
    ```
* use mxhr
    ```js
    mxhr('POST','/addr','data',{'Content-Type': 'application/json'});
    ```
## promise
* XMLHttpRequest
    ```js
    function mxhr(method,url,send,headers={}){
        return new Promise((res,rej)=>{
            let xhr=new XMLHttpRequest();
            xhr.onload=()=>(xhr.status==200||xhr.status==201)?res(xhr):rej(xhr);
            xhr.onerror=()=>rej(xhr);
            xhr.open(method,url);        
            for(let v in headers){            
                xhr.setRequestHeader(v,headers[v]);
            }
            xhr.send(send);
        });
    }
    ```
* fetch (simple)
    ```js
    function mxhr(method,url,send,headers={}){
        return fetch(url,{
            method,
            headers,
            body:send,
        })
        .then(res=>res);
    }
    ```
* fetch
    ```js
    function mxhr(method,url,send,headers={}){
        let head=new Headers(headers);
        let reqop={
            method,
            headers:head,
            body:send,
        };    
        let nreq=new Request(url,reqop);    
        return fetch(nreq)
        .then(res=>res);
    }
    ```
* use mxhr
    ```js
    mxhr('POST','/addr','data',{'Content-Type': 'application/json'})
        .then((res)=>{
            console.log(res.responseText);
        })
        .catch((rej)=>{
            console.error(rej.responseText);
        });
    ```
