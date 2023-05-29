---
layout: default
title: 03_Gradle
parent: Eclipse
grand_parent: Dev Tools
nav_order: 3
---

# [Eclipse] Gradle 프로젝트 생성하기  


## 1. Gradle이란?  

**그루비(Grrovy)**를 기반으로 한 **빌드 자동화 도구**이다.  


**빌드 자동화**란 반복되는 코딩을 잘 짜여진 프로세스를 통해 자동으로 실행하여, 믿을 수 있는 결과물도 생산해 낼 수 있는 일련의 작업방식 및 방법을 말한다.  

<hr/>

## 2. 빌드 자동화 도구 비교 (ANT vs Maven vs Gradle)  

새로운 프로젝트를 위해 AS-IS 시스템 분석 중 ANT라는 빌드도구를 알게 되었는데,  
ANT와 이전에 사용해 보았던 Maven, 그리고 TO-BE 시스템에 적용할 Gradle을 비교해보고자 한다.  

<br/>

**[Ant]**
* **XML 기반**으로 빌드 스크립트를 작성
* 형식적인 규칙이 없어 자유롭게 빌드 단위를 지정할 수 있다. (명확한 빌드 절차 정의가 필요)
* 생명주기(Lifecycle)을 갖지 않아서 각각의 target에 대한 의존 관계를 명시해야 한다.
* 스크립트가 정형화 돼 있지 않아 프로젝트가 커지면 스크립트 관리나 빌드 과정이 복잡해지고 유지보수가 어렵다.
* 외부 라이브러리 관리 불가 (관리를 위해 IVY 도입)

**[Maven]**
* **XML 기반**으로 빌드 스크립트를 작성
* 표준화된 포맷을 제공 (pom.xml)
* 생명주기(Lifecycle)와 프로젝트 객체 모델(POM, Project Object Model)이란 개념이 도입됐다.
* 상속 방식으로  멀티 프로젝트 빌드 지원 (멀티 프로젝트 빌드 지원)
* pom.xml에 필요한 라이브러리를 선언하면 자동으로 해당 프로젝트로 불러온다.
* Ant의 장황한 빌드 스크립트를 개선했지만 라이브러리가 서로 의존하는 경우 복잡해질 수 있다.

**[Gradle]**
* Gradle에서는 **groovy 기반의 DSL**을 사용하여 XML에 비해 가독성이 좋음
    * 의존 관계가 복잡하더라도 가독성 좋게 풀어낼 수 있다.
    * 동적인 Build를 Groovy 스크립트로 플러그인을 호출하거나 직접 코드를 짜면 된다. (Java와 문법이 유사)
* 일관된 디렉토리 구조를 가지고 빌드 프로세스를 유지
* **멀티 프로젝트 빌드 지원**
* Configuration Injection(의존성 주입) 방식을 사용→ 상속하지 않아도 됨
* 빌드 속도가 Maven보다 10~100배 빠름.
* 기존의 빌드 스크립트를(ant, maven)을 간단하게 변환할 수 있다.

<hr/>

## 3. 이클립스에서 Gralde 프로젝트 생성하기  

### 1) Gradle Plug-in 다운로드  

> 상단 메뉴에서 **Help → Eclipse Marketplace...** 클릭  

![230413-01](https://user-images.githubusercontent.com/44853626/231641546-b3709472-daf8-43d9-8af7-c9a96c4a4916.png)  

> **'Buildship Gradle Integration 3.0'** 플러그인을 다운받아야 한다.  
> 'Gradle'을 입력하여 검색  
> (이클립스 2020-06버전을 다운받았더니 기본으로 깔려있었음)  
> 버튼에 아래와 같이 'Installed'라고 되어 있거나 Installed 탭에 있으면 다운된 것  

![230413-02](https://user-images.githubusercontent.com/44853626/231641577-5cb9c70a-61ec-4953-9bc3-e7c35de95664.png)  


### 2) 새 프로젝트 생성  

> **'프로젝트 탐색기(Project Exploler)'** 나 **'패키지 탐색기(Package Exploler)'** 에서 **우클릭  
> → New → Project...**  클릭  

![230413-03](https://user-images.githubusercontent.com/44853626/231641588-a580f27e-e979-4da0-a316-b24fb7dfe6d2.png)  

> 'Gradle'로 검색하여 Gradle Project 선택 후 Next  

![230413-04](https://user-images.githubusercontent.com/44853626/231641627-5c8cc6d1-3676-4552-8c14-f76b981db691.png)  

> Gradle의 장점에 대해 소개하는 내용인데 프로젝트 만들 때마다 보고 싶지 않으면 체크박스 풀고 Next  

![230413-05](https://user-images.githubusercontent.com/44853626/231641658-ec8f1fb5-6592-439b-813f-65190e523e56.png)  

> Project name에 이름 적고 Next  
> 아래에선 'GradleTestProject'로 프로젝트명을 만들었다.  

![230413-06](https://user-images.githubusercontent.com/44853626/231644186-783d7e96-9006-439b-9c52-2656cfe17efc.png)

> 현재 Workspace 디폴트 세팅이 Gradle Version 8.1-rc-3 이다.  
> 우선 디폴트 버전으로 두고 Next  

![230413-07](https://user-images.githubusercontent.com/44853626/231644190-77e0d1ba-8f8e-4912-b73e-bfbc0a0c5841.png)  

> 그러면 Gradle Project Structure에 GradleTestProject 밑에 lib가 생성된 것을 볼 수 있다.  
> GradleTestProject 패키지 하위에 lib 패키지가 생성된 것.  
> Finish를 클릭하면 프로젝트가 생성된다.  

![230413-08](https://user-images.githubusercontent.com/44853626/231644191-2d8af5b3-f1e3-49d8-9855-261b32b781d4.png)

> Project Explorer(왼쪽 사진)를 보면  
> GradleTestProject 패키지 하위에 lib 패키지가 생성된 것을 알 수 있다.  
> Package Explorer에서는 오른쪽 사진과 같이 패키지가 분리되어 보인다.  

![230413-09](https://user-images.githubusercontent.com/44853626/231644194-208d006c-cbb8-4d02-8c5e-7215399a704c.png) 
![230413-10](https://user-images.githubusercontent.com/44853626/231644196-f7cdf4f8-3789-4ece-bf4f-2bcc88b2057c.png)  

> GradleTestProject 패키지 안에 settings.gradle을 보면  
> 다음과 같이 'lib'를 include하도록 되어있다.  
> 프로젝트를 여러 개 include 할 수 있어 '멀티 프로젝트 빌드'를 지원한다.  

![230413-11](https://user-images.githubusercontent.com/44853626/231644198-4deeff61-c4bd-4bb8-8a31-c1db0f42de68.png)  

> 여러 프로젝트를 빌드할 필요가 없고 하나의 폴더 안에 모든 세팅과 소스를 관리하고 싶다면  
> 6.6.1 이하의 버전으로 만들어야 한다.  
> 6.6.1 버전으로 'GradleTestProject2'라는 새로운 프로잭트를 만들어 본다.  
> 앞에 과정과 같이 Project Name에 이름 적고 Next  

![230413-12](https://user-images.githubusercontent.com/44853626/231644204-0d34d7c2-e6f0-45b5-bc63-3ec01498f7b7.png)  

> Override workspace settings 체크 후 Specific Gradle Version에 6.6.1 입력 후 Next  

![230413-13](https://user-images.githubusercontent.com/44853626/231644207-12520eb0-8a31-49a9-b95c-2488c3ce9465.png)  

> 아까와 다르게 Gradle project structure에 패키지가 GradleTestProject2 하나만 생성된 것을 확인할 수 있다.  

![230413-14](https://user-images.githubusercontent.com/44853626/231644209-4891bf91-c368-408a-81c3-bcdaf40f541a.png)  

> GradleTestProject와 GradleTestProject2 프로젝트의 구조는 다음과 같이 보인다.  
> Project Explorer(왼쪽 사진)/ Package Explorer(오른쪽 사진)  

![230413-15](https://user-images.githubusercontent.com/44853626/231644211-7b2a5aa3-b3ad-4511-86bd-0963765c578a.png) 
![230413-16](https://user-images.githubusercontent.com/44853626/231644212-59249d3b-aa73-479d-81b9-5e3562362637.png)  

> GradleTestProject2 패키지 안에 디폴트로 생성된 settings.gradle을 보면 패키지를 include하는 부분이 없다.  
> (현재 하위에 생성된 패키지가 없으니 너무나도 당연)  

![230413-17](https://user-images.githubusercontent.com/44853626/231644213-b4e6324d-af2f-4490-b447-3d102e1730f8.png)  

> 단일 프로젝트 구조를 사용하고 싶은데 6.6.1버전보다 상위 버전을 쓰고 싶다면 아래 블로그를 참조.  
> [https://jiurinie.tistory.com/123](https://jiurinie.tistory.com/123) 

<hr/>

참고:  
[Gradle 홈페이지]  
[https://gradle.org](https://gradle.org)  


[블로그]  
- ANT vs Maven vs Gradle  
[https://madplay.github.io/post/what-is-gradle](https://madplay.github.io/post/what-is-gradle)  
[https://velog.io/@yeseolee/JAVA-Build-Tool-Ant-Maven-Gradle](https://velog.io/@yeseolee/JAVA-Build-Tool-Ant-Maven-Gradle)  
[https://jaehoney.tistory.com/209](https://jaehoney.tistory.com/209)  
[https://blog.naver.com/rorean/222236619759](https://blog.naver.com/rorean/222236619759)  
- Gradle 프로젝트 설치 방법  
[https://jiurinie.tistory.com/123](https://jiurinie.tistory.com/123)  
