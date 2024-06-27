# 장식자 패턴(Decorator Pattern)
- 객체에 동적 기능을 추가하기 위해 구조를 개선하는 패턴
- 동적으로 객체를 결합하기 위해서 객체지향의 구성을 통해 확장
- 기본이 되는 객체를 감싸서 새로운 객체로 확장

|구성요소 | 설명|
| --- | --- |
|Component | 인터페이스 정의 |
|ConcreateComponent | 인터페이스에 정의 실제를 구현 |
|Decorator | 컴포넌트를 참조하며 인터페이스를 일치화 |
|ConcreateDecorator | 확장 및 추가되는 기능을 작성 |

## 장단점 및 결과
### 장점
- 상속 형태의 확장보다 더 융통성 있게 설계 가능
- 객체 실행 중 동적으로 기능 추가 가능
- 자원을 동적으로 처리되는 시점에 할당 받아 사용

### 단점
- 많아지는 객체의 수
-- 무조건 단점이지만은 않음. 작은 코드로 이루어진 객체는 이해하기 쉬움

## 예제: 커피 주문 시스템

다음은 커피 주문 시스템을 구현하는 예제입니다.

```java
// 커피 주문 인터페이스
interface Coffee {
    String getDescription();
    double getCost();
}

// 기본 커피 클래스
class SimpleCoffee implements Coffee {
    @Override
    public String getDescription() {
        return "단순한 커피";
    }

    @Override
    public double getCost() {
        return 1.0;
    }
}

// 장식자 추상 클래스
abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;

    public CoffeeDecorator(Coffee decoratedCoffee) {
        this.decoratedCoffee = decoratedCoffee;
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription();
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost();
    }
}

// 설탕 장식자
class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee decoratedCoffee) {
        super(decoratedCoffee);
    }

    @Override
    public String getDescription() {
        return super.getDescription() + ", 설탕";
    }

    @Override
    public double getCost() {
        return super.getCost() + 0.5;
    }
}

// 우유 장식자
class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee decoratedCoffee) {
        super(decoratedCoffee);
    }

    @Override
    public String getDescription() {
        return super.getDescription() + ", 우유";
    }

    @Override
    public double getCost() {
        return super.getCost() + 1.0;
    }
}

// 사용 예시
public class CoffeeOrderSystem {
    public static void main(String[] args) {
        // 기본 커피 주문
        Coffee simpleCoffee = new SimpleCoffee();
        System.out.println("주문: " + simpleCoffee.getDescription());
        System.out.println("가격: $" + simpleCoffee.getCost());

        // 설탕 추가
        Coffee sugarCoffee = new SugarDecorator(simpleCoffee);
        System.out.println("주문: " + sugarCoffee.getDescription());
        System.out.println("가격: $" + sugarCoffee.getCost());

        // 우유 추가
        Coffee milkCoffee = new MilkDecorator(simpleCoffee);
        System.out.println("주문: " + milkCoffee.getDescription());
        System.out.println("가격: $" + milkCoffee.getCost());

        // 설탕과 우유 추가
        Coffee sugarAndMilkCoffee = new SugarDecorator(new MilkDecorator(simpleCoffee));
        System.out.println("주문: " + sugarAndMilkCoffee.getDescription());
        System.out.println("가격: $" + sugarAndMilkCoffee.getCost());
    }
}
```

이 예제에서는 커피 주문 시스템을 구현하기 위해 장식자 패턴을 사용했습니다. `Coffee` 인터페이스는 `getDescription()`과 `getCost()` 메서드를 정의하고, `SimpleCoffee` 클래스는 이 인터페이스를 구현합니다. 

`CoffeeDecorator` 추상 클래스는 `Coffee` 인터페이스를 구현하고, `decoratedCoffee` 멤버 변수를 가지고 있습니다. 이 클래스를 상속받은 `SugarDecorator`와 `MilkDecorator` 클래스는 각각 설탕과 우유를 추가하는 기능을 구현합니다.

`CoffeeOrderSystem` 클래스에서는 다양한 커피 주문을 생성하고, 주문 내용과 가격을 출력합니다. 예를 들어, `SugarDecorator`를 사용하여 설탕을 추가한 커피를 주문할 수 있습니다.

이 예제를 통해 장식자 패턴을 사용하여 동적으로 커피에 기능을 추가하는 방법을 알 수 있습니다.

