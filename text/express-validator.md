---
title: express-validator
---
<link rel="stylesheet" href="/global.css">

# express-validator 활용.
## custom validator
이게 바로 promise의 활용이라는 것입니다 여려분.  
```js
const company_id = null

const custom_validator_user_in_company = (user_id)=>{
  return model.user.findOne({
    where:{
      id:user_id, // PK
      company_id,
    }
  })
  .then(user=>{
    if(!user){
      return Promise.reject('컴퍼니에 속하지 않은 사용자. 혹은 없는 사용자.')
    }
  })
}

const custom_validator_car_in_company = (car_id)=>{
  return model.car.findOne({
    where:{
      id:car_id, // PK
    }
  })
  .then(car=>{
    if(!car){
      return Promise.reject('해당 자동차가 없음.')
    }
    return custom_validator_user_in_company(car.get().user_id)
  })
}
```
car는 user랑 연관.  
user는 company와 연관.  
car가 company와 연관되어 있는지 간접적으로 찾는다.  

```js
async function somename(){
    await custom_validator_car_in_company(car_id)
}
```
Promise.reject가 실행되면 에러를 throw함.  

## cf.  
[custom-validators-sanitizers](https://express-validator.github.io/docs/custom-validators-sanitizers.html)  
