---
title: openssl
---
# openssl
<style >body {background-color:lightblue;}</style>
1. issue self-signed certification.
```bash
openssl genrsa -out rootCA.key 2048
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.crt
```
2. issue certification signed by rootCA.
```bash
openssl genrsa -out device.key 2048
openssl req -new -key device.key -out device.csr -config req.conf 
openssl x509 -req -in device.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out device.crt -days 500 -sha256 -extensions v3_req -extfile req.conf
```
3. 해당 도메인에 https서버를 실행한다.  
4. 위에서 만든 rootCA.crt를 신뢰하는 인증서 목록에 추가하고 접속하면 브라우저에 자물쇠 아이콘이 나온다.  
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
