# 방문자 패턴(Visitor Pattern)

- 공통된 객체의 데이터 구조와 처리를 분리
- 분산된 객체에서 공통된 처리 로직만 분리
- 공통된 로직 구도를 별도의 객체로 분리
- 이렇게 하면 데이터를 갖고 있는 객체는 크게 수정하지 않고도 행위를 쉽게 변경 가능
- 방문자와 원소 객체 간의 양방향 의존 관계 가짐

### 원소

- 데이터를 보관하는 구조 클래스
- 외부 접근 허용 위해 accept 메서드 추가로 가짐
- accept는 외부의 Visitor를 전달 받도록 설계
- 이후 Visitor 객체의 order 메서드를 실행

## 방문자 패턴 예제

```java
// Visitor interface
interface Visitor {
    void visit(ElementA element);
    void visit(ElementB element);
}

// Concrete Visitor
class ConcreteVisitor implements Visitor {
    @Override
    public void visit(ElementA element) {
        // Perform specific operations on ElementA
    }

    @Override
    public void visit(ElementB element) {
        // Perform specific operations on ElementB
    }
}

// Element interface
interface Element {
    void accept(Visitor visitor);
}

// Concrete Elements
class ElementA implements Element {
    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

class ElementB implements Element {
    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        Element elementA = new ElementA();
        Element elementB = new ElementB();

        Visitor visitor = new ConcreteVisitor();

        elementA.accept(visitor);
        elementB.accept(visitor);
    }
}
```

방문자 패턴은 다음과 같은 상황에서 유용하게 사용될 수 있습니다:

1. 객체 구조와 처리 로직의 분리: 방문자 패턴을 사용하면 객체의 데이터 구조와 처리 로직을 분리할 수 있습니다. 이는 객체를 수정하지 않고도 새로운 처리 로직을 추가하거나 변경할 수 있게 해줍니다.

2. 분산된 객체에서 공통된 처리 로직 분리: 방문자 패턴은 분산된 객체들 사이에서 공통된 처리 로직을 분리할 수 있습니다. 이는 객체들 간의 중복 코드를 제거하고 유지보수성을 향상시킬 수 있습니다.

3. 다양한 종류의 객체에 대한 처리 로직 추가: 방문자 패턴을 사용하면 새로운 종류의 객체에 대한 처리 로직을 쉽게 추가할 수 있습니다. 새로운 Visitor 클래스를 작성하여 해당 객체에 대한 처리를 구현하면 됩니다.

4. 객체 간의 양방향 의존 관계: 방문자 패턴은 방문자와 원소 객체 간의 양방향 의존 관계를 가질 수 있습니다. 이는 객체들 간의 상호작용을 유연하게 설계할 수 있게 해줍니다.

이러한 상황에서 방문자 패턴을 사용하면 코드의 유연성과 확장성을 향상시킬 수 있습니다.