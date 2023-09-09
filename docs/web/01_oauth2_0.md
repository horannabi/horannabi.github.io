---
layout: default
title: Oauth 2.0
parent: Web
nav_order: 1
has_children: false
---

# OAuth 2.0  

## 1. OAuth 2.0 란?  

### 1) OAuth 2.0 정의  
- 인터넷 사용자들이 비밀번호를 제공하지 않고 웹사이트나 애플리케이션에 대한 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, <u>접근 위임을 위한 개방형 표준</u>  

- OAuth는 사용자가 누구인지를 확인하는 인증(Authentication) 프로토콜이 아닌, 사용자의 요청이 <u>권한이 있는지를 확인하는 인가(Authorization) 프로토콜</u>  


### 2) OAuth 2.0의 등장 배경
- OAuth와 같은 인증방식의 표준이 없었을 때는 기본인증인 아이디와 비밀번호를 사용함.  
이 방식은 보안상 취약한 구조일 가능성이 매우 많으며, 기본 인증이 아닐 경우는 각 애플리케이션들이 각자의 개발한 회사의 방법대로 사용자를 확인함.  

- OAuth는 이렇게 제 각각인 <u>인증방식을 표준화</u>하여 OAuth를 이용하면 이 인증을 공유하는 애플리케이션끼리는 별도의 인증이 필요없음.  
따라서 여러 애플리케이션을 통합하여 사용하는 것이 가능하게 됨.  


### 3) OAuth 구성요소

|구분|설명|
|----|------------|
|Resource Owner|- 리소스 소유자 또는 사용자. 보호된 자원에 접근할 수 있는 자격을 부여해 주는 주체. <br/>- OAuth2 프로토콜 흐름에서 클라이언트를 인증(Authorize)하는 역할을 수행. 인증이 완료되면 권한 획득 자격(Authorization Grant)을 클라이언트에게 부여. <br/>- 리소스 소유자가 자격을 부여하는 것이지만 일반적으로 권한 서버가 리소스 소유자와 클라이언트 사이에서 중개 역할을 수행|
|Client|보호된 자원을 사용하려고 접근 요청을 하는 애플리케이션|
|Resource Server|사용자의 보호된 자원을 호스팅하는 서버|
|Authorization Server|권한 서버. 인증/인가를 수행하는 서버로 클라이언트의 접근 자격을 확인하고 Access Token을 발급하여 권한을 부여하는 역할을 수행|


### 4) OAuth 주요 개념

|구분|설명|
|----|------------|
|Authentication|인증, 접근 자격이 있는지 검증하는 단계|
|Authorization|인가, 자원에 접근할 권한을 부여하는 것. 인가가 완료되면 리소스 접근 권한이 담긴 Access Token이 클라이언트에게 부여됨|
|Access Token|리소스 서버에게서 리소스 소유자의 보호된 자원을 획득할 때 사용되는 만료 기간이 있는 Token|
|Refresh Token|Access Token 만료시 이를 갱신하기 위한 용도로 사용하는 Token. Refresh Token은 일반적으로 Access Token보다 만료 기간이 김.|

<hr/>

## 2. OAuth 2.0 인증 종류  

|구분|설명|
|----|------------|
|1. Authorization Code Grant <br/> (권한 부여 승인 <br/> 코드 방식)|**권한 부여 승인을 위해 자체 생성한 Authorization Code를 전달** <br/><br/>- 많이 쓰이고 기본이 되는 방식 <br/>- 클라이언트가 사용자를 대신하여 특정 자원에 접근을 요청할 때 사용. 보통 타사의 클라이언트에게 보호된 자원을 제공하기 위한 인증에 사용 → <u>간편 로그인 기능</u>에서 사용 <br/>- Refresh Token 사용 가능|
|2. Implicit Grant <br/> (암묵적 승인 방식)|**권한 부여 승인 코드 없이 바로 Access Token 발급** <br/><br/>- 자격증명을 안전하게 저장하기 힘든 클라이언트(예 - JavaScript등 스크립트 언어를 사용한 브라우저)에게 최적화된 방식 <br/>- 권한 서버는 client_secret를 사용해 클라이언트를 인증하지 않음. Access Token을 획득하기 위한 절차가 간소화되기에 응답성과 효율성은 높아지지만 Access Token이 URL로 전달된다는 단점이 있음. <br/>→ 만료기간을 짧게 설정하여 누출의 위험을 줄일 필요가 있음 <br/>- Refresh Token 사용 불가능|
|3. Resource Owner Password Credentials Grant <br/> (자원 소유자 자격증명 <br/> 승인 방식)|**username, password로 Access Token을 받는 방식** <br/><br/>- 권한 서버, 리소스 서버, 클라이언트가 모두 같은 시스템에 속해 있을 때 사용되어야 하는 방식. <br/>→ 자신의 서비스에서 제공하는 어플리케이션일 경우에만 사용되는 인증 방식. 다른 회사의 외부 프로그램의 경우 적용하면 안 됨. <br/>- Refresh Token 사용 가능|
|4. Client Credentials Grant <br/> (클라이언트 자격증명 <br/> 승인 방식)|**클라이언트의 자격증명만으로 Access Token을 획득하는 방식** <br/><br/>- 가장 간단한 방식 <br/>- 클라이언트 자신이 관리하는 리소스 혹은 권한 서버에 해당 클라이언트를 위한 제한된 리소스 접근 권한이 설정되어 있는 경우 사용 <br/>- 자격증명을 안전하게 보관할 수 있는 클라이언트에서만 사용 <br/>- Refresh Token 사용 불가능|

