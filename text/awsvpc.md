---
title: AWS VPC
---
<link rel="stylesheet" href="/global.css">

# Amazon Virtual Private Cloud
집에서 쓰는 공유기는 내부 포트와 내부 IP주소를 외부 포트와 IP주소로 변환한다. 이것이 NAT(네트워크 주소 변환)이다. 이 개념만 가지고 있으니 AWS(아마존 웹 서비스)에서 제공하는 VPC(Virtual Private Cloud)의 구조가 파악이 되지 않았다. 그래서 도움말을 읽어보면서 정리를 해보았다.  

## VPC와 subnet
+ 하나의 계정에는 여러개의 VPC가 가능.  
+ 하나의 VPC에는 여러개의 subnet이 가능.  
+ 라우팅 테이블은 subnet마다 있음.  
+ 라우팅 테이블에서 '인터넷 게이트웨이'를 추가하면 외부 인터넷과 접속이됨. 즉 subnet마다 외부 인터넷과 연결이 가능할지 안할지 제어가능.  
+ '인터넷 게이트웨이'가 인스턴스에 대응하는 퍼블릭 IP로 통신을 할 수 있게 해줌.  
## 보안
+ 인스턴스는 보안그룹이 그리고 subnet은 ACL이 방화벽의 역할을 함.  
+ VPC에는 기본 ACL이 있음. 그 VPC에 해당하는 subnet에 ACL을 따로 정하지 않으면 기본 ACL로 자동으로 연결됨.  
+ 마찬가지로 VPC에는 기본 '보안 그룹'이 있음. 인스턴스에 보안 그룹을 따로 지정하지 않으면 기본 '보안 그룹'이 지정됨.  
## 기타
+ VPC에서 S3같은 다른 서비스나 다른 VPC로 연결하려면 ['VPC 엔드포인트'](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-endpoints.html)를 이용한다.  
