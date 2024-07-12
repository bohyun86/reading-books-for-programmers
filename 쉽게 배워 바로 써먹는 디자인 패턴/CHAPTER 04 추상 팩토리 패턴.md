# 추상 팩토리 패턴(Abstract Factory Pattern)

#### 패턴유사성(팩토리 패턴, 팩토리 메서드 패턴, 추상 팩토리 패턴)

1. 팩토리 패턴과 팩토리 메서드 패턴 차이: 추상화
2. 팩토리 매서드 패턴과 추상 팩토리 패턴 차이: 추상화된 그룹을 형성하고 관리

#### 추상 팩토리

- 여러 개의 팩토리 메서드를 그룹으로 묶는 것과 유사, 생성 패턴을 그룹 형태로 변경
- 추상 팩토리 사용 목적: 복수의 객체 생성을 담당하는 군집을 관리

#### 추상 팩토리의 장점 단점
장점
1. 생성 패턴을 독립적으로 동작하도록 분리하며 분리된 하나의 그룹별로 객체를 선택하여 생성
2. 추상 팩토리 그룹은 동일한 처리 로직을 갖고 있고, 다른 그룹으로 변경돼도 하위 클래스를 통해 선택적 객체를 다르게 생성

단점
1. 새로운 종류의 군을 추가하는 것이 쉽지 않음
- 모든 서브 클래스들이 동시에 변경돼어야 함
2. 관리할 그룹이 많고 계층의 크기가 커질수록 복잡한 문제가 발생

### 추상 팩토리 패턴 예제
```java
// Abstract Factory Interface
interface AbstractFactory {
    ProductA createProductA();
    ProductB createProductB();
}

// Concrete Factory 1
class ConcreteFactory1 implements AbstractFactory {
    @Override
    public ProductA createProductA() {
        return new ConcreteProductA1();
    }

    @Override
    public ProductB createProductB() {
        return new ConcreteProductB1();
    }
}

// Concrete Factory 2
class ConcreteFactory2 implements AbstractFactory {
    @Override
    public ProductA createProductA() {
        return new ConcreteProductA2();
    }

    @Override
    public ProductB createProductB() {
        return new ConcreteProductB2();
    }
}

// Abstract Product A
interface ProductA {
    void operationA();
}

// Concrete Product A 1
class ConcreteProductA1 implements ProductA {
    @Override
    public void operationA() {
        System.out.println("ConcreteProductA1 operationA");
    }
}

// Concrete Product A 2
class ConcreteProductA2 implements ProductA {
    @Override
    public void operationA() {
        System.out.println("ConcreteProductA2 operationA");
    }
}

// Abstract Product B
interface ProductB {
    void operationB();
}

// Concrete Product B 1
class ConcreteProductB1 implements ProductB {
    @Override
    public void operationB() {
        System.out.println("ConcreteProductB1 operationB");
    }
}

// Concrete Product B 2
class ConcreteProductB2 implements ProductB {
    @Override
    public void operationB() {
        System.out.println("ConcreteProductB2 operationB");
    }
}

// Client
class Client {
    private ProductA productA;
    private ProductB productB;

    public Client(AbstractFactory factory) {
        productA = factory.createProductA();
        productB = factory.createProductB();
    }

    public void executeOperations() {
        productA.operationA();
        productB.operationB();
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        AbstractFactory factory1 = new ConcreteFactory1();
        Client client1 = new Client(factory1);
        client1.executeOperations();

        AbstractFactory factory2 = new ConcreteFactory2();
        Client client2 = new Client(factory2);
        client2.executeOperations();
    }
}
```

이 예제에서는 `AbstractFactory`라는 추상 팩토리 인터페이스가 있으며, `ProductA`와 `ProductB`의 생성 메서드를 선언합니다. 그런 다음 `ConcreteFactory1`과 `ConcreteFactory2`라는 두 개의 구체적인 팩토리가 `AbstractFactory` 인터페이스를 구현하고 해당 제품을 생성하는 구현을 제공합니다.

추상 제품 인터페이스 `ProductA`와 `ProductB`는 구체적인 제품 `ConcreteProductA1`, `ConcreteProductA2`, `ConcreteProductB1`, `ConcreteProductB2`가 구현할 작업을 정의합니다.

클라이언트 클래스 `Client`는 생성자에서 추상 팩토리를 매개변수로 받아 제품을 생성하는 데 사용하고 생성된 제품에 대해 작업을 실행합니다.

`Main` 클래스에서는 추상 팩토리 패턴의 사용법을 보여주기 위해 `ConcreteFactory1`과 `ConcreteFactory2`의 인스턴스를 생성하고 해당 제품에 대해 작업을 생성하고 실행합니다.