# 팩토리 메서드 패턴(Factory Method Pattern)

- 팩토리 패턴과 템플릿 메서드 패턴을 결합하여 사용 
- 추상화 기법을 활용하여 패턴을 확장하고, 추상화를 적용하면 팩토리 메서드 패턴과 추상 팩토리 패턴으로 분리
- 추상 클래스로 변경되면 클래스는 강제적으로 상위 클래스와 하위 클래스로 분리되며, 하위 클래스에 구현을 위임
- 객체의 생성을 군집화하고 군집된 객체를 매개변수로 선택

개방-폐쇄 원칙(Open-Closed Principle)을 적용하여 바뀌지 않는 공통된 부분을 분리하여 관리할 수 있습니다. 팩토리 메서드 코드를 분리할 때 OCP 원칙을 적용할 수 있습니다.

팩토리 메서드는 프레임워크 같은 응용 프로그램에서 많이 이용됩니다. 객체의 생성 과정을 캡슐화하고 이를 분리하여 관리할 수 있기 때문입니다.

## 장점
- 유연성: 팩토리 메서드 패턴은 객체 생성을 캡슐화하고, 이를 하위 클래스에 위임함으로써 유연성을 제공합니다. 새로운 객체를 추가하거나 기존 객체를 변경할 때, 기존 코드를 수정하지 않고도 새로운 객체를 생성할 수 있습니다.
- 확장성: 팩토리 메서드 패턴은 추상화를 통해 객체 생성을 확장할 수 있습니다. 새로운 하위 클래스를 추가하거나 기존 하위 클래스를 변경하여 다양한 객체를 생성할 수 있습니다.
- 유지보수성: 팩토리 메서드 패턴은 객체 생성 코드를 분리하여 관리할 수 있습니다. 이로써 코드의 가독성과 유지보수성을 향상시킬 수 있습니다.

## 단점
- 복잡성: 팩토리 메서드 패턴은 추가적인 추상화 계층을 도입하여 복잡성을 증가시킬 수 있습니다. 이로 인해 코드의 이해와 디버깅이 어려워질 수 있습니다.
- 클래스 수의 증가: 팩토리 메서드 패턴은 객체 생성을 위해 많은 하위 클래스를 생성해야 합니다. 이로 인해 클래스의 수가 증가할 수 있으며, 이는 코드의 복잡성을 증가시킬 수 있습니다.

## 팩토리 메서드 패턴 예제
```java
// 추상 클래스
abstract class Product {
    public abstract void use();
}

// 구체적인 제품 클래스
class ConcreteProductA extends Product {
    @Override
    public void use() {
        System.out.println("ConcreteProductA를 사용합니다.");
    }
}

// 구체적인 제품 클래스
class ConcreteProductB extends Product {
    @Override
    public void use() {
        System.out.println("ConcreteProductB를 사용합니다.");
    }
}

// 팩토리 클래스
class ProductFactory {
    public static Product createProduct(String type) {
        if (type.equals("A")) {
            return new ConcreteProductA();
        } else if (type.equals("B")) {
            return new ConcreteProductB();
        }
        return null;
    }
}

// 클라이언트 코드
public class Main {
    public static void main(String[] args) {
        Product productA = ProductFactory.createProduct("A");
        productA.use(); // ConcreteProductA를 사용합니다.

        Product productB = ProductFactory.createProduct("B");
        productB.use(); // ConcreteProductB를 사용합니다.
    }
}
```

위의 예제에서는 `Product`라는 추상 클래스를 정의하고, `ConcreteProductA`와 `ConcreteProductB`라는 구체적인 제품 클래스를 구현합니다. 그리고 `ProductFactory`라는 팩토리 클래스를 통해 제품을 생성합니다. 클라이언트 코드에서는 `ProductFactory`를 사용하여 원하는 제품을 생성하고 사용합니다.

이 예제는 팩토리 메서드 패턴을 사용하여 객체 생성을 캡슐화하고, 유연성과 확장성을 제공하는 방법을 보여줍니다.



