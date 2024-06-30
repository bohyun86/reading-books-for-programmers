# 팩토리 패턴(Factory Pattern)

1. 팩토리 패턴의 목적은 객체 생성 시 발생하는 강력한 의존 관계를 보다 느슨하게 만드는 것입니다.
2. 실제 코드가 `new` 키워드를 직접 사용하지 않고 팩토리 객체를 호출하는 것으로 대체합니다.
3. 객체 생성을 전담하는 클래스를 생성합니다.

**단순팩토리**: 팩토리 객체를 생성하지 않고 객체 생성 전용 메소드를 추가합니다.

**패턴 연구자들 중에서는 단순 팩토리 패턴을 생성 패턴에 포함시키지 않는 경우도 있습니다.**

### 팩토리 패턴 장점

1. 사용과 생성을 분리하여 중복된 코드를 정리할 수 있습니다.
2. 유연성과 확장성을 개선할 수 있습니다. (코드 수정 없이 팩토리 객체를 통해 클래스를 변경할 수 있습니다.)
3. 어떤 객체를 생성할지 모르는 초기 단계 코드에 유용합니다.

## 팩토리 패턴 예제
```java
// Product interface
interface Product {
    void use();
}

// Concrete Product A
class ConcreteProductA implements Product {
    @Override
    public void use() {
        System.out.println("Using Concrete Product A");
    }
}

// Concrete Product B
class ConcreteProductB implements Product {
    @Override
    public void use() {
        System.out.println("Using Concrete Product B");
    }
}

// Factory class
class Factory {
    public static Product createProduct(String type) {
        if (type.equals("A")) {
            return new ConcreteProductA();
        } else if (type.equals("B")) {
            return new ConcreteProductB();
        } else {
            throw new IllegalArgumentException("Invalid product type.");
        }
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        Product productA = Factory.createProduct("A");
        productA.use();

        Product productB = Factory.createProduct("B");
        productB.use();
    }
}
```