# CHAPTER 11 프록시 패턴(Proxy Pattern)

- 원격 객체의 로컬 대변자 역할을 함
- 로컬 대변자: 로컬 대변자의 어떤 메소드를 호출하면, 다른 원격 객체에게 그 메소드 호출을 전달해 주는 객체
- 프록시 패턴은 객체의 대리자 역할을 하는 객체를 제공하여 객체의 접근을 제어하거나 객체의 생성을 지연하는 패턴
- 특정 객체로의 접근을 제어하는 대리인(특정 객체를 대변하는 객체)을 제공합니다.

## 프록시 패턴 구성 요소

- Subject(주제) : 실제 서비스를 제공하는 객체와 프록시 객체가 구현해야 하는 인터페이스
- RealSubject(실제 주제) : 실제 서비스를 제공하는 객체
- Proxy(대변자) : 실제 서비스를 제공하는 객체에 대한 참조자를 가지고 있으며, 실제 서비스를 제공하는 객체의 인터페이스와 동일한 인터페이스를 구현


## RMI(Remote Method Invocation)

- 원격 객체를 사용하기 위한 자바의 표준 기술
- RMI에서 클라이언트 보조 객체는 스텁(stub), 서비스 보조 객체는 스켈레톤(skeleton)이라고 함

## 프록시의 종류

- 가상 프록시(Virtual Proxy) : 실제 객체의 생성을 지연하는 프록시
- 원격 프록시(Remote Proxy) : 원격 객체에 대한 로컬 대리자 역할을 하는 프록시
- 보호 프록시(Protection Proxy) : 실제 객체에 대한 접근을 제어하는 프록시
- 스마트 프록시(Smart Proxy) : 실제 객체에 대한 접근을 제어하거나 추가적인 기능을 제공하는 프록시
- 캐싱 프록시(Caching Proxy) : 실제 객체의 결과를 캐싱하여 동일한 요청에 대한 결과를 캐싱된 결과를 반환하는 프록시
- 동적 프록시(Dynamic Proxy) : 프록시 객체를 동적으로 생성하는 프록시
- 동기화 프록시(Synchronization Proxy) : 다중 스레드 환경에서 실제 객체에 대한 접근을 동기화하는 프록시
- 복잡도 숨김 프록시(Complexity Hiding Proxy) : 복잡한 객체에 대한 접근을 숨기는 프록시
- 지연 복사 프록시(Copy-on-Write Proxy) : 복사를 지연하는 프록시