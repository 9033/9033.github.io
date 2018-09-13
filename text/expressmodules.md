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
