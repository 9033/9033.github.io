---
title: git으로 로컬 repo를 서버에 올리고 다른 컴퓨터에서 사용하기
---
<link rel="stylesheet" href="/global.css">

# remote git 명령어  
visual studio code에서 구름 모양이 나오면 안된다. 구름 눌렀다가 수정한거 다 날라간적 있음. 옆에 branch를 다시 확인해서 checkout해야됨.  
밑에 예제에서 브랜치 명인 'remotegit'은 임의로 설정가능.  

## 로컬에 있는 기존 git repo. 를 remote git에 추가
`git remote add remotegit https://.../your_repo.git`  
`git push remotegit`  

## 빈 로컬 폴더에서 remote git에 있는 repo.를 불러오기
`git init`  
`git remote add remotegit https://.../your_repo.git`  
`git pull remotegit`  
`git checkout master`  

## 다른 컴퓨터에서 사용하기 직전
remote git에 있는 갱신된 데이터를 가지고 옴.  
`git pull remotegit`  

## ssl verifycation오류가 나오는 경우
인증서가 신뢰할수 없어서 나오는 오류이다. 일단 git에서 인증서를 확인하지 않게 하려면 다음과 같이 입력한다.  
`git config http.sslVerify false`  
