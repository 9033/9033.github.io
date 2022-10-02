---
title: express modules
---
<link rel="stylesheet" href="/global.css">

# 사용량 제한
- [express-rate-limit](https://www.npmjs.com/package/express-rate-limit) : each ip, limit scope are below.\
    all requests
    ```js
    app.use(limiter);
    ```
    a api
    ```js
    app.use("/api/", apiLimiter);
    ```
    a method, a route
    ```js
    app.post("/create-account", createAccountLimiter, function(req, res) {
      //...
    });
    ```
    

- [express-limiter](https://www.npmjs.com/package/express-limiter)\
    each ip, each user.

- my delay middleware
    ```js
    // javascript, node.js, express
    const busloc_ipaddr=new Set();
    const buslocdelay=(req,res,next)=>{
        if(!busloc_ipaddr.has(req.ip)){
            busloc_ipaddr.add(req.ip);
            setTimeout((ip)=>{
                next();
                busloc_ipaddr.delete(ip);
            },500, req.ip);
        }
    };
    ```
