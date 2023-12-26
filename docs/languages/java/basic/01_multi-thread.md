---
layout: default
title: 01_Multi Thread
parent: 01_Basic
grand_parent: Java
nav_order: 1
---

# Multi-thread 관련 인터페이스

## 1. Thread와 Runnable의 한계점  
- 쓰레드의 <u>생성과 실행을 저수준의 API</u>에 의존
- 쓰레드 작업이 끝난 후 <u>결과값 반환이 불가</u>
- 매번 쓰레드 <u>생성과 종료 시 오버헤드</u> 발생
- 쓰레드들의 <u>관리가 어려움</u>   


## 2. Callable과 Future  
위의 Thread와 Runnable의 한계점을 보완하기 위해 Java5부터 추가됨  


**1) Callable**  
- 기존의 Runnable 인터페이스는 결과를 반환할 수 없음. (결과값을 얻으려면 공용 메모리나 파이프 등을 사용, 번거로움)  
- Runnable의 발전된 형태로 <u>제네릭을 사용해 결과를 받을 수 있는</u> Callable 인터페이스가 추가됨.  

```java
public interface Callable<V> {
  V call() throws Exception;
}
```


**2) Future**  
- Callable 인터페이스의 구현체인 작업(Task)은 가용 가능한 쓰레드가 없어서 실행이 미뤄지거나, 작업 시간이 오래 걸려 실행 결과를 바로 받지 못할 수 있음.   
- <u>미래에 완료된 Callable의 결과값을 반환</u>받기 위해 Future 인터페이스가 추가됨.   

```java
public interface Future<V> {
  V get() throws InterruptedException, ExecutionException;

  V get(long timeout, TimeUnit unit) throws InterruptedException, ExecutionException, TimeoutException;

  boolean isCancelled();

  boolean isDone();

  boolean cancel(boolean mayInterruptIfRunning)
}
```

<br/>

**(1) V get() throws InterruptedException, ExecutionException**  
- 작업된 결과를 가지고 오는 메서드. 결과가 반환되기 전까지 애플리케이션의 진행을 'block' (결과가 나올 때 까지 기다림)  


**(2) V get(long timeout, TimeUnit unit) throws InterruptedException, ExecutionException, TimeoutException**  
- get() 메서드를 호출한 Thread는 작업 결과가 반환되지 않으면 무한히 대기.  
- 따라서 이 메드로 Timeout 시간을 설정, 설정된 시간 내에 응답이 없으면 'TimeoutException' 예외를 발생 (try-catch로 처리)  

## 3. 쓰레드 풀 (Thread-pool)  
Executors, Executor, ExecutorService  
쓰레드 풀을 위한 Executor, ExecutorService, ScheduledExecutorService  
쓰레드 풀 생성을 도와주는 팩토리 클래스인 Executor  
