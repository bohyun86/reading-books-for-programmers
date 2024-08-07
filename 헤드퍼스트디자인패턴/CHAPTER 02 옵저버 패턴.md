# 옵저버 패턴(Observer Pattern)

- 한 객체의 상태가 바뀌면 그 객체에 의존하는 다른 객체에게 연락이 가고 자동으로 내용이 갱신되는 방식으로 일대다(one-to-many) 의존성을 정의합니다.
- 주제가 데이터를 보내거나(푸시 방식) 옵저버가 데이터를 가져올(풀 방식) 수 있습니다. (일반적으로 풀방식을 권장)

## 요약

1. 주제 객체는 옵저버 객체를 등록하고 삭제하는 메서드를 가지고 있음
2. 옵저버 객체는 주제 객체에 등록되어 있어야 함

## 옵저버 패턴 구성요소

1. 주제(Subject) 인터페이스
2. 구체적인 주제(Concrete Subject) 클래스
3. 옵저버(Observer) 인터페이스
4. 구체적인 옵저버(Concrete Observer) 클래스
5. 클라이언트(Client) 클래스


***느슨한 결합(Loose Coupling)***

- 객체들이 상호작용할 수 있지만, 서로를 잘 모르는 관계

## 디자인 원칙

***상호작용하는 객체 사이에는 가능하면 느슨한 결합을 사용해야 한다.***

- 느슨하게 결합하는 디자인을 사용하면 변경 사항이 생겨도 무난히 처리할 수 있는 유연한 객체지향 시스템을 구축할 수 있음
- 객체 사이의 상호의존성을 최소화

 