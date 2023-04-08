---
layout: default
title: 02_DB Connection 추가 (오라클)
parent: DBeaver
grand_parent: Dev Tools
nav_order: 2
---

## [DBeaver] DB Connection 연결 (오라클)  

### 1. 콘센트 모양 클릭  

<hr style="border:0; height:1px;"/>

![230406_01](https://user-images.githubusercontent.com/44853626/230562352-e07efa76-05aa-4df5-98ad-10ab9b18f520.png)
<br/>

### 2. DB 종류 선택
<hr/>

오라클 DB를 연결할 것이므로 오라클 선택  
![230406_02](https://user-images.githubusercontent.com/44853626/230266744-42ae07c6-32b1-416c-ad33-1610be840176.png)
<br/>

### 3. 연결할 DB 정보 입력
<hr/>

- Host와 Port에 각각 오라클 서버 IP/Port 입력  
- Database Server Name으로 입력할 경우  
  Enterprise 버전 디폴트 값은 ORCL, Express 버전 디폴트 값은 XE이다.  
  Service Name이 설정된 경우엔 설정된 Service Name을 입력해준다.  
- DB 정보 입력 후 Test Connection 클릭  

![230406_03](https://user-images.githubusercontent.com/44853626/230266770-81b79d93-2032-43ca-ae59-739a3184d0bc.png)
<br/>

### 4. Test Connection
<hr/>

Oracle Driver가 없으면 자동으로 다운받을 수 있게 창이 뜬다.  
Custom ojdbc를 사용할 거 아님 그대로 확인을 누르면 Connection 연결에 성공할 경우 다음과 같은 창이 뜬다.  
확인을 누르고 완료를 누르면 DB Connection 추가 완료.  
![230406_04](https://user-images.githubusercontent.com/44853626/230266785-35209505-5abd-495e-992e-e14032085514.png)  
<br/>
