---
title: openssl
---
<link rel="stylesheet" href="/global.css">

# openssl로 https서버용 인증서 만들기
https서버의 인증서에 Subject Alternative Name(SAN)에 도메인을 추가해야 브라우저에서 경고가 뜨지 않는다.  
아래와 같은 방법으로 SAN을 포함한 인증서를 발행 하면 된다.
## 순서
1. self-signed 인증서를 발행한다.
    ```bash
    openssl genrsa -out rootCA.key 2048
    openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.crt
    ```
2. 1번의 root인증서로 해당 https서버의 도메인에 대한 인증서를 발행한다.  
발행할때 `-extensions v3_req -extfile req.conf`옵션으로 SAN을 포함시킨다. `-config req.conf`옵션으로 device.csr에 포함이 되어있다고 빼먹으면 안됨.  
req.conf파일의 예제는 밑에 있다.  
    ```bash
    openssl genrsa -out device.key 2048
    openssl req -new -key device.key -out device.csr -config req.conf 
    openssl x509 -req -in device.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out device.crt -days 500 -sha256 -extensions v3_req -extfile req.conf
    ```
3. 해당 도메인에 https서버를 실행한다. 예시는 node.js  
    ```js
    const https=require('https');

    const fs = require('fs');

    const options = {
      key: fs.readFileSync('device.key'),
      cert: fs.readFileSync('device.crt'),
      ca: [ fs.readFileSync('rootCA.crt') ]
    };

    https.createServer(options, (req, res) => {
      res.writeHead(200);
      res.end('https test page\n');
    }).listen(443);
    ```
4. 위에서 만든 rootCA.crt를 신뢰하는 인증서 목록에 추가하고 접속하면 브라우저에 자물쇠 아이콘이 나온다.  

## 참고
- check request file.  
  ```bash
  openssl req -noout -text -in device2.csr
  ```
- 실제로 사용한 req.conf의 예제.  
  ```conf
  [req]
  distinguished_name = req_distinguished_name
  prompt = no
  [ req_distinguished_name ]
  CN = skyred.cloud
  [ v3_req ]
  subjectAltName = @alt_names
  [ alt_names ]
  DNS.1 = *.skyred.cloud
  DNS.2 = skyred.cloud
  ```
- 위키에 SAN에 대한 페이지  
[SAN](https://en.wikipedia.org/wiki/Subject_Alternative_Name)  
- 로컬호스트용 인증서  
[Certificates for localhost](https://letsencrypt.org/docs/certificates-for-localhost)  