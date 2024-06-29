# 파사트 패턴(Pacade Pattern)
- 파사드 패턴은 메인 시스템과 서브 시스템 중간에 위치
- 새로운 인터페이스 계층을 추가하여 시스템 간 의존성 해결
- 파사드의 인터페이스 계층은 '겉모습', '건물의 정면'과 같이 접근 할 수 있는 하나의 통로 역할만 담당
- 싱글턴 추상 팩토리라고 불리기도 함

## 최소 지식 원칙 적용이 중요
- 자기 자신만의 객체 사용
- 메서드에 전달된 매개변수 사용
- 메서드에서 생성된 객체 사용
- 객체에 속하는 메서드 사용

```java
// Subsystem 1
class Subsystem1 {
    public void operation1() {
        System.out.println("Subsystem 1: operation 1");
    }
}

// Subsystem 2
class Subsystem2 {
    public void operation2() {
        System.out.println("Subsystem 2: operation 2");
    }
}

// Facade
class Facade {
    private Subsystem1 subsystem1;
    private Subsystem2 subsystem2;

    public Facade() {
        subsystem1 = new Subsystem1();
        subsystem2 = new Subsystem2();
    }

    public void facadeOperation() {
        subsystem1.operation1();
        subsystem2.operation2();
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.facadeOperation();
    }
}
```