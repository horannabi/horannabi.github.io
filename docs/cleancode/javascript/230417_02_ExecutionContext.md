---
layout: default
title: 02_실행컨텍스트
parent: Javascript
grand_parent: Clean Code
nav_order: 2
---

# [JS] 실행 컨텍스트 (Execution Context)  

<u>[코어 자바스크립트](https://product.kyobobook.co.kr/detail/S000001766397)-Chapter 02_실행 컨텍스트에 대한 요약</u>  

## 1. 실행 컨텍스트란?  

**실행 컨텍스트 (Execution Context):** 실행할 코드에 대한 환경 정보들을 모아놓은 객체  
동일한 환경에 있는 코드들을 실행할 때 필요한 환경정보들을 모아 컨텍스트를 구성  
실행 컨텍스트를 구성하는 방법: 전역공간, eval() 함수, 함수  

실행 컨텍스트를 콜 스택(call stack)에 쌓아올려 가장 위에 쌓여있는 컨텍스트와 관련 있는 코드들을 실행하는 식으로  
전체 코드의 환경과 순서를 보장  
