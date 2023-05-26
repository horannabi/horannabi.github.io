---
layout: default
title: 01_정적생성자
parent: C#
grand_parent: Programming Languages
nav_order: 1
---

# [C#] 정적 생성자 (Static Constructor)

## 1. 호출 시점
- 첫 번째 인스턴스가 만들어지거나 정적 멤버가 참조되기 전에 런타임에 자동으로 호출  
- 런타임은 단일 애플리케이션 도메인에서 정적 생성자를 딱 1번만 호출  

<br/>

## 2. 정적 생성자의 특징
- 액세스 한정자와 매개변수 가질 수 없음  
- 상속, 오버로드 불가  
- 직접 호출 불가 (사용자가 호출 시점 제어 불가)  

<br/>

## 3. 정적 생성자 & 인스턴스 생성자 실행 순서
- 정적 생성자 -> 인스턴스 생성자 순으로 실행
- 정적 필드 변수 이니셜라이저가 정적 생성자의 클래스에 있는 경우 클래스 선언에 나타나는 텍스트 순서대로 실행  
- 이니셜라이저는 정적 생성자가 실행되기 직전에 실행됨  

<br/>

## 4. 정적 필드 초기화
- 정적 필드는 정적 생성자에서만 초기화 가능 (아님 기본값으로 초기화)  
- static readonly로 선언된 필드는 해당 선언의 일부로 또는 정적 생성자에서만 할당   
- 명시적 정적 생성자가 필요하지 않은 경우 런타임 최적화 향상을 위해 정적 생성자를 통하지 않고 선언에서 정적 필드를 초기화  

<br/>
<hr/>

참고: [정적 생성자(C# 프로그래밍 가이드)](https://learn.microsoft.com/ko-kr/dotnet/csharp/programming-guide/classes-and-structs/static-constructors)
