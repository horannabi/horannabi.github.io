---
layout: default
title: 02_JWT
parent: 01_Authorization
grand_parent: Web
nav_order: 2
has_children: false
---

# JWT (JSON Web Token)  

## 1. 토큰 기반 인증  
- 토큰 기반 인증 시스템에서는 클라이언트가 서버에 접속을 하면 서버에서 해당 클라이언트에게 인증되었다는 의미로 '토큰'을 부여함.   
- 토큰을 발급받은 클라이언트는 서버에 요청을 보낼 때 요청 헤더에 토큰을 심어서 보냄.  
- 서버에서는 클라이언트로부터 받은 토큰을 서버에서 제공한 토큰과 일치하는지 여부를 체크하여 인증 과정을 처리.  


## 2. JWT(JSON Web Token)란?  
- 웹에서 사용되는 <u>JSON 형식의 토큰에 대한 표준 규격</u>  
- 사용자의 인증(authentication) 또는 인가(authorization) 정보를 서버와 클라이언트 간에 안전하게 주고 받기 위해서 사용
- Claim 기반(다른 토큰과 비교)  
