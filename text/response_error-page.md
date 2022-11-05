---
title: reponse_error-page
---
<link rel="stylesheet" href="/global.css">

# 에러 페이지 응답하기 (AWS)
## 평상시
![](img/aws-server-out-of-service-page-01.svg)  
EC2는 HTML 페이지랑 DB에서 데이터를 가공해서 API형태로 응답한다.  
로드벨런서의 역할은 요청하는 경로를 보고 EC2나 Lambda로 분배를 한다.  
여기서는 EC2가 멈추었을때 이메일로 알람을 보내는것 외에 별다른 설정을 하지 않은 상태다.  

이런 경우에 EC2가 멈추면 응답을 할 수 없다. HTML페이지를 응답해서 현재 점검중이라는 페이지를 띄워주어야 하는데 그게 불가능 하기 떄문이다.  

## 서버 점검시
![](img/aws-server-out-of-service-page-02.svg)  
Lambda함수를 추가한다. 점검중이라는 페이지를 리턴하게 한다. 람다로 리턴을 하면 DB의 데이터를 참고하거나 워드프레스같은 외부에서 만든 페이지를 상황에 맞게 가지고 와서 띄울 수 있다.  

로드벨런서는 EC2가 오류가 있으면 람다 함수로 요청을 보내고 결과를 응답한다. 로드벨런서는 평상시 EC2가 동작하는지 health check를 하기 때문에 EC2가 오류가 있는지 알 수 있다.

추가적으로 Cloudwatch를 이용해서 EC2가 오류가 있어서 멈추면 이메일등으로 알람을 보내는 것도 가능하다.  

## 기타
MariaDB에도 Database Proxy를 지원되기 때문에 프록시를 이용해서 Lambda 함수에서 DB에 접속하면 좋을 것이다.  
