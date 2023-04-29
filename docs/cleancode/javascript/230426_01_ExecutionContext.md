---
layout: default
title: 02_실행컨텍스트
parent: Javascript
grand_parent: Clean Code
nav_order: 2
---

# [JS] 실행 컨텍스트 (Execution Context)  

'[코어 자바스크립트](https://product.kyobobook.co.kr/detail/S000001766397)-Chapter 02_실행 컨텍스트'에 대한 요약 

## 1. 실행 컨텍스트란?  

**실행 컨텍스트 (Execution Context):** 실행할 코드에 대한 환경 정보들을 모아놓은 객체  
동일한 환경에 있는 코드들을 실행할 때 필요한 환경정보들을 모아 컨텍스트를 구성  


실행 컨텍스트를 콜 스택(call stack)에 쌓아올려 가장 위에 쌓여있는 컨텍스트와 관련 있는 코드들을 실행하는 식으로  
전체 코드의 환경과 순서를 보장  
(같은 실행컨택스트 = 동일한 환경)  


**실행 컨택스트 구성방법**  
> 1. 전역공간  
> 2. eval() 함수  
> 3. 함수  

- 전역공간은 자동으로 생성  
- eval()은 문자로 표현 된 JavaScript 코드를 실행하는 함수로, 절대 사용하지 말 것을 권고 (eval() is evil)  
- 따라서 함수 => 흔히 실행 컨택스트를 구성하는 방법


```js
var a = 1;
function outer(){
    function inner(){
        console.log(a);
        var a = 3;
    }
    inner();
    console.log(a);
}
outer();
console.log(a);
```


**전역 컨택스트**  
최상단의 공간, 코드 내부에 별도의 실행 명령이 없어도 브라우저에서 자동으로 실행  
자바스크립트 파일이 열리는 순간 전역 컨택스트가 활성화 됨  


실행 컨택스트가 콜 스택의 맨 위에 쌓이는 순간이 현재 실행할 코드에 관여하게 되는 시점  


어떤 실행 컨택스트가 활성화될 때 자바스크립트 엔진은 해당 컨택스트에 관련된 코드들을 실행하는 데 필요한 환경 정보들을수집해서 실행 컨택스트 객체에 저장.  
이 객체는 자바스크립트 엔진이 활용할 목적으로 생성할 뿐 개발자가 코드를 통해 확인할 수는 없음.  
- **VariableEnvironment:** 현재 컨택스트 내의 식별자들에 대한정보 + 외부 환경 정보  
선언 시점의 LexicalEnvironment의 스냅샷으로, 변경 사항은 반영 되지 않음
- **LexicalEnvironment:** 처음엔 VariableEnvironment와 같지만 변경 사항이 실시간으로 반영됨.  
실행 컨텍스트를 생성할 때 VariableEnvironment에 정보를 먼저 담고 이를 그대로 복사해서 LexicalEnvironment를 만듦
- **ThisBinding:** this 식별자가 바라봐야 할 대상 객체


**VariableEnvironment & LexicalEnvironment**의 내부는  
**envronmentRecord** & o**uter-EnvrionmentReference**로 구성돼 있음  


## 2. LexicalEnvironment  
### 1) environmentRecord와 호이스팅  
**environmentRecord**  
- environmentRecord에는 <u>현재 컨택스트와 관련된 코드의 식별자 정보</u>들이 저장됨.  
컨택스트를 구성하는 함수에 지정된 매개변수 식별자, 선언한 함수가 있을 경우 그 함수 자체, var로 선언된 변수의 식별자등이 식별자에 해당.  
- 컨택스트 내부 전체를 처음부터 끝까지 쭉 훑어나가며 순서대로 수집함.  
<u>따라서 코드가 실행되기 전에도 자바스크립트 엔진은 이미 해당 환경에 속한 변수명을 모두 알고 있음.</u>  


**호이스팅(hoisting)**  
자바스크립트 엔진은 식별자들을 최상단으로 끌어올려놓은 다음 실제 코드를 실행하는 것 처럼 동작 => 호이스팅(hoisting)  
(hoist: '끌어올리다', 실제로 끌어올리진 않지만 편의상 이해하기 쉬운 가상의 개념)  


```js
function a (x) {           // 수집대상 1 (매개변수)
    console.log(x);        // (1)
    var x;                 // 수집대상 2 (변수 선언)
    console.log(x);        // (2)
    var x = 2;             // 수집대상 3 (변수 선언 & 할당)
    console.log(x);        // (3)
}
a(1)
```

LexicalEnvironment 입장에선 인자들과 함께 함수를 호출한 경우(상단의 예시 코드)  코드 내부에서 변수를 선언한 것(하단의 예시 코드)과 같음  

```js
function a () {
    var x = 1;             // 수집대상 1 (매개변수 선언)
    console.log(x);        // (1)
    var x;                 // 수집대상 2 (변수 선언)
    console.log(x);        // (2)
    var x = 2;             // 수집대상 3 (변수 선언 & 할당)
    console.log(x);        // (3)
}
a();
```

호이스팅 처리 결과는 다음과 같음.  
**environmentRecord**는 현재 실행될 컨텍스트의 대상 코드 내에 <u>어떤 식별자들이 있는지</u>만 관심,  
각 식별자에 어떤 값이 할당될 것인지는 관심 X  
<u>따라서 변수명만 끌어올리고 할당 과정은 원래 자리에 둠.</u>  


```js
function a () {
    var x;                 // 수집대상 1의 변수선언 부분
    var x;                 // 수집대상 2의 변수선언 부분
    var x;                 // 수집대상 3의 변수선언 부분

    x = 1;                 // 수집대상 1의 할당 부분
    console.log(x);        // (1)
    console.log(x);        // (2)
    x = 2;                 // 수집대상 3의 할당 부분
    console.log(x);        // (3)
}
a();
```

따라서 출력결과는 다음과 같음   
<div class="code-example" markdown="1">

(1) 1, (2) 1, (3) 2  
*((2)가 undefined가 아님!)*  

</div>

